# Software Developer Salary Prediction Web App

This project is a web application that predicts software developer salaries based on data from the Stack Overflow Developer Survey 2020. It also provides an interactive data exploration page to visualize salary trends across different countries and experience levels.

## Features

-   **Explore Page**: An interactive dashboard with visualizations on:
    -   The number of survey data points from different countries.
    -   Mean salary based on the developer's country.
    -   Mean salary based on years of professional coding experience.
-   **Predict Page**: A user-friendly form to predict a software developer's salary. Users can input their:
    -   Country
    -   Education Level
    -   Years of Experience

## Live Demo

[Live App on Streamlit Community Cloud](https://employeesalaryapp-hixbmbku7dnxkpdnhadgmh.streamlit.app/)

## Screenshots

**Explore Page**
![Pie Chart](screenshots\explore_page_1.png)
![Bar Chart and Line Chart](screenshots\explore_page_2.png)

**Predict Page**
![Before Prediction](screenshots\predict_page_1.png)
![After Prediction](screenshots\predict_page_2.png)

## Methodology

The project follows a standard data science workflow, detailed in the `salary_predictions.ipynb` notebook:

1.  **Data Loading and Cleaning**: The raw data from `survey_results_public.csv` is loaded. Only relevant columns (`Country`, `EdLevel`, `YearsCodePro`, `Employment`, `ConvertedComp`) are selected. Rows with missing salary data are dropped, and the dataset is filtered to include only "Employed full-time" developers.

2.  **Data Preprocessing and Feature Engineering**:
    *   Categorical features like `Country` and `EdLevel` are cleaned and consolidated. For instance, countries with fewer than 400 data points are grouped into an "Other" category, and various education degrees are mapped to broader categories like "Bachelor's degree" or "Master's degree".
    *   The `YearsCodePro` column is cleaned to handle non-numeric values (e.g., "Less than 1 year") and converted to a numerical format.
    *   Outliers in salary (above $250,000 or below $10,000) are removed to improve model performance.

3.  **Model Training and Tuning**:
    *   Several regression models were tested, with the `DecisionTreeRegressor` showing promising results.
    *   `GridSearchCV` was used to find the optimal `max_depth` for the decision tree, which helped prevent overfitting and improved accuracy.

4.  **Model Persistence**:
    *   The final trained `DecisionTreeRegressor` model, along with the `LabelEncoder` objects for `Country` and `EdLevel`, is saved into a single `saved_steps.pkl` file using `pickle` for easy loading in the web app.

## Files in This Repository

-   `streamlit_app.py`: The main entry point for the Streamlit application. It handles the navigation between the "Explore" and "Predict" pages.
-   `explore_page.py`: Contains the code for the data visualization and exploration page of the app.
-   `predict_page.py`: Contains the code for the salary prediction user interface and model inference.
-   `salary_predictions.ipynb`: A Jupyter Notebook detailing the entire data analysis, cleaning, model training, and evaluation process.
-   `saved_steps.pkl`: A pickled file containing the trained `DecisionTreeRegressor` model and the label encoders.
-   `requirements.txt`: A list of all the Python packages required to run this project.
-   `survey_results_public.csv`: The raw dataset from the Stack Overflow Developer Survey 2020.

## How to Run the Project

To run this application on your local machine, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Create and activate a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install the required dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Prepare Data:**
    *   Ensure the `survey_results_public.csv` file is present in the root directory of the project.

5.  **Run the Streamlit application:**
    ```bash
    streamlit run streamlit_app.py
    ```
