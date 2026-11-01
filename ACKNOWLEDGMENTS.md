# Acknowledgements and assistance

## ByteTrack / YOLOX-based official source

Yifu Zhang et al., *ByteTrack: Multi-Object Tracking by Associating Every Detection Box*, ECCV2022. Official repository: https://github.com/FoundationVision/ByteTrack . This project attributes the tracking algorithm, detector architecture, checkpoint and original implementation to their authors.

The notebooks fetch a pinned official revision and apply disclosed compatibility/ablation edits. ByteTrack's MIT notice is preserved in [licenses/ByteTrack-MIT.txt](licenses/ByteTrack-MIT.txt). Original copyright headers remain in fetched source. This repository does not redistribute the whole upstream repository or pretrained checkpoint. Check upstream notices for its third-party components.

## Evaluator and dataset

TrackEval: https://github.com/JonathonLuiten/TrackEval . The notebooks fetch a pinned revision and record NumPy compatibility changes. Follow the upstream evaluator's license and citation instructions.

MOT17: https://motchallenge.net/data/MOT17/ . Selected cropped/annotated comparison clips and keyframes derived from MOT17-02-FRCNN are included under `assets/`, with attribution and transformation details in [docs/visual_examples.md](docs/visual_examples.md). Full source sequences and ground-truth annotation files are not included. Dataset imagery is not covered by the ByteTrack MIT license. Obtain them from the original publisher and follow their distribution/use terms.

## Project Materials

This project is based on the original ByteTrack algorithm and implementation by Yifu Zhang et al., using the MOT17 dataset and TrackEval for evaluation.

I ran experiments in Google Colab and compared Full ByteTrack with a high-confidence-only variant. I also examined pedestrian recovery, identity changes, and potential tracking errors using experimental results and visual examples.

AI assistance was used to develop notebook code. I reviewed the code, executed the experiments, and analyzed the results. The original algorithm, dataset, and evaluation tools are credited to their respective authors.
