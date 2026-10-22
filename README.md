# Machine Learning Assignment

AIC354 Assignment 2 - End-to-End Machine Learning

This project contains the two Jupyter notebooks, source datasets, trained model bundles, and a combined Streamlit app for the assignment's Titanic and Heart Disease tasks.

## Project files

- `notebooks/Titanic_Passenger_Survival.ipynb` - run and understand the instructor Titanic teaching workflow.
- `notebooks/Heart_Disease_Prediction.ipynb` - adapt that workflow with exactly four inputs: `age`, `sex`, `cp`, and `thalach`.
- `data/sample-data.csv` and `data/heart_disease.csv` - the supplied Titanic sample and UCI Cleveland dataset.
- `titanic_model.pkl` and `heart_disease_model.pkl` - trained models and their feature/target encoders.
- `app.py` and `model_utils.py` - combined local/cloud prediction app and model loading helpers.
- `requirements.txt` - Python dependencies.
- `data/DATA_SOURCES.txt` - dataset source and attribution.

## Run on Windows

Use Python 3.12 to match the environment used to create the serialized model files. From this project folder in PowerShell:

```powershell
py -3.12 -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m notebook
```

In Jupyter, open each notebook and choose **Kernel -> Restart Kernel and Run All Cells**. Then launch the combined app from this folder:

```powershell
python -m streamlit run app.py
```

## Deploy

Live deployment: [https://sp24-bse-091-machine.streamlit.app/](https://sp24-bse-091-machine.streamlit.app/). I verified that both prediction tabs return model outputs and that the app source points to this repository's `app.py`.

To redeploy, select this repository and set `app.py` as the entrypoint. Keep `requirements.txt`, `data/`, both `.pkl` files, and the Python source files in the repository. Select Python 3.12 in Advanced settings. If you deploy under a new URL, replace the deployment link at the top of both notebooks.

See `STEP_BY_STEP_GUIDE.md` for the full workflow and Google Classroom checklist.

## Data and limitations

The heart target maps UCI `num=0` to **No disease** and `num=1,2,3,4` to **Disease present**. Evaluation metrics explicitly count Disease present as the positive class. The Titanic teaching sample has 100 rows with 55 repeated rows; the notebook removes exact duplicates before its small holdout split. Both are classroom examples. The heart model is not for diagnosis or medical decisions.

The assignment statement includes a plagiarism policy. Run the notebooks, review their explanations, add any student details your instructor requires, and submit work you can explain.
