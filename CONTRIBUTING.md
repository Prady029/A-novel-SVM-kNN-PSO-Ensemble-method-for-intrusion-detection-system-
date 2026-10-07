# Contributing to SVM-kNN-PSO Ensemble IDS

We welcome contributions to this research implementation! This document provides guidelines for contributing.

## 🚀 Quick Start

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/your-username/A-novel-SVM-kNN-PSO-Ensemble-method-for-intrusion-detection-system-.git
   cd A-novel-SVM-kNN-PSO-Ensemble-method-for-intrusion-detection-system-
   ```

3. **Set up development environment**:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

4. **Create a feature branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```

5. **Make your changes** and test them

6. **Submit a pull request**

## 🔧 Development Setup

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook / JupyterLab
- Git

### Environment Setup
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pip install flake8 black isort  # Development tools
```

### Running Notebooks
```bash
jupyter notebook
# Or for Colab: upload the notebook to Google Colab
```

## 📝 Code Style

We follow Python best practices and use automated tools for code quality:

### Formatting
- **Black** for code formatting
- **isort** for import sorting
- Line length: 88 characters (Black default)

```bash
# Format all Python files
black .

# Sort imports
isort .
```

### Linting
- **flake8** for style checking

```bash
flake8 . --max-line-length=88 --extend-ignore=E203,W503 --exclude=.git,__pycache__,.venv,venv,env
```

## 🧪 Testing Guidelines

Since this is a research notebook-based project, testing focuses on:

1. **Notebook Execution**: All notebooks should execute without errors
2. **Reproducibility**: Results should be reproducible with the same random seeds
3. **Documentation**: New features should include explanatory markdown cells

### Manual Testing
```bash
# Execute notebooks headless (for CI)
pip install nbconvert
jupyter nbconvert --to notebook --execute Soft_Computing_project.ipynb --stdout
```

## 📋 Pull Request Guidelines

### Before Submitting
- [ ] Code follows style guidelines (`black`, `isort`, `flake8` pass)
- [ ] Notebooks execute without errors
- [ ] New functionality includes documentation in markdown cells
- [ ] README.md is updated if needed

### Pull Request Description
Include:
- **Purpose**: What does this PR accomplish?
- **Changes**: What specific changes were made?
- **Testing**: How was this tested?
- **Breaking Changes**: Any backwards incompatible changes?

### Example PR Description
```
## Purpose
Add support for additional base classifiers in the ensemble

## Changes
- Added Random Forest and XGBoost as optional base classifiers
- Updated ensemble weight optimization to handle variable number of classifiers
- Added configuration section for classifier selection

## Testing
- Verified notebook executes with new classifiers
- Compared accuracy with original SVM/kNN ensemble

## Breaking Changes
None - new classifiers are optional
```

## 🐛 Bug Reports

When reporting bugs, please include:

1. **Environment**: Python version, OS, package versions
2. **Reproduction**: Minimal steps to reproduce the issue
3. **Expected vs Actual**: What you expected vs what happened
4. **Error Messages**: Full error traceback if applicable

Use the issue template:
```
**Environment:**
- Python: 3.9.7
- OS: Ubuntu 20.04
- Scikit-learn: 1.0.0

**Bug Description:**
Brief description of the issue

**Reproduction:**
1. Step 1
2. Step 2
3. Step 3

**Expected Behavior:**
What should happen

**Actual Behavior:**
What actually happens

**Error Message:**
```
Full traceback here
```
```

## 💡 Feature Requests

For new features:
1. **Check existing issues** to avoid duplicates
2. **Describe the use case** - why is this needed?
3. **Propose implementation** if you have ideas
4. **Consider backwards compatibility**

## 📚 Documentation

### Notebook Documentation
- Use clear, descriptive markdown cells
- Include mathematical formulations where relevant
- Add references to original papers
- Include expected outputs/visualizations

### Adding Documentation
- Update README.md for user-facing changes
- Add docstrings for any helper functions
- Include examples for new functionality

## 🤝 Community Guidelines

- **Be respectful** and inclusive
- **Help others** learn and contribute
- **Ask questions** if something is unclear
- **Provide constructive feedback**

## 📞 Getting Help

- **GitHub Issues**: For bugs and feature requests
- **GitHub Discussions**: For questions and general discussion

Thank you for contributing to SVM-kNN-PSO Ensemble IDS! 🎉