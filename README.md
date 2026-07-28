# DLCodes

One-line summary
This is a personal collection of Deep Learning experiments and learning notebooks — image classification (including X-ray use-cases and streamlit demo), autoencoders, image augmentation, LSTM stock prediction, and a churn-prediction case study combining classical ML and ANN.

## Table of contents
- [What this is](#what-this-is)
- [Stack](#stack)
- [Repository layout](#repository-layout)
- [How to run / Quick start](#how-to-run--quick-start)
- [Notes on datasets and models](#notes-on-datasets-and-models)
- [Files of interest (high level)](#files-of-interest-high-level)
- [Development / Reproducibility tips](#development--reproducibility-tips)
- [Try asking](#try-asking)
- [License & Contact](#license--contact)

## What this is
A study portfolio of Deep Learning projects and reference notebooks demonstrating common DL workflows: building and training CNNs, using pretrained models, autoencoders for X-ray images, image augmentation techniques, an LSTM-based stock predictor, and a churn-prediction case study showing both classical ML and ANN approaches. Intended for personal reference, learning, and small demos.

### Stack
- Language(s): Python (notebooks and small scripts)
- Frameworks / runtimes: TensorFlow / Keras, scikit-learn, Streamlit (for a small demo)
- Notable libraries: tensorflow / keras, streamlit, numpy, pandas, matplotlib, opencv-python, scikit-image, scikit-learn

## Repository layout
Top-level entries (annotated)
```
Autoencoders_XRay_Images.ipynb        # Autoencoder notebook for chest X-ray reconstruction/anomaly detection
CML+ANN_Churn_Use_Case.ipynb         # Classical ML + ANN churn modelling case study (uses Churn_Modelling.csv)
CNN_Image_Classification.ipynb       # CNN training on Fashion / example image classifications
Image_Augmentation.ipynb             # Image augmentation examples (skimage / cv2)
Image-Classification-Streamlit/      # Small Streamlit app to demo an X-ray classifier
  ├─ ImageClassifier.py              # Streamlit app that loads provided .h5 model and predicts uploaded jpeg
  └─ custom_pre_trained_model_10.h5  # Saved Keras model used by Streamlit demo (~73 MB)
LSTM/                                # LSTM stock prediction example
  ├─ TATA__StockPrediction_LSTM.ipynb
  ├─ NSE-TATAGLOBAL.csv
  └─ tatatest.csv
Churn_Modelling.csv                  # Dataset used by churn notebook
Pre_Trained_Models.ipynb             # Example using VGG16 / pretrained models
X_ray_Image_Classification - with PreTrained Models.ipynb  # X-ray classification examples with transfer learning
```

How it fits together
- Most work is organized as self-contained Jupyter notebooks demonstrating a single experiment or concept. The Streamlit folder contains a small demo app that loads a saved Keras model and serves predictions for uploaded X‑ray jpeg images.

## How to run / Quick start

1) Run the Streamlit demo (if you want an interactive demo)
- From the repository root, create and activate a Python environment, then install dependencies and run the app:
```bash
python -m venv .venv
source .venv/bin/activate        # or .venv\Scripts\activate on Windows
python -m pip install --upgrade pip
python -m pip install streamlit tensorflow numpy pandas opencv-python
streamlit run Image-Classification-Streamlit/ImageClassifier.py
```
- The Streamlit app expects the model file `Image-Classification-Streamlit/custom_pre_trained_model_10.h5` to be present (it is included in the repo). Upload a JPEG X-ray image via the app UI and click PREDICT.

2) Open and run notebooks
- Use Jupyter Lab/Notebook or Google Colab. Example:
```bash
# from repo root
jupyter lab
# then open any .ipynb, e.g. CNN_Image_Classification.ipynb
```
- Many notebooks were originally run in Google Colab and refer to mounting Google Drive (e.g., dataset paths in Autoencoders_XRay_Images.ipynb). If you use Colab, adjust the dataset paths as needed.

3) Reproduce classical ML experiments (CML+ANN_Churn_Use_Case.ipynb)
- `Churn_Modelling.csv` is included. Open the notebook and run cells in order. Install the usual data-science dependencies:
```bash
python -m pip install pandas numpy scikit-learn matplotlib seaborn
```

## Notes on datasets and models
- The X-ray-related notebooks reference chest_xray datasets stored on Google Drive in the original runs. The repository does not contain the full chest X-ray dataset — you'll need to download or mount the dataset and update paths used in the notebooks (e.g., `/content/drive/MyDrive/chest_xray/...`).
- `Churn_Modelling.csv` is included at the repo root and is used by the churn notebook.
- `Image-Classification-Streamlit/custom_pre_trained_model_10.h5` is a saved Keras model included for the demo. It is a binary model file (~73 MB). Loading this requires compatible TensorFlow/Keras versions.
- Some notebooks save or load model artifacts and expect Colab / Drive paths — search for `drive.mount` and adjust paths locally.

## Files of interest (high level)
- Image-Classification-Streamlit/ImageClassifier.py — a tiny Streamlit app that:
  - loads `custom_pre_trained_model_10.h5`
  - resizes inputs to 100x100 and predicts between "NORMAL" and "PNEUMONIA"
  - run with `streamlit run ...`
- LSTM/TATA__StockPrediction_LSTM.ipynb — example LSTM applied to stock (TATA) time series using CSVs in LSTM/
- CML+ANN_Churn_Use_Case.ipynb — full pipeline showing preprocessing, classical ML (Decision Tree, Random Forest), and ANN experiments
- Autoencoders_XRay_Images.ipynb — builds a convolutional autoencoder for X-ray images; shows training, early stopping, and reconstruction visualizations
- Image_Augmentation.ipynb — small cookbook of augmentation operations (flip, rotate, noise, resize)

## Development / Reproducibility tips
- Use a virtual environment and pin package versions if you plan to reproduce training runs (TensorFlow changes may break saved models).
- If running the Streamlit app, ensure Keras/TensorFlow can load the .h5 file; if you run into version issues, try matching the TensorFlow version used when the model was saved (commonly TF 2.x).
- For heavy training (autoencoders, CNN training), use GPU-backed environments (Colab, local GPU) for reasonable runtimes.
- If you want the notebooks to be runnable in Colab as-is, mount Google Drive and set dataset paths the same way the notebooks expect (they include `drive.mount('/content/drive')`).


