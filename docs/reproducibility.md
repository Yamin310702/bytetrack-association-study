# 실험 조건과 재현 절차

## 고정한 구성

- ByteTrack revision: `d1bf0191adff59bc8fcfeaa0b33d3d1642552a99`.
- TrackEval revision: `12c8791b303e0a0b50f753af204249e622d0281a`.
- Detector: official YOLOX-X ablation checkpoint, `bytetrack_ablation.pth.tar`.
- Checkpoint SHA256: `26cb8d2808664e5068a4c812d53becbc948b47fd6eacf2b45db049ab40c48b1a`.
- 기록한 환경: Tesla T4, Python 3.13.16, PyTorch 2.11.0+cu130, torchvision 0.26.0+cu130, NumPy 2.1.3.
- Detector input: 800 × 1440, FP16 model, fused convolutions, confidence cutoff 0.01, NMS 0.7.
- Post-NMS cache: 7-column float32, without recasting. The model itself runs in FP16.
- track_thresh=0.6, match_thresh=0.9, mot20=False.
- track_buffer=30, except MOT17-05:14 and MOT17-13:25; BYTETracker uses the original evaluator's default frame_rate=30 convention.
- Output filters: area >100 and width/height ≤1.6.

Exact settings are also in [environment.json](../results/environment.json) and [run_info.json](../results/run_info.json). Package versions describe the completed run; installing into a later Colab session may require compatibility checks.

## 프레임 분할

Scenes: MOT17-02,04,05,09,10,11,13, using FRCNN-named copies only. There are 2,652 selected frames, not 21 independent scenes. Original one-based validation frames are `N//2+2` through `N`, matching the source converter's indexing. Predictions and GT both use new one-based validation indices. Tracker state resets at validation start.

## 실행

1. Run `ByteTrack_Official_MOT17_HalfVal_Colab.ipynb` on a Colab GPU. Set `ALL_SEQUENCES=True`. Inspect GT overlays, set `ALIGNMENT_CHECKED=True`, then continue.
2. Save the baseline result ZIP.
3. Run `ByteTrack_Official_Controlled_Comparison_Colab.ipynb`. It downloads/reuses the same source and checkpoint, checks the ablation, and computes YOLOX outputs once.
4. Both variants replay the same cache, with independent array copies because the original tracker rescales boxes in place. Empty-detection frames advance both trackers. Cache hashes are checked after replay.
5. TrackEval uses standard MOT17 preprocessing for ignored/distractor annotations. Read `comparison.csv` and `full_minus_high_only.csv`, then download the result ZIP.
6. Compare `full_minus_previous_baseline.csv`: the submitted record contains zero differences for all scores/counts. Later environments may produce numerical differences; inspect them before interpreting a change.

## 통제한 변경

The high-only tracker changes only:

```python
inds_second = np.logical_and(inds_low, inds_high)
```

to:

```python
inds_second = np.zeros_like(scores, dtype=bool)
```

The notebook records the source diff and synthetic checks. It does not remove every instruction in the second-stage code path; this is an accuracy ablation, not a clean runtime-speed study.

## 원 코드와 다른 실행 부분

Compatibility edits replace deprecated NumPy aliases and disable GUI keyboard waiting. A documented inference wrapper handles original JPEG frames, explicit frame indices and empty detections. TrackEval replaces the old script's summary, and COCO AP is not computed. These are documented reproduction conditions rather than a claim that every original evaluation-script step is unchanged.

Recorded tracking call times include wrapper effects and fixed execution order. They do not support an unbiased speedup claim.
