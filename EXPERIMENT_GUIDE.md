# VITON experiment inputs and outputs

Start from the repository root and set the locations in [config.py](config.py). The default dataset root is `data/VITON_V8`. This repository includes a data placeholder; supply the actual person and garment images, pose keypoints, parsing images, prepared cloth masks, and train/test pair lists.

| Step | Entry | What passes to the next step |
|---|---|---|
| Index pairs | [001_make_Dataset.py](001_make_Dataset.py) | Reads `train_pairs.txt` and `test_pairs.txt`; writes the `Training_Set` and `Testing_Set` records to `data/viton_annotations.pkl` by default. |
| Train | [002_train_gmm.py](002_train_gmm.py) | Uses the indexed examples for the warping network and lightweight generator. |
| Generate test images | [003_test.py](003_test.py) | Expects `RootCheckpoint/checkpoint.best.pth.tar` with both `GMM_state_dict` and `GEN_state_dict`. Writes corresponding PNGs under `results/for_evaluate/img/real/` and `fake/`. |
| Score | [004_evaluation.py](004_evaluation.py) | Reads those two image directories and prints SSIM, LPIPS, and FID. Keep the input pair list, checkpoint, and generated image set together when recording a run. |

The [related CAFANet paper](https://github.com/Chi-An-Chen/CAFANet/blob/cab683cf242aba0047c9a1407fba561ba46d26cc/docs/paper.pdf) provides background on appearance flow. The metrics in this repository's README describe its own recorded VITON experiment.
