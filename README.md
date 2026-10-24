# Rice Leaf Disease Classification | FPTU Can Tho Olympic AI 2026

Image classification of **eight rice-leaf classes**, created for the private FPTU Can Tho Olympic AI 2026 Warmup Kaggle competition.

## Overview and my work

- Processed **2,026 labeled training images** using CLAHE illumination normalization.
- Extracted **200-dimensional features** based on HSV histograms, color statistics, and HOG.
- Split labeled images into train and validation (**304 validation images, stratified**) **before augmentation**.
- Applied lightweight augmentation to training images, standardized features with `StandardScaler` fit on training data only, and compared **6 classifiers** (Decision Tree, KNN, SVM, Random Forest, Gradient Boosting, AdaBoost) with validation Macro F1.
- Selected **Random Forest**, then retrained on all labeled images to generate the submitted prediction file for **300 unlabeled competition test images**.

## Results and evidence

| Evaluation | Metric | Result | Evidence |
|---|---|---:|---|
| Internal validation (304 images) | Accuracy | **95.39%** (290/304) | Notebook classification report / confusion matrix |
| Internal validation (304 images) | Macro F1 | **0.9469** | Notebook classifier comparison |
| Kaggle hidden test | **Private Macro F1-Score** | **0.77641** | **0.77641** | Screenshot taken from the private Kaggle notebook page |

![Validation confusion matrix](results/confusion_matrix.png)

![Kaggle displayed Private Score](results/kaggle_private_score.png)

**Important limitations:** The Kaggle competition and original notebook are private, so viewers cannot verify the hidden-test score on a public leaderboard. The screenshot documents the score shown to the notebook owner, not an independently verifiable public result. The validation metrics and Kaggle Private Score measure different evaluation sets and should not be conflated. The exact metric underlying Private Score has not been verified.

## Data access and reproducibility

The **2 GB competition dataset is not included**. It comes from a private Kaggle competition and may require organizer permission to access or redistribute. Reproduction of the exact reported metrics needs authorized access to the original dataset. This repository supplies saved code and outputs for review, not a claim of fully public reproducibility.

This notebook expects Kaggle data beneath `/kaggle/input/` with a `label_mapping.json`, `train/` directory, and the test directory defined by the notebook's `TEST_FOLDER`. To run elsewhere, supply an authorized copy of the data and adjust `find_dataset_root()` and data paths.

## Repository files

- `Rice_Leaf_Classification.ipynb` — original notebook with saved outputs
- `results/confusion_matrix.png` — internal validation predictions
- `results/submission.csv` — 300 predictions (no ground-truth test labels)
- `results/kaggle_private_score.png` — screenshot evidence
- `requirements.txt` — approximate runtime dependencies, not pinned environment

## Reproduction steps (authorized dataset required)

1. Install dependencies with `pip install -r requirements.txt`.
2. Make the authorized dataset available with the structure expected by the notebook.
3. Open and run `Rice_Leaf_Classification.ipynb` (the notebook uses Kaggle-style `/kaggle/input` and `/kaggle/working` paths).
4. Compare output Macro F1 and the confusion matrix to those saved here.

## Sharing note

**Before publishing**, confirm the competition rules permit disclosure of the solution code, predictions, and screenshot. No raw competition images are included in this archive.
