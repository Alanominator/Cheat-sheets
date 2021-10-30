# Creating a skeleton of djangoReactProject ( on linux )
______

### preparing the tools

> sudo apt install ....... ?

> sudo apt-get install python3-venv
> ...
___________________________________________

### creating virtual environment

> python3 -m venv myenv

> . myenv/bin/activate

### creating a file with reauirements for pip

> touch requirements.txt

_______

#### in requirements.txt write the packages you need

django
pillow
djangorestframework
_______

> pip3 install -r requirements.txt
_______

### then just create a django project

> django-admin startproject project_name
_______

### create app api

> cd project_name
> python3 manage.py startapp api

### create app frontend

> python3 manage.py startapp frontend


____

### add the following to INSTALLED_APPS in settings
```python
    "rest_framework",
    "api.apps.ApiConfig",
    "frontend.apps.FrontendConfig",
```

### cd project_name/api
___
> touch serializers.py
___________________________________________

.
___
#### cd frontend
>  mkdir static src templates
> touch babel.config.json   webpack.config.js
___
.
___
#### cd static
> mkdir frontend css images
___
.
___
#### cd frontend/src
> mkdir components
> touch index.js
___
___
#### cd frontend/src/components
> touch App.js
___
.
___________________________________________
### Let's install some packages

### but before do some things to avoid some problems
___
#### cd frontend
> npm config set proxy null
> npm config set https-proxy null
> npm config set registry http://registry.npmjs.org/
___
> npm init -y

> npm i webpack webpack-cli --save-dev

> npm i @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev

> npm i react react-dom --save-dev

> npm install @material-ui/core

> npm install @babel/plugin-proposal-class-properties

> npm install react-router-dom

> npm install @material-ui/icons
____

.
### in " frontend/babel.config.json " add this code

```javascript

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
```


### in " frontend/webpack.config.js " add in this code:

```javascript
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
```

### open frontend/package.json replace the code in "scripts" : { } with this code

```javascript
    "dev": "webpack --mode development --watch",
    "build":"webpack --mode production"
```
___________________________________________


### cd frontend/templates create a folder " frontend "
___
> mkdir frontend
___
### cd frontend/templates/frontend
___
> touch index.html
___
### in this file ( frontend/templates/frontend/index.html ) write this

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    {% load static %}
</head>

<body>
    <div id="main">
        <div id="app">
            
        </div>
    </div>

    <script src="{% static  'frontend/main.js' %}"></script>
</body>

</html>
```
___________________________________________

### in frontend/views.py make a function

```python

def index(request, *args, **kwargs):
    return render(request, "frontend/index.html")
    
```
________

### in frontend create " urls.py " and add:

```python
from django.urls import path
from .views import index

urlpatterns = [
    path('', index),
]
```
### in api create " urls.py " ;

### connect these urls with the main urls in " project_name/urls "

```python
from django.contrib import admin
from django.urls import path, include


urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('api.urls')),
    path('', include('frontend.urls')),
]
```
### make your first migrations
___
### cd project_name
> python3 manage.py makemigrations
> python3 manage.py migrate
___
.
# Done! Goodluck!
