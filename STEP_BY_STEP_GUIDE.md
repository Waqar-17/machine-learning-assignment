# Machine Learning Assignment - Deployment Guide

## What the files say and what you asked for

Your request is to understand the assignment, use your friend's ZIP as guidance, prepare the work, and get all completion steps. The assignment PDF itself requires two Jupyter notebooks, deployment of both models, the code/data/model files uploaded to Google Classroom, and a live deployment link at the top of each notebook. The ZIP is a worked example, not the official statement. I used its combined Streamlit app structure and data, then corrected the Titanic duplicate handling and the Heart Disease positive-class metrics.

The PDF says the submission deadline was **October 11, 2026 at 23:59**, with a three-day cutoff. As of **October 23, 2026**, that cutoff has passed. Contact the instructor now to ask whether they will accept a late submission or extension.

## 1. Extract the project

1. Download `Machine_Learning_Assignment.zip` from the output link beside this guide.
2. Extract it to a short path such as `C:\Machine_Learning_Assignment`.
3. Check that the folder contains `app.py`, `model_utils.py`, `requirements.txt`, `notebooks/`, `data/`, `titanic_model.pkl`, and `heart_disease_model.pkl`.

## 2. Set up Python and Jupyter on Windows

Use Python 3.12 to match the environment used for the model files. Open PowerShell in the project folder and run:

```powershell
py -3.12 -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m notebook
```

If PowerShell blocks activation, use Command Prompt and run:

```bat
.venv\Scripts\activate.bat
```

In Jupyter, choose the project `.venv` kernel if prompted.

## 3. Run the Titanic notebook

Open `notebooks/Titanic_Passenger_Survival.ipynb`. Choose **Kernel -> Restart Kernel and Run All Cells**. Read the markdown instructions as you run each part:

1. **Understand the data:** inspect the shape, columns, types, missing values, duplicate rows, and target balance in the instructor's 100-row sample.
2. **Preprocess and encode:** use the four predictors `PClass`, `Gender`, `Sibling`, and `Embarked`; drop incomplete and exact duplicate rows; encode the categories and `Survived` with `LabelEncoder`.
3. **Train and evaluate:** make a fixed stratified 80/20 split, train an SVC, and read accuracy, precision, recall, F1, the classification report, and confusion matrix. Metrics label `Yes` as the positive survival class.
4. **Apply and save:** try the example passenger and save the trained model bundle, with its encoders and feature order, as `titanic_model.pkl`.

The supplied Titanic CSV has 100 rows but only 45 distinct complete records. The notebook removes duplicates before splitting so identical rows do not land in both train and test sets. The resulting test set is tiny, so its scores are only a workflow demonstration.

## 4. Run the Heart Disease notebook

Open `notebooks/Heart_Disease_Prediction.ipynb` and run every cell from a fresh kernel:

1. **Understand the data:** inspect the UCI Cleveland data, its 14 columns, missing values, and raw `num` values.
2. **Use the required four inputs:** `age`, `sex`, `cp`, and `thalach`. The model input matrix has four columns; `num` is only the target.
3. **Prepare the target:** map `num=0` to **No disease**, and `num=1, 2, 3, 4` to **Disease present**. Encode `sex`, `cp`, and the target; keep `age` and `thalach` numeric.
4. **Train and evaluate:** use a fixed stratified 80/20 split and an SVC. Precision, recall, and F1 explicitly treat **Disease present** as the positive class. Review the confusion matrix.
5. **Apply and save:** inspect the example output. The notebook saves `heart_disease_model.pkl` with the encoders and exact feature order.

Missing values in unused fields such as `ca` and `thal` do not remove rows because those fields are not model inputs. All 303 rows have values for the four selected inputs and target.

The assignment PDF does not name the four ML-cycle phase labels. The notebooks organize the work into data collection/understanding, preprocessing/feature encoding, training/testing, and application/deployment. If your instructor used specific phase names in class, use those names when discussing the same work.

## 5. Start the app locally

From the project root, with `.venv` activated, run:

```powershell
python -m streamlit run app.py
```

The browser opens the combined app. Submit one example on the **Titanic Survival** tab and one on the **Heart Disease** tab. Stop the server with `Ctrl+C` in PowerShell.

## 6. Deploy to Streamlit Community Cloud

The friend's ZIP uses Streamlit, and this project keeps that route. The assignment asks for cloud deployment and itself points to a live Streamlit demo, so the combined app covers both model tasks with one public URL.

1. Create a GitHub repository in your own account.
2. Push the contents of the project folder to the repository root. Include `app.py`, `model_utils.py`, `requirements.txt`, `data/`, and both `.pkl` files.
3. Sign in to [Streamlit Community Cloud](https://share.streamlit.io/) with GitHub.
4. Choose **Create app**, select your repository and branch, and set the app file to `app.py`.
5. Open **Advanced settings**, select Python 3.12, then deploy.
6. Wait for the build to finish. Open the public URL and confirm both tabs make predictions. If the build fails, open the app logs and verify that the repository contains the dependency file, data folder, model files, and source code.
7. Copy the verified URL, such as `https://your-app-name.streamlit.app/`.

Streamlit deploys from a GitHub repository and reads Python dependencies from `requirements.txt`. See its [deployment instructions](https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/deploy) and [dependency instructions](https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/app-dependencies).

## 7. Finish the notebooks and upload

1. In the first markdown cell of **both** notebooks, replace the pending deployment-link text with your working public URL. The link must be the first line.
2. Save both notebooks with their executed outputs.
3. Include these items in the final submission:

   - `notebooks/Titanic_Passenger_Survival.ipynb`
   - `notebooks/Heart_Disease_Prediction.ipynb`
   - `data/sample-data.csv`
   - `data/heart_disease.csv`
   - `titanic_model.pkl`
   - `heart_disease_model.pkl`
   - `app.py`, `model_utils.py`, and `requirements.txt`
   - `data/DATA_SOURCES.txt` and `README.md`

4. Zip the updated project folder and upload it to Google Classroom. Keep your live URL at the top of both notebooks as the assignment requires.

## 8. Be ready to explain these choices

- **Why encode categories?** SVC needs numeric inputs. The saved feature encoders keep the app's input mapping consistent with training.
- **Why split the data?** A holdout set gives a basic check using records not used to fit the evaluation model.
- **Why use several metrics?** Accuracy can hide class-specific mistakes; precision, recall, F1, and the confusion matrix show different error patterns.
- **Why is `num` not a fifth input?** It is the answer the model is learning to predict, so including it among inputs would leak the target.
- **What are the limits?** The Titanic example is tiny and repetitive. The heart data are historical and the model uses only four features. Neither result should be treated as general or clinical performance.

The PDF states a strict plagiarism policy. Review the notebook code and outputs, run the cells yourself, add any student details your instructor asks for, and submit work you can explain. Dataset sources are listed in `data/DATA_SOURCES.txt`.
