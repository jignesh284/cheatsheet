# steps to build Python application with numpy, pandas, scipy, and flask

```diff
//creates a virtual environment for the files
- pip install pipenv

//activate virtual environment
- pipenv shell

//install dependencies in new environment
- pip install gunicorn
- pip install flask
- pip install numpy
- pip install pandas
- pip install scipy

//once installed all the dependenies in local (test the application in local)

create a file name 'Procfile' in root add following line to the file:
- web: gunicorn app:app

delete Pipfile from the folder

//will gather all the dependencies for the project from virtual environment 
- pip freeze > requirements.txt

// Creating git setup for heroku

- git init
- heroku git:remote -a [HEROKU-PROJECT-NAME]

//  set the build pack to be heroku python 
- heroku buildpacks:set heroku/python

- git push heroku master

Hurray ! you are good to go
```
