# Brain Tumor Diagnostic System

This system is a diagnostic engine that is clinically graded and has been developed to analyze MRIs of the brain. Rather than simply classifying images by category, the diagnostic engine uses multi-modal symptom fusion to incorporate patient symptoms, detects structural anomalies, and tracks changes over time to provide clinicians with a reliable second opinion.

## Features of the Engine

- **Classification Engine** - The Classification Engine uses freshly developed DenseNet121 (with PyTorch) as its backbone to classify brain MRI scans into one of four categories (Glioma, Meningioma, Pituitary Tumour or No Tumour).
- **Morphology Validation (Anomaly Detection)** - Anomaly detection is performed by an Isolation Forest model to evaluate both image features and color variance before running the primary classifier and will automatically reject non-scan images (e.g., random images or badly formatted x-rays).
- **Multi-modal Fusion** - The MRI scan's visual features and corresponding patient symptom data (e.g., headaches, seizures, cognitive issues) are fused by using a cartesian heuristic to adjust for the baseline probabilities of each of the fused symptoms.
- **Explainability (Grad-CAM)** - Grad-CAM will be automatically generated to create heatmaps over the original scan showing where on the scan the artificial intelligence model evaluated to provide its classification.
- **CBIR (Content-based image retrieval** - Previous similar historical scans can be retrieved using the local vector database and cosine similarity to retrieve the most relevant scan.
- **Longitudinal Tracking** - Longitudinal tracking is used to evaluate the differences between the two scans taken at different times (e.g., T1 versus T2) and create a difference map of any changes in the size or mass of the tumour.

### Project Structure
- **round1_eda.py** - This is where you will perform your initial data exploration, confirm the distributions of your data, and extract baseline features.
- **round2_training.py** - The primary model training loop, it will load datasets, compute focal loss, and will save the .pth weights to the file system.
- **train_model.py** - This is where the architecture definition for the `BrainTumorDenseNet` resides.
- **core_engine.py** - This is where the `ClinicalAIEngine` class resides and addresses all inference logic, generates Grad-CAM images, fuses the symptom components, and creates longitudinal differential images.
- **app.py** - The Streamlit frontend - provides the user interface to upload an image/s scan of a brain and view a diagnostic report.

### Setup & Running Locally
1. Clone the repository and navigate to the directory location of the code.
2. Install all required dependencies (PyTorch, StreamLit, OpenCV, Scikit-Learn, PIL).
   ```bash
   pip install -r requirements.txt

File Drive Link
https://drive.google.com/drive/u/1/folders/11vKQZOsX0jAFh-xSfGeGSDbbgcQGQcUr
