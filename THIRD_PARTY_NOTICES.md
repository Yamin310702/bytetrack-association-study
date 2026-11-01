# Third-party sources and assistance

## ByteTrack / YOLOX-based official source

Yifu Zhang et al., *ByteTrack: Multi-Object Tracking by Associating Every Detection Box*, ECCV2022. Official repository: https://github.com/FoundationVision/ByteTrack . This project attributes the tracking algorithm, detector architecture, checkpoint and original implementation to their authors.

The notebooks fetch a pinned official revision and apply disclosed compatibility/ablation edits. ByteTrack's MIT notice is preserved in [licenses/ByteTrack-MIT.txt](licenses/ByteTrack-MIT.txt). Original copyright headers remain in fetched source. This repository does not redistribute the whole upstream repository or pretrained checkpoint. Check upstream notices for its third-party components.

## Evaluator and dataset

TrackEval: https://github.com/JonathonLuiten/TrackEval . The notebooks fetch a pinned revision and record NumPy compatibility changes. Follow the upstream evaluator's license and citation instructions.

MOT17: https://motchallenge.net/data/MOT17/ . Dataset media and ground-truth annotations are not included here. Obtain them from the original publisher and follow their distribution/use terms.

## Project materials

Notebook scaffolding, experiment guidance and documentation received AI assistance. Recorded experiments were executed in the user's Google Colab sessions; reported metrics come from their returned experiment archives. Public availability does not establish compliance with a course's rules. Follow the instructor's policy for assessed submissions and independently explain the work.
