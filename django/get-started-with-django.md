# Get Started With Django

Create a folder using `mkdir` or clone a repo from your git.

Install this if not:

```sh
pipenv --version #check if installed
pip install --user pipenv
```

Install Django inside your folder:

```sh
pipenv install django
```

Check if these files exists `Pipfile` and `Pipfile.loc` these files are like package.json in React.

Then activate the virtual environment:

```sh
pipenv shell
```

Then do this:

```sh
django-admin startproject foo .
```

Take note that the `foo` folder is the folder that we created for example.

Now, run your django in the web!

```sh
python manage.py runserver
```

Or add a port if you want like this:

```sh
python manage.py runserver 3000
```
