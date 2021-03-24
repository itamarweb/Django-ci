# Django-ci
 a simple Continuous Integration process using GitHub Actions
 
 
 ## Objectives
 - Learn the basics of using Git repository 
 - Learn the basics of GitHub Actions and deploy a simple CI process


## Basic requirements:
- Basic knowledge in GitHub and Git useage
- Basic knowledge in YAML formmating 
- GitHub Account




## 1. Fork this example repository
## 2. Delete .github/workflows folder
## 3. Clone the repository to local machine
## 4. Go to "Actions" in the repository Github
## 5. Create a new workflow from scratch ("Manual workflow")
## 6. Delete the contant of the yaml file
## 7. Copy the content of this yaml file (will be explained later):

```
name: Django CI

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build: 

    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.8
      uses: actions/setup-python@v2
      with:
        python-version: 3.9
    - name: Install Dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r Django-cicd/requirements.txt
        pip install coverage
    - name: Run Tests
      run: |
        python Django-cicd/manage.py test app
```


