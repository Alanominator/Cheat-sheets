# creating a django-react project with postgresql database on linux
___________________________________________

(((

```javascript

for (let x; x < someArray.length; x++){
	console.log(x**2)
}

```

# preparing the tools

> sudo apt install .......

> sudo apt-get install python3-venv
> ...

)))
___________________________________________

# creating virtual environment

> python3 -m venv myenv

> . myenv/bin/activate

>(myenv) touch requirements.txt

_______

# in requirements.txt write the packages you need

django
pillow
psycopg2-binary 
psycopg2
djangorestframework

_______

>(myenv) pip install -r requirements.txt

# then just create a django project

>(myenv) django-admin startproject project_name
_______

# then create a database

>(myenv) sudo apt-get install libpq-dev python-dev
>(myenv) sudo pip install psycopg2

# open console postgresql
>(myenv) sudo -u postgres psql postgres

(((

# create a password

postgres=#  \password postgres

postgres=#  create user user_name with password 'password';
    alter role user_name set client_encoding to 'utf8';
    alter role user_name set default_transaction_isolation to 'read committed';
    alter role user_name set timezone to 'UTC';

)))

# create database

postgres=# create database django_db owner user_name;

# quit

postgres=#  \q

________

# open settings in your project

        'NAME': 'django_db',
        'USER' : 'user_name',
        'PASSWORD' : 'password',
        'HOST' : '127.0.0.1',
        'PORT' : '5432',

# make migrations

>(myenv) python3 manage.py makemigrations
...
>(myenv) python3 manage.py migrate

___________________________________________

# create app api

>(myenv) cd project_name
>(myenv) python3 manage.py startapp api

# add this to INSTALLED_APPS in settings

    "rest_framework",
    "api.apps.ApiConfig",

# create serializers.py in api

___________________________________________

# now create frontend app

>(myenv) cd project_name
>(myenv) python3 manage.py startapp frontend


# open settings in project_name, add this code to INSTALLED_APPS to registrate this app

    "frontend.apps.FrontendConfig",


>(myenv) cd frontend
>(myenv) mkdir static src templates

>(myenv) cd static
>(myenv) mkdir frontend css images

>(myenv) cd src
>(myenv) mkdir components

___________________________________________

>(myenv) cd frontend

>(myenv) npm init -y
>(myenv) npm i webpack webpack-cli --save-dev
>(myenv) npm i @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
>(myenv) npm i react react-dom --save-dev
>(myenv) npm install @material-ui/core
>(myenv) npm install @babel/plugin-proposal-class-properties
>(myenv) npm install react-router-dom
>(myenv) npm install @material-ui/icons

_______

in frontend create " babel.config.json "

in " babel.config.json " write this:

{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          "node": "10"
        }
      }
    ],
    "@babel/preset-react"
  ],
  "plugins": ["@babel/plugin-proposal-class-properties"]
}

_______

in frontend create " webpack.config.js " and in this file add the following:

const path = require("path");
const webpack = require("webpack");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, "./static/frontend"),
    filename: "[name].js",
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
    ],
  },
  optimization: {
    minimize: true,
  },
  plugins: [
    new webpack.DefinePlugin({
      "process.env": {
        // This has effect on the react lib size
        NODE_ENV: JSON.stringify("production"),
      },
    }),
  ],
};


# open package.json in frontend and replace code in "scripts" : { } with this code

    "dev": "webpack --mode development --watch",
    "build":"webpack --mode production"

___________________________________________

in frontend/src create a file " index.js "

inside frontend/templates create a folder " frontend " 
in frontend/templates/frontend create a file " index.html " and make a simple html structure

in head add
    {% load static %}
    ( jquery , ajax, google fonts )

in body create div with id="main" . in #main create #app

and script

<script src='{% static "frontend/main.js" %}'></script>

___________________________________________

in frontend/views.py make a function

def index(request, *args, **kwargs):
    return render(request, "frontend/index.html")

________

in frontend create " urls.py " and add:

from django.urls import path
from .views import index

urlpatterns = [
    path('', index),
]

connect it with urls in project_name

    path('', include('frontend.urls')),

________


Done! Goodluck!

# now you can create your first component

in frontend/src/components make " App.js "