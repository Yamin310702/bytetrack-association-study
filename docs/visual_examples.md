# 시각 사례

시각화는 동일한 원본 프레임에서 High-only를 왼쪽, Full ByteTrack을 오른쪽에 표시합니다. 원본 영상이나 정답 주석은 이 저장소에 재배포하지 않습니다. 두 시각화 노트북은 사용자가 받은 MOT17 이미지와 자신의 결과 ZIP으로 사례를 생성합니다.

## 회복 사례

- Sequence: MOT17-02-FRCNN.
- Original frames 369–376; representative frame 373.
- Scored ground-truth identity G39.
- Full ByteTrack retains T28; frame373 score0.15 and GT IoU about0.833.
- High-only has no close matching prediction on that pedestrian.

This illustrates retaining a useful low-confidence observation. It does not prove every long-term occlusion can be recovered.

## 국소적인 ID 연속성 문제

Same annotated pedestrian G32 in MOT17-02:

| Original frame | High-only | Full ByteTrack |
|---|---|---|
| 350 | T26 | T26 |
| 357 | T26 | T36 |
| 365 | T26 | T26 |

Saved best-overlap assignments show Full T26 through351, T36 at352–362, and T26 again from363. High-only retains T26 throughout348–367. The keyframes show the same foreground pedestrian carrying a backpack. This is a visual/coordinate continuity observation, not an independent replay identifying particular TrackEval IDSW events or the exact internal cause.

## 이전의 먼 사람 후보에 대한 주의

An earlier crop around MOT17-11 frame790 contained extra predictions without matching GT. Distant human figures are visible. This is not proof of a nonexistent-person detection. Missing annotations, reflections/depictions, or localization errors are possible explanations. Do not present that crop as an unambiguous background false positive.
