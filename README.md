# Django-ci
 a simple Continuous Integration process using GitHub Actions
 
 
 ## Objectives
 - Learn the basics of using Git repository 
 - Learn the basics of GitHub Actions and deploy a simple CI process


## Basic requirements:
- Basic knowledge in GitHub and Git useage
- Basic knowledge in YAML formmating 
- GitHub Account
- IDE with git client connected to the github account



## Getting Started:
### 1. Fork this example repository
### 2. Delete .github/workflows folder
### 3. Clone the repository to local machine
### 4. Go to "Actions" in the repository Github
### 5. Create a new workflow from scratch ("Manual workflow")
### 6. Delete the contant of the yaml file
### 7. Copy the content of this yaml file (will be explained later):

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
    - name: Set up Python 3.9
      uses: actions/setup-python@v2
      with:
        python-version: 3.9
    - name: Install Dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r Django-cicd/requirements.txt
    - name: Run Tests
      run: |
        python Django-cicd/manage.py test app
```

### 8. Push the "Start commit" button (up right). You now have a basic workflow with tests.
### 9. On your local machine preforme a "pull" request.
### 10. Do a sample "Push" who faile the tests
With your favorit IDE (after the local repository had been added) go to Django-cicd/app/tests.py and change:

```
    def test_about(self):
        """Tests the about page."""
        response = self.client.get('/about/')
        self.assertContains(response, 'About', 3, 200)
        #self.assertEqual('22222'.upper(), 'FOO')
```

to:

```
    def test_about(self):
        """Tests the about page."""
        response = self.client.get('/about/')
        #self.assertContains(response, 'About', 3, 200)
        self.assertEqual('22222'.upper(), 'FOO')
```
*we comment the "good" test and uncomment a sure-fail test

### 11. Perform a stage and commit (give the commit a rememberable name like: "test 1"); then do a push
### 12. See the results
 - Go to the GitHub Actions section in the online repository
 - Look under "X workflow runs" and see the last one that ran (shuold be with a white X in a red circle near it)
 - click on it and then click on the box with "build" on it.
 - Search the failuire reasone. It sould look lik this:
 ![fail image from github](https://github.com/itamarweb/Django-ci/raw/master/FailTest.jpg) 
## 13. Do Steps 10, 11, 12 again but change the commant
revert step 10 so that the "bad" test will be commented
```
    def test_about(self):
        """Tests the about page."""
        response = self.client.get('/about/')
        self.assertContains(response, 'About', 3, 200)
        #self.assertEqual('22222'.upper(), 'FOO')
```
and do a pull-stage-commit-push to see the results:

![pass tests image from githu](https://github.com/itamarweb/Django-ci/raw/master/PassTest.jpg)


## 14. Chillout have a drink and keep on coding!

<br/><br/><br/><br/>
# Understanding the workflow YAML

next is the explanation of the workflow yaml file statement by statement.


```
name: Django CI
```
Gives the workflow a name

```
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]
```
states the trigers of the work flow and the context:
- do this workflow on a "push" for the "master" branch
- do this workflow on "pull_request" (befor the pull itself) for the "master" branch

```
jobs:
  build: 
```
state a single job - "build" (in here we also test the app)


```
jobs:
  build: 
```
state a single job - "build" (in here we also test the app)


```
  runs-on: ubuntu-latest 
```
tell the workflow environment to be the latest version ob ubuntu


```
 steps:
    - uses: actions/checkout@v2
```
start a job steps list and tells it to use the "actions/checkout@v2" module


```
 - name: Set up Python 3.9
      uses: actions/setup-python@v2
      with:
        python-version: 3.9
    - name: Install Dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r Django-cicd/requirements.txt
```
set up the python environment and install dependencies with [pip](https://pypi.org/project/pip/)


```
    - name: Run Tests
      run: |
        python Django-cicd/manage.py test app

```
run the tests using [Django](https://www.djangoproject.com/) built in test module.

### if one of the steps fails for some reason you'll be notified


