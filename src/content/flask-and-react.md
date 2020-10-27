---
layout: post
title: How to Run Flask and React
image: img/test-tube.jpg
author: Pranay Aryal
date: 2019-11-10T10:00:00.000Z
tags:
  - Flask
  - React
---

I'm sure you know how to run Flask app as detailed in [here](http://flask.pocoo.org/)

Use <mark>create-react-app</mark> to build a skeleton boiler-plate React structure.

Copy over the folders into the Flask project.

The final directory structure:

```bash
flask_app
|_node_modules
|_build
|    |_static
|       |_css
|       |_js
|    |_asset-manifest.json
|    |_favicon.ico
|    |_index.html
|    |_manifest.json
|    |_service-worker.js
|_src
|    |_components
|       |_Hero.js
|    |_App.css
|    |_App.css
|    |_App.test.js
|    |_index.css
|    |_index.js
|    |_registerServiceWorker.js
|_serve.py
|_package.json
|_package-lock.json
```
Flask should be configured to serve the `build/index.hmtl` file.

This is the same file which will reference the compiled javascript code which are present in build/static/css and build/static/js folders.

Your `serve.py` should be like this:
```py
from flask import Flask, render_template
app = Flask(__name__, static_folder="build/static", template_folder="build")
@app.route("/")
def hello():
    return render_template('index.html')
print('Starting Flask!')
app.debug=True
app.run(host='0.0.0.0')
```

You will need two instance of terminals:

In one terminal go to the root folder of the project and type `npm run build`. This should create the static javascript and css code.

In another terminal run `python serve.py`. This will run the flask app.

Open the browser and visit http://localhost:5000. You should see your app running with the javascript code.

If you make any changes to React, you will have to run `npm run build` in another terminal to compile your javascript to static files so that Flask can recognize them.

You can also make api calls from React to your flask backend and use the returned variables to populate the html.

Unfortunately, this does not work with React's hot reloading.

I can be found in <a href="https://twitter.com/pranayaryal" target="__blank">twitter</a>

