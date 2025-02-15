# Contributing to Design Patterns in Python

Thank you for your interest in contributing to this project! Here are some guidelines to help you get started.

## Setting Up the Development Environment

1. **Fork the repository**: Click the "Fork" button at the top right corner of the repository page to create a copy of the repository in your GitHub account.

2. **Clone the repository**: Clone your forked repository to your local machine using the following command:

    ```sh
    git clone https://github.com/matiagimenez/design-patterns-explained.git
    cd design-patterns-explained
    ```

3. **Install Pipenv**: If you don't have Pipenv installed, you can install it using pip:

    ```sh
    pip install pipenv
    ```

4. **Install dependencies**: Navigate to the root directory of the repository and install the required dependencies:

    ```sh
    pipenv install --dev
    ```

5. **Activate the virtual environment**:
    ```sh
    pipenv shell
    ```

## Running Pre-Commit Hooks

This repository uses pre-commit hooks to ensure code quality and consistency. To set up pre-commit hooks, follow these steps:

1. **Install the pre-commit hooks**:

    ```sh
    pre-commit install
    ```

2. **Run the pre-commit hooks manually** (optional):
    ```sh
    pipenv run format
    ```

## Making Changes

1. **Create a new branch**: Create a new branch for your changes:

    ```sh
    git checkout -b <branch-name>
    ```

2. **Make your changes**: Make your changes to the codebase.

3. **Commit your changes**: Commit your changes with a descriptive commit message:

    ```sh
    git add .
    git commit -m "Description of the changes"
    ```

4. **Push your changes**: Push your changes to your forked repository:

    ```sh
    git push origin <branch-name>
    ```

5. **Create a pull request**: Go to the original repository and create a pull request from your forked repository. Provide a clear description of your changes and any relevant information.

## Code Style

Please ensure that your code adheres to the following guidelines:

-   Use meaningful variable, function and class names.
-   Ensure that your changes follow the project structure used in the repository.
