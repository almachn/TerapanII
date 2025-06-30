# 🐶 Dog Breed Classifier with CNN + Transfer Learning

This is an image classification project using Convolutional Neural Networks (CNN) and **MobileNetV2** as a pre-trained model to classify dog breeds. The model achieves high accuracy and supports deployment across multiple platforms: **SavedModel**, **TensorFlow Lite**, and **TensorFlow.js**.

---

## 📂 Project Structure
.
├── notebook.ipynb # Training & evaluation notebook
├── saved_model/ # Exported SavedModel format
├── model.tflite # TFLite version of the model
├── tfjs_model/ # TFJS model (model.json + bin files)
├── label.txt # Label mapping for predictions
├── requirements.txt # Python dependencies
└── README.md # This file


---

## 🚀 Features

- ✅ **CNN + Transfer Learning** using MobileNetV2
- ✅ Achieves >85% accuracy on validation & test sets
- ✅ Converted into:
  - `.keras` for native Keras format
  - `.tflite` for mobile deployment
  - `.tfjs` for web deployment
- ✅ Inference-ready with class label mapping

---

## 🛠️ How to Run

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Run notebook
Use Jupyter or Colab to open notebook.ipynb and run training, evaluation, and export.

## 🐕 Inference Examples

### Keras Model

```bash
model = tf.keras.models.load_model("my_model.keras")
pred = model.predict(img_array)
```

### TFLite Inference
```bash
interpreter = tf.lite.Interpreter(model_path="model.tflite")
interpreter.allocate_tensors()
```

### TFJS Inference
```bash
const model = await tf.loadLayersModel("tfjs_model/model.json");
```






