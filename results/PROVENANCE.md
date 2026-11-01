# 결과 파일의 출처

아래 원본 실험 기록에서 추출했습니다. ZIP 자체, GT, 영상, 이미지, detector caches 및 모델 가중치는 저장소에 포함하지 않습니다.

| 원본 기록 | SHA256 |
|---|---|
| ByteTrack_official_MOT17_halfval_results-2.zip | `9327bd67465d5bfa75d81438c6e3a275cb217192428976c12f449d7b4e87bd51` |
| ByteTrack_official_controlled_comparison.zip | `992683d55cdf1f5334a42f04df718d89b534887d3e190bd6418db35d2d7078a1` |
| ByteTrack_visual_examples.zip | `c03e3f28031546353fb2b7ac2a777d7a3484464e793d4e2b75a4b3d6b4a6b06e` |
| ByteTrack_identity_change_example.zip | `d463a27e53419d6f46a84bdb25cf3fcf84a254bea5391ccdbc1b09d30082e1d6` |

`comparison.csv`는 두 버전의 장면별/전체 점수입니다. `full_minus_high_only.csv`는 같은 조건의 차이이며, `full_minus_previous_baseline.csv`는 Full이 이전 baseline을 재현했는지 확인합니다. `*_checks.json`은 노트북 실행 중 기록한 점검 결과로서 독립적인 재실행을 의미하지 않습니다.

`split_info.json`에서는 Colab의 일시적 이미지 경로만 제거했습니다. 프레임 범위, 해상도와 점수는 변경하지 않았습니다. `identity_timeline.csv`는 시각 분석용 best-overlap 기록이며 TrackEval의 공식 ID-switch 사건 로그가 아닙니다.

The summary rows are recorded outputs, not a promise that a fresh Colab runtime reproduces every decimal. The notebooks and exact upstream/checkpoint identifiers explain how to repeat the experiment.
