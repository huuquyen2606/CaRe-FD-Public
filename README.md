# CaRe-FD Research Handover

Research materials accompanying **CaRe-FD: Class-Aware Reliability and Recipient-Deficiency-Aware Federated Distillation for Intrusion Detection**, submitted to **ICCIES 2027**.

**Authors:** Truong Duc Duong, Tran Tuan Kiet, Nguyen Huu Quyen, and Pham Van-Hau.

This handover contains the submitted manuscript, preprocessing and experiment notebooks, partitioned datasets, saved checkpoints, execution logs, and the analysis package used to reproduce the paper's figures and numerical tables. The experiments cover six methods under 10-client and 100-client configurations.

The paper reports results at **communication round 20**. Some archived sessions continued beyond round 20; their later results are retained for provenance and must not replace the paper's reported endpoint.

## 1\. Start Here

| Task | Location |
| :---- | :---- |
| Read the submitted paper | [CaRe-FD.pdf](http://Full-Source/Paper/Submitted/CARD-FD.pdf) |
| Open the accompanying LaTeX source | [Overleaf.zip](http://Full-Source/Paper/Submitted/Overleaf.zip) |
| Reproduce figures and numerical tables without training | [CARD\_FD\_analysis\_handover.zip](http://Full-Source/Analysis/CARD_FD_analysis_handover.zip) |
| Inspect historical result workbooks | [Statistic.zip](http://Full-Source/Analysis/Statistic.zip) |
| Access partitioned data and preprocessing notebooks | [Data](http://Full-Source/Data/) |
| Access training notebooks, checkpoints, and logs | [Experiment](http://Full-Source/Experiment/) |

The current files occupy approximately **27.9 GB (26.0 GiB)** before extraction. Plan for additional disk space when extracting dataset and checkpoint archives. You can extract only the method and configuration needed for your task.

## 2\. Directory Structure

```
CaRe-FD-Handover/
├── README.md
└── Full-Source/
    ├── Analysis/
    │   ├── CARD_FD_analysis_handover.zip
    │   └── Statistic.zip
    ├── Data/
    │   ├── 10C/
    │   │   ├── data-preprocessing_10C.ipynb
    │   │   ├── data-preprocessing_10C_logs.log
    │   │   ├── Raw_10C.zip
    │   │   └── Review_data_10C.zip
    │   └── 100C/
    │       ├── data_preprocessing_100C.ipynb
    │       ├── data_preprocessing_100C_logs.log
    │       └── Raw_100C.zip
    ├── Experiment/
    │   ├── CaRe-FD/
    │   ├── FedAvg/
    │   ├── FedALA/
    │   ├── FedNH/
    │   ├── FedPLVM/
    │   └── MP-FedCL/
    │       └── [each method has 10C/ and 100C/ subdirectories]
    └── Paper/
        └── Submitted/
            ├── CaRe-FD.pdf
            └── Overleaf.zip
```

Directory names and capitalization above match this handover. Preserve them when moving files to a case-sensitive system.

## 3\. Experiment Inventory

Every method has a notebook, checkpoint archive(s), and execution log(s) for both configurations.

| Method | 10-client notebook | 100-client notebook |
| :---- | :---- | :---- |
| CaRe-FD | [CaRe-FD\_10C.ipynb](http://Full-Source/Experiment/CARD-FD/10C/CARD-FD_10C.ipynb) | [CaRe-FD\_100C.ipynb](http://Full-Source/Experiment/CARD-FD/100C/CARD-FD_100C.ipynb) |
| FedAvg | [FedAvg\_10C.ipynb](http://Full-Source/Experiment/FedAvg/10C/FedAvg_10C.ipynb) | [FedAvg\_100C.ipynb](http://Full-Source/Experiment/FedAvg/100C/FedAvg_100C.ipynb) |
| FedALA | [FedALA\_10C.ipynb](http://Full-Source/Experiment/FedALA/10C/FedALA_10C.ipynb) | [FedALA\_100C.ipynb](http://Full-Source/Experiment/FedALA/100C/FedALA_100C.ipynb) |
| FedNH | [FedNH\_10C.ipynb](http://Full-Source/Experiment/FedNH/10C/FedNH_10C.ipynb) | [FedNH\_100C.ipynb](http://Full-Source/Experiment/FedNH/100C/FedNH_100C.ipynb) |
| FedPLVM | [FedPLVM\_10C.ipynb](http://Full-Source/Experiment/FedPLVM/10C/FedPLVM_10C.ipynb) | [FedPLVM\_100C.ipynb](http://Full-Source/Experiment/FedPLVM/100C/FedPLVM_100C.ipynb) |
| MP-FedCL | [MP-FedCL\_10C.ipynb](http://Full-Source/Experiment/MP-FedCL/10C/MP-FedCL_10C.ipynb) | [MP-FedCL\_100C.ipynb](http://Full-Source/Experiment/MP-FedCL/100C/MP-FedCL_100C.ipynb) |

**FedAvg uses the PyTorch implementation associated with the updated paper results.** Historical workbooks may contain earlier FedAvg results; use the verified PyTorch records in the analysis package when reproducing the submitted tables and curves.

`CARe-FD`, `carefd`, and `CaRe-FD` appear in historical filenames and run directories. The paper's displayed method name is **CaRe-FD**. Preserve internal run names because notebooks and resume paths may depend on them.

### CaRe-FD 100-client checkpoints

The 100-client run is stored in five independent session archives:

| Archive | Checkpoint rounds found in the archive |
| :---- | :---- |
| `CaRe-FD_100C_checkpoint_R1.zip` | 1 |
| `CaRe-FD_100C_checkpoint_R2_R6.zip` | 2-6 |
| `CaRe-FD_100C_checkpoint_R7-R11.zip` | 7-11 |
| `CaRe-FD_100C_checkpoint_R12_R16.zip` | 12-16 |
| `CaRe-FD_100C_checkpoint_R17_R20.zip` | 17-20 |

These are separate ZIP archives, not multipart pieces of one ZIP. Each contains a run directory with the same name and session-specific metadata. **Extract each archive into its own destination directory** to preserve its logs, summaries, manifests, and checkpoints. Do not blindly merge the archives and overwrite identically named files.

Other checkpoint archives can also contain metrics, configuration files, preprocessing metadata, or caches in addition to model states. Check their contents before selecting an evaluation or resume file.

## 4\. Data and Preprocessing

The experiments use CICIoT2023 with 34 classes and the feature configuration recorded in the notebooks and manifests.

Despite their filenames, **`Raw_10C.zip` and `Raw_100C.zip` contain exported client partitions and test data**, rather than an untouched copy of the upstream dataset:

- `Raw_10C.zip` contains `part_1.csv` through `part_10.csv` and `test_total.csv` at its archive root.  
- `Raw_100C.zip` contains the partition export under `cic_iot_noniid_100/run_20260907T180249Z_immfyucm/`, including client files, `test_total.csv`, distribution statistics, and a manifest.  
- `Review_data_10C.zip` contains `dataset_statistics_pivot.csv` and distribution images.  
- The preprocessing notebooks and accompanying logs document how the partitions were produced. They retain the original Kaggle input paths; update these paths for another environment.

The two configurations use randomized, heterogeneous partitioning procedures; they are **not Dirichlet partitions**. Do not describe them using an invented Dirichlet concentration parameter. Consult the corresponding preprocessing notebook for the exact selection, allocation, and split logic; the 10-client and 100-client procedures are not identical.

For reproduction of the reported runs, prefer the saved partitions and the associated preprocessing metadata. Recreating a partition from the upstream data is a separate operation and must be checked against the archived counts and manifests.

CaRe-FD reserves 340 calibration samples and 680 reference samples, with 10 and 20 samples per class, respectively. The distribution figure uses the original training counts **before** removing these shared pools. Keep the class order, feature order, and any saved preprocessing state consistent with the chosen checkpoint.

## 5\. Reproduce Figures and Tables Without Training

The lightweight analysis archive contains all inputs required for its saved-result calculations. No GPU or multi-gigabyte dataset extraction is needed for this workflow.

1. Extract `Full-Source/Analysis/CARD_FD_analysis_handover.zip` into a separate directory, for example `Full-Source/Analysis/Reproduction/`.

2. The extracted archive has its own `Full-Source/` wrapper. Open:

```
Full-Source/Analysis/Reproduction/Full-Source/analysis/
```

3. Read its `README.md`. Pre-generated results are already available in `outputs/`.

4. To regenerate the results, run the following commands from that extracted `analysis` directory on Windows:

   ```powershell

   python -m venv .venv

   .\.venv\Scripts\python.exe -m pip install -r requirements.txt

   .\.venv\Scripts\python.exe scripts/reproduce.py

   .\.venv\Scripts\python.exe scripts/verify_submission.py

   ```

   On Linux/macOS, use `python3 -m venv .venv` and `.venv/bin/python` for the remaining commands.

The verification script expects the PDF stored in the extracted archive's sibling `paper/submitted/` directory. Keep that wrapper and PDF in place. That archived PDF is byte-identical to `Full-Source/Paper/Submitted/CaRe-FD.pdf` in this handover at the time this README was prepared.

| Paper item | Reproduction source | Main outputs inside the extracted `analysis/outputs/` |
| :---- | :---- | :---- |
| Figure 1: workflow | Editable `inputs/CARD_FD_Workflow.drawio` | `card_fd_workflow.png` |
| Figure 2: client training distributions | `scripts/plot_data_distribution.py` and original class-count CSV files | `data_distribution.pdf`, `data_distribution.png` |
| Figure 3: round-wise performance | `scripts/render_comparison.py` and per-round measurements | `learning_curves.pdf`, `learning_curves.png` |
| Table 1: round-20 performance | `scripts/reproduce.py` and saved metric evidence | `table1_performance_percent.csv`, `table1_performance.tex` |
| Table 2: communication cost | `scripts/reproduce.py`, model shapes, and prototype-count evidence | `table2_communication_display.csv`, `table2_communication.tex`, `communication_R20_by_setting.csv` |

Figure 1 is a manually editable workflow diagram, not a plot generated from experimental measurements. Open its `.drawio` source in diagrams.net to edit it.

The analysis package includes provenance records, checksums, and validation reports. Its checks matched 84 numerical cells in Table 1 and 13 displayed values in Table 2 to the supplied PDF. These are saved-evidence and arithmetic checks, not a rerun of model training or test-set inference.

`Statistic.zip` preserves historical and intermediate workbooks. Its `Save/` folder and files marked `Old` should not be treated as the authoritative submitted results. Use the analysis package's verified input records and output tables for the current paper.

## 6\. Run or Resume an Experiment

The archived notebooks reflect Kaggle sessions and may already be configured to resume an existing run. There is no single shared training entry point for all methods.

1. Select a method and `10C` or `100C` configuration under `Full-Source/Experiment/`.  
2. Extract the corresponding data archive into a known location.  
3. Open the matching notebook and inspect its configuration and dependency cells before execution.  
4. Update data paths such as `DATA_DIR` or `DATA_ROOT` to the extracted directory containing the expected client and test files.  
5. Decide whether to start from scratch, evaluate a saved state, or resume training. Review variables such as `RESUME_CHECKPOINT`, `RESUME_FROM`, and `CHECKPOINT_INPUT_DIR`, where present. Follow that notebook's documented fresh-run or resume settings rather than assuming a shared switch across methods.  
6. For a resumed run, select the checkpoint from the same method, client configuration, and session lineage. Restore additional state as required by that notebook; a global model weight file alone may not contain everything needed for an exact continuation.  
7. Configure a writable output directory separate from the archived evidence, then execute the intended cells in order.  
8. Compare round-20 outputs with the analysis package. Retain new-run outputs separately from the submitted-run artifacts.

Use the package versions, hardware information, seed settings, and configuration recorded by the selected experiment when available. A common software/hardware environment across all archived baseline sessions has not been established. The analysis package's `requirements.txt` and `environment_analysis.txt` describe figure/table reproduction, **not** the training environments.

## 7\. Interpretation of Results and Communication Cost

- Results are reported at the fixed round-20 endpoint, not the best observed test round.  
- CaRe-FD metrics summarize post-distillation client models using an unweighted client mean. Baseline rows evaluate the corresponding global model or global body/prototype combination. These are different evaluation objects.  
- The evidence comprises the supplied runs; do not interpret it as repeated-seed means or confidence intervals.  
- Communication cost is a **logical tensor-value payload per client at round 20**, expressed in decimal kB (`1 kB = 1,000 bytes`). It is not measured network traffic, checkpoint file size, or an average over training rounds.  
- Table 2 averages the per-client means of the 10-client and 100-client settings, except MP-FedCL download, which is shown separately for the two settings. It does not pool all 110 clients into one weighted mean.  
- FedPLVM prototype counts vary across rounds; its round-20 counts must not be applied to every round.  
- MP-FedCL download reflects the padded global prototype pool in the archived implementation and depends on the client count.  
- Serialization, transport headers, and other excluded metadata are documented in the analysis README. Preserve these qualifications when using the cost values elsewhere.

## 8\. Manuscript Files

`Full-Source/Paper/Submitted/CaRe-FD.pdf` is the archived submitted PDF supplied for this handover. `Overleaf.zip` contains the accompanying LaTeX project and figure assets, with `main.tex` at the archive root.

Preserve the submitted PDF as the record of the submission. If rebuilding or revising the LaTeX source, save the new PDF separately and compare it before labeling it as the submitted version. The presence of the source archive alone does not establish that a fresh compilation is byte-identical to the archived PDF.

## 9\. Drive Storage and Public Repository

This directory is the full research handover intended for the team's designated Google Drive **Full Source** folder. The actual Drive sharing URL should be taken from the mentor's message when preparing the public repository.

The designated public repository is [CaRe-FD-Public](https://github.com/huuquyen2606/CARD-FD-Public).

Prepare the public code release as a separate copy. Keep runnable code, configuration instructions, lightweight analysis resources, and links explaining how to obtain and place the full data/checkpoints. Keep large datasets and checkpoint archives in the designated storage location. This directory does not itself assert that a Drive upload or GitHub release has been completed.

## 10\. Verification Scope

To prepare this README, the folder structure, notebook source/configuration text, and ZIP directory listings were inspected. The CaRe-FD 100-client checkpoint round coverage above was checked from archive member names. The submitted PDF was also compared by SHA-256 with the PDF bundled in the analysis archive.

This inventory is not a full integrity test of every multi-gigabyte archive, a successful load of every checkpoint, or an end-to-end training reproduction. After transferring the handover, verify upload completion and file integrity before removing local copies. Preserve session-specific metadata when extracting or reorganizing archives.
