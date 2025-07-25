# SAST Machine Learning Project

This project leverages machine learning techniques to enhance Static Application Security Testing (SAST) workflows by dynamically analyzing code repositories. The goal is to identify potential security vulnerabilities and generate actionable insights for developers.

## Project Structure

- **src/**: Contains the main application code.
  - **main.py**: Entry point for the application, orchestrating the workflow.
  - **ml/**: Contains machine learning components.
    - **model.py**: Defines the machine learning model for training and predictions.
    - **preprocess.py**: Handles data preprocessing for the model.
  - **sast/**: Contains components specific to static analysis.
    - **analyzer.py**: Analyzes code repositories using the machine learning model.
    - **report_generator.py**: Generates reports based on analysis results.
  - **utils/**: Contains utility functions for logging and configuration management.

- **data/**: Contains datasets and models.
  - **sample_repos/**: Sample repositories for testing and training.
  - **models/**: Information about the models used in the project.

- **tests/**: Contains unit tests for the application components.
  - **test_analyzer.py**: Tests for the Analyzer class.
  - **test_model.py**: Tests for the Model class.
  - **test_helpers.py**: Tests for utility functions.

- **requirements.txt**: Lists the dependencies required for the project.

- **.gitignore**: Specifies files and directories to be ignored by Git.

## Setup Instructions

1. Clone the repository:
   ```
   git clone <repository-url>
   cd sast-ml-project
   ```

2. Install the required dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Prepare the data:
   - Place your sample repositories in the `data/sample_repos/` directory.

4. Run the application:
   ```
   python src/main.py
   ```

## Usage Guidelines

- The application will automatically read the code repositories from the specified directory and perform static analysis using the machine learning model.
- Generated reports will be available for review and further action.

## Contributing

Contributions are welcome! Please submit a pull request or open an issue for any enhancements or bug fixes.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
