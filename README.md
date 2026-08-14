# ✈️ Airplane Object Detection Using Faster R-CNN

## 📌 Overview

This project implements **object detection using Faster R-CNN (Region-based Convolutional Neural Network)** to detect airplanes in aerial images.

The model uses annotated airplane images with bounding-box coordinates and learns to identify and localize airplanes in previously unseen images.

The experiment was implemented using **Python, PyTorch, Torchvision, and Google Colab with an NVIDIA T4 GPU**.

---

## 🎯 Objectives

* Understand object detection using R-CNN-based methods.
* Process images and bounding-box annotations.
* Train a Faster R-CNN object detection model.
* Detect airplanes in unseen images.
* Visualize predicted bounding boxes.
* Evaluate object localization using Intersection over Union (IoU).

---

## 📂 Dataset

The dataset contains airplane images and corresponding annotation files.

### Dataset Structure

```text
Airplane-Object-Detection/
│
├── Images/
│   ├── 42845.jpg
│   ├── 42847.jpg
│   ├── airplane_001.jpg
│   └── ...
│
├── Airplanes_Annotations/
│   ├── 42845.csv
│   ├── 42847.csv
│   ├── airplane_001.csv
│   └── ...
│
├── faster_rcnn_airplane.pth
├── airplane_detection.ipynb
└── README.md
```

### Dataset Details

* Total images: **733**
* Valid annotated images: **729**
* Empty/invalid annotations: **4**
* Image size: **256 × 256 pixels**
* Annotation format: Bounding-box coordinates
* Dataset split: **80% training / 20% testing**

### Annotation Format

Each annotation file contains:

```text
Number of airplanes
x_min y_min x_max y_max
x_min y_min x_max y_max
...
```

Example:

```text
4
15 69 40 96
10 173 42 203
74 212 100 243
233 197 256 226
```

---

## 🧠 Model

The experiment uses:

**Faster R-CNN with ResNet-50 FPN**

### Classes

```text
0 → Background
1 → Airplane
```

The pretrained Faster R-CNN model was adapted for the airplane detection task by replacing its original classification head with a classifier containing two classes.

---

## 🛠️ Technologies Used

* Python
* PyTorch
* Torchvision
* NumPy
* Pandas
* Matplotlib
* Scikit-learn
* Google Colab
* NVIDIA T4 GPU

---

## ⚙️ Methodology

The overall workflow is:

```text
Airplane Images + Annotations
            ↓
     Data Preprocessing
            ↓
   Bounding Box Extraction
            ↓
      Dataset Validation
            ↓
     Train/Test Split
            ↓
     Faster R-CNN Model
            ↓
        Model Training
            ↓
       Model Prediction
            ↓
     Bounding Box Detection
            ↓
       IoU Evaluation
```

---

## 🚀 Implementation

### 1. Load the Dataset

The images and annotation files are loaded and paired based on their filenames.

### 2. Process Annotations

The bounding-box coordinates are extracted from each annotation file in the format:

```text
x_min, y_min, x_max, y_max
```

### 3. Dataset Split

The valid dataset was divided into:

* **80% Training**
* **20% Testing**

### 4. Model Training

Faster R-CNN was trained for **3 epochs** using SGD optimization.

Training configuration:

```text
Epochs: 3
Learning Rate: 0.005
Momentum: 0.9
Weight Decay: 0.0005
Optimizer: SGD
```

---

## 📊 Training Results

The training loss decreased consistently:

| Epoch |   Loss |
| ----: | -----: |
|     1 | 0.3673 |
|     2 | 0.2608 |
|     3 | 0.2034 |

The decrease in loss indicates that the model learned to localize and detect airplanes from the training data.

---

## 🔍 Detection Results

The trained Faster R-CNN model was tested on an unseen image.

### Result

```text
Ground-truth airplanes: 4
Predicted airplanes:    4
```

The model successfully detected all four airplanes in the selected test image.

---

## 📐 IoU Evaluation

Intersection over Union (IoU) was used to measure the overlap between predicted and ground-truth bounding boxes.

### IoU Results

```text
0.8320
0.8268
0.8003
0.8208
```

### Average IoU

```text
0.81997 ≈ 82%
```

The average IoU of approximately **82%** indicates good overlap between the predicted and actual bounding boxes for the selected test image.

> **Note:** The reported 82% IoU is for the selected test image and should not be interpreted as the overall dataset accuracy.

---

## 💾 Trained Model

The trained model weights were saved as:

```text
faster_rcnn_airplane.pth
```

The model can be reloaded using:

```python
model.load_state_dict(
    torch.load("faster_rcnn_airplane.pth")
)
```

---

## 📸 Sample Output

The output of the model consists of airplane images with predicted bounding boxes and confidence scores.

Example:

```text
        ┌─────────────┐
        │  Airplane   │
        │   Score     │
        └─────────────┘
```

The bounding boxes indicate the detected airplane locations.

---

## 📁 Project Files

```text
├── Images/
├── Airplanes_Annotations/
├── airplane_detection.ipynb
├── faster_rcnn_airplane.pth
└── README.md
```

---

## 🎓 Learning Outcomes

Through this project, the following concepts were learned:

* Object detection using R-CNN-based architectures.
* Bounding-box annotation processing.
* Faster R-CNN model configuration.
* Transfer learning using a pretrained detection model.
* GPU-based deep learning using PyTorch.
* Object localization and IoU evaluation.
* Saving and reusing trained model weights.

---

## ⚠️ Challenges Faced

### 1. Annotation Format

The annotation files were space-separated rather than comma-separated.

**Solution:** Whitespace-based parsing was used to extract the coordinates.

### 2. Empty Annotation Files

Four annotation files did not contain valid bounding boxes.

**Solution:** These files were excluded from the training dataset.

### 3. CPU Training

Initially, the model was running on CPU.

**Solution:** Google Colab was switched to an NVIDIA T4 GPU.

### 4. Runtime Disconnection

The Colab runtime disconnected during the experiment.

**Solution:** The model was retrained and its weights were saved using `torch.save()`.

---

## 🔮 Future Improvements

The model performance could be improved by:

* Increasing the number of training epochs.
* Using more training data.
* Applying data augmentation.
* Performing evaluation across the complete test dataset.
* Calculating mAP (mean Average Precision).
* Tuning learning rate and other hyperparameters.
* Comparing Faster R-CNN with YOLO-based object detection models.

---

## 👩‍💻 Conclusion

The experiment successfully demonstrated **airplane object detection using Faster R-CNN**. The model was trained on annotated airplane images and successfully detected all four airplanes in the selected test image. The average IoU of approximately **82%** demonstrates good bounding-box localization for the evaluated image.

---

## 📜 License

This project is intended for **educational and academic purposes**.
