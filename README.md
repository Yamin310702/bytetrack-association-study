# ByteTrack Association Study

공식 YOLOX + ByteTrack 구현을 이용한 **저신뢰도 2차 연관 단계의 통제 비교**입니다. 컴퓨터비전 수업의 재현·분석 프로젝트이며 새로운 추적 알고리즘을 제안한 결과는 아닙니다.

English: Reproduction and controlled ablation of ByteTrack's low-confidence association, using identical cached YOLOX detections.

## 연구 질문

동일한 검출 결과와 추적 설정에서 저신뢰도 2차 연관을 사용하면, 보행자의 ID 유지와 미검출·오탐지에 어떤 변화가 나타나는가?

## 완료한 실험

- 원 저자들의 YOLOX-X ablation 체크포인트와 BYTETracker 실행.
- MOT17의 고유 장면 7개, 문서화한 half-validation 구간 **2,652 프레임** 평가.
- Full ByteTrack과 high-confidence-only 변형에 **같은 검출 캐시** 입력.
- High-only는 저신뢰도 후보 마스크만 비우고 다른 설정은 유지.
- 문서화한 추론 래퍼와 TrackEval을 통한 평가.

High-only는 **SORT 전체 구현이 아닌 ByteTrack ablation**입니다. 데이터셋의 FRCNN 접미사는 장면 복제본 이름이며, 본 실험의 검출기는 YOLOX입니다.

## 전체 결과

| 지표 | High-only | Full ByteTrack | Full − High-only |
|---|---:|---:|---:|
| MOTA | 76.83 | 77.93 | +1.09 pp |
| IDF1 | 77.59 | 79.97 | +2.38 pp |
| HOTA | 66.46 | 67.94 | +1.49 pp |
| ID switches | 196 | 173 | −23 |
| False positives | 1,697 | 2,633 | +936 |
| False negatives | 10,591 | 9,090 | −1,501 |

차이는 반올림 전 수치로 계산합니다. 원본 수치와 장면별 결과는 [comparison.csv](results/comparison.csv), 변화량은 [full_minus_high_only.csv](results/full_minus_high_only.csv)에 있습니다.

전체 추적 성능과 미검출은 개선되지만 오탐지는 증가했습니다. 모든 장면에서 같은 이득을 얻지는 않았습니다. 이 표는 본 프로젝트의 측정값이며 원 논문의 표를 옮긴 값이 아닙니다.

## Colab 실행 순서

각 노트북을 Google Colab의 **File → Upload notebook**으로 열고 위에서부터 실행하세요. 노트북의 설치·체크포인트·데이터 준비 셀을 포함해 실행합니다.

| 순서 | 노트북 | 목적 | 환경 |
|---|---|---|---|
| 1 | [First Run](notebooks/ByteTrack_Official_First_Run_Colab.ipynb) | 공식 코드의 짧은 영상 실행 확인 | GPU |
| 2 | [MOT17 Half-validation](notebooks/ByteTrack_Official_MOT17_HalfVal_Colab.ipynb) | baseline 평가. 전체 평가 시 ALL_SEQUENCES=True | GPU |
| 3 | [Controlled Comparison](notebooks/ByteTrack_Official_Controlled_Comparison_Colab.ipynb) | 동일 검출 캐시로 Full/High-only 비교 | GPU |
| 4 | [Visual Examples](notebooks/ByteTrack_Visual_Examples_Colab.ipynb) | 저장한 결과를 영상으로 검토 | CPU |
| 5 | [Identity Change](notebooks/ByteTrack_Identity_Change_Example_Colab.ipynb) | G32의 ID 연속성 사례 검토 | CPU |

Colab 바로 열기: [Baseline 평가](https://colab.research.google.com/github/Yamin310702/bytetrack-association-study/blob/main/notebooks/ByteTrack_Official_MOT17_HalfVal_Colab.ipynb) · [통제 비교](https://colab.research.google.com/github/Yamin310702/bytetrack-association-study/blob/main/notebooks/ByteTrack_Official_Controlled_Comparison_Colab.ipynb)

처음 세 단계는 pretrained detector를 사용하며 새 학습은 필요하지 않습니다. 공식 MOT17 이미지 ZIP은 약 5.5 GB입니다. 결과 ZIP은 각 단계에서 내려받아 보관하며, 시각화 단계에는 3단계의 결과 ZIP이 필요합니다. GPU 제공 여부와 실행 시간은 Colab 세션에 따라 달라집니다.

## 재현 및 해석 자료

- [실험 조건과 재현 절차](docs/reproducibility.md)
- [시각 사례와 해석 한계](docs/visual_examples.md)
- [향후 개선 계획](docs/future_work.md)
- [결과 파일의 출처](results/PROVENANCE.md)
- [원 코드와 제3자 자료의 출처](ACKNOWLEDGEMENTS.md)

## 참고자료

- Yifu Zhang et al. *ByteTrack: Multi-Object Tracking by Associating Every Detection Box*. ECCV 2022. [Paper](https://arxiv.org/abs/2110.06864), [official code](https://github.com/FoundationVision/ByteTrack).
- [MOT17 dataset](https://motchallenge.net/data/MOT17/).
- [TrackEval evaluator](https://github.com/JonathonLuiten/TrackEval).
