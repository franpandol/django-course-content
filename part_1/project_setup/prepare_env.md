Welcome to the first class of the course!

To get started, we need to set up a virtual environment for our Python project. This will allow us to isolate our project from other Python libraries installed on our system.

For these we have plenty of tools, some classics like virtualenv and virtualenvwrapper and some newer ones like pipenv and poetry. 
We will be using pipenv.


**Instructions for macOS**

```bash
# install pyenv with brew
brew update && brew install pyenv
```

```bash
# install python 3.10 using pyenv
pyenv install 3.10.4
```

```bash
# create virtual environment
pyenv virtualenv 3.10.4 my_project
```


```bash
# activate virtual environment
pyenv activate my_project
```

Now in this environment we have a fresh python 3.10 installed . We are going to use Django so we need to install it in our virtual environment. We are using pip to install Django:

```bash
# install Django
pip install Django
```

The latest version of Django at the moment of writing this is 4.1. We can check it with:

```bash
# check Django version
python -m django --version
```

Using a virtual environment is a good practice that helps to isolate your project dependencies and avoid conflicts with other projects or libraries on your system. pyenv is a useful tool that makes it easy to create and manage virtual environments for Python projects.