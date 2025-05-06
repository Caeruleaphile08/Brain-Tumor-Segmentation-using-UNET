# Brain Tumor Segmentation using Deep Learning

## 🧠 Project Overview

This project aims to segment brain tumors from MRI scans using a deep learning model. The segmentation identifies various tumor regions from multimodal 3D MRI scans and classifies them accurately.

---

## 📁 Dataset

**Source**: [BraTS 2020 Dataset on Kaggle](https://www.kaggle.com/datasets/awsaf49/brats2020-training-data)

- Format: `.nii` (3D NIfTI format)
- 4 Modalities:
  - **T1**: Brain anatomy (grey vs. white matter)
  - **T1CE**: Blood-brain barrier damage (tumors/inflammation)
  - **T2**: Highlights cerebrospinal fluid
  - **FLAIR**: Highlights abnormalities by removing CSF

⚠️ **Note**: We use only T1CE, T2, and FLAIR modalities for training (T1 is skipped).

---

## 🧾 Annotations

- `Label 0`: Background
- `Label 1`: Necrotic & Non-enhancing tumor
- `Label 2`: Peritumoral edema
- `Label 4`: GD-enhancing tumor
- `Label 3`: Reassigned to Label 4

---

## ⚙️ Data Preprocessing

1. **Normalization**: Convert 3D to 2D, normalize using `MinMaxScaler`, reshape to 3D.
2. **Modality Selection**: Only T1CE, T2, FLAIR used.
3. **Cropping**: Remove black background regions.
4. **Filtering**: Retain only slices with >1% valid image data.
5. Final valid data points: **344** out of 369.

---

## 🔄 Custom Data Generator

- Created to handle `.npy` format
- Generates batches in the format:  
  `(image, corresponding_mask)`  
  Shape: `(1, H, W, Channels)` per batch

---

## 🖼️ Visualization

Sample visualization includes:
- FLAIR, T1CE, T2 slices for a patient (e.g., #45, slice #78)
- Corresponding segmentation mask (with tumor regions in color)

---

## 🧠 Model Architecture

- **Model**: U-Net
- **Layers**:
  - `Conv3D`, `MaxPooling3D`
  - Activation: `ReLU`
  - Weight Init: `he_uniform`
  - Skip connections between encoder and decoder

---

## 📉 Training Details

- **Loss Functions**:
  - **Dice Loss**: Measures overlap between prediction and ground truth
  - **Categorical Focal Loss**: Focuses on hard-to-classify regions
- **Optimizer**: Adam
- **Metrics**:
  - **Accuracy**: 98.50%
  - **IOU Score**: 0.6946
  - **Dice Loss**: 0.8059
  - **Mean IOU**: 0.5183

---

## 💾 Model Saving

- `.h5`: Includes model + architecture
- `.tf`: TensorFlow format for deployment

---

## 📌 Summary

This project presents an end-to-end pipeline for medical image segmentation with preprocessing, visualization, custom data generation, U-Net-based training, and evaluation metrics optimized for detecting brain tumor regions.

---

## 📎 References

- [BraTS 2020 Challenge](https://www.med.upenn.edu/cbica/brats2020/)
- [Kaggle Dataset](https://www.kaggle.com/datasets/awsaf49/brats2020-training-data)
