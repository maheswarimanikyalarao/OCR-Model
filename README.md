# **Optimuz**

This repository contains the code for a **GENAI-based project** featuring a user interface with various accessibility options. The project integrates **PaddleOCR** for Optical Character Recognition (OCR) and the **GEMINI AI chatbot** for enhanced user interaction.

---

## **Table of Contents**
- [Overview](#overview)
- [PaddleOCR Features](#paddleocr-features)
- [Model Architecture](#model-architecture)
- [Implementation Workflow](#implementation-workflow)
- [Model Fine-tuning for Vertical and Long Text](#model-fine-tuning-for-vertical-and-long-text)
- [JSON Output Example](#json-output-example)

---

## <a id="overview"></a> **Overview**

**PaddleOCR** is an advanced toolkit for optical character recognition that allows users to extract text from images and documents. The toolkit includes multiple pre-trained models for:

- Text Detection
- Text Direction Classification
- Text Recognition

PaddleOCR supports multiple languages such as Latin, Arabic, Traditional Chinese, Korean, and Japanese, making it a versatile tool for global applications.

---

## <a id="paddleocr-features"></a> **PaddleOCR Features**

- 🖼️ **Text Detection**: Detects text areas in images and generates bounding boxes around them.
- 🔤 **Text Recognition**: Recognizes and extracts text content within the detected regions.
- 🔄 **Vertical Text Detection**: Detects rotated or vertically aligned text.
- 📏 **Handling Long Text**: Optimized to recognize longer blocks of text.
- ⬆️ **Angle Classification**: Automatically detects and corrects the text's orientation.
- 📸 **High-Resolution Text Detection**: Supports high-res input for detecting small and large text accurately.

---

## <a id="model-architecture"></a> **Model Architecture**

**PP-OCRv3**

- **Text Detection** is based on the **Differentiable Binarization (DB)** algorithm, trained with a distillation strategy for high accuracy.
- **Text Recognition** leverages the **Scene Text Recognition with a Single Visual Model (SVTR)**, as outlined by _Du et al. (2022)_.

---

## <a id="implementation-workflow"></a> **Implementation Workflow**

The **Optimuz** project utilizes the **PaddleOCR** model to process images and extract text content. Here's the step-by-step process:

1. **Image Input**: The image is fed into the OCR model.
2. **Text Detection**: Bounding boxes are generated around the detected text areas.
3. **Text Recognition**: Extracts the actual text from the regions inside the bounding boxes (if recognition is enabled).
4. **JSON Output**: The model generates a JSON file containing the detected text, bounding box coordinates, and confidence scores.

---

## <a id="model-fine-tuning-for-vertical-and-long-text"></a> **Model Fine-tuning for Vertical and Long Text**

While PaddleOCR excels at detecting horizontal text, several adjustments were made to enhance performance for vertical and lengthy text:

- **`use_angle_cls=True`**: Enables detection and correction of rotated or vertically aligned text.
- **`det_db_box_thresh=0.2`**: Lowers the detection threshold to increase sensitivity for text detection.
- **`det_db_unclip_ratio=2.5`**: Increases the unclip ratio to capture larger text areas.
- **`lang='en'`**: Specifies the language to be used (English in this case).
- **`rec=False`**: Disables the text recognition component (if only detection is required).
- **`det_limit_side_len=1536`**: Sets a maximum side length for detected text to handle high-resolution images.

---

## **Example Images**

We implemented the PaddleOCR model to extract text from images. The image below shows the text detection process:

![example image](https://github.com/user-attachments/assets/bedbca55-8d79-4186-9a25-9cbb8e3e253d)

Another example illustrates PaddleOCR's performance with vertical text and larger text areas:

![example image](https://github.com/user-attachments/assets/f603e2b9-7401-4836-9d8f-3e469f5d460b)

---

## <a id="json-output-example"></a> **JSON Output Example**

```json
[
    {
        "text": "Hello",
        "confidence": 0.98,
        "position": [[12, 34], [56, 34], [56, 78], [12, 78]]
    },
    {
        "text": "World!",
        "confidence": 0.95,
        "position": [[100, 150], [200, 150], [200, 180], [100, 180]]
    }
]

