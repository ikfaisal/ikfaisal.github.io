---
title:  "Create A Simple Web Application & Deploy In Herokuy"
---

In this blog I'll create a simple hello world application and deploy that application to heroku.

## Flask (web framework)

Flask is a micro web framework written in Python. It is classified as a microframework because it does not require particular tools or libraries.

Using any text editor create an app.py file.

```
from flask import Flask, render_template, jsonify, request
app = Flask(__name__)

@app.route("/")
def homepage():
    return render_template("index.html")

# Receive JSON from client, send response from server to client
@app.route('/sayHello', methods=['POST'])
def sayHello():
  json_ = request.get_json()
  return jsonify({'html': getHello(json_['helloName'])})

def getHello(json_):
    hellostring = "Hello, ", json_, "!"
    return hellostring

if __name__ == "__main__":
    app.run(debug=True)
```

Create a simple html page to interact with server. Place that file in templates folder.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Predict Job Title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="static/bootstrap.min.css" rel="stylesheet" media="screen">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  </head>
  <body>
    <div class="container">
      <h1>Predict Job Title</h2>
    </div>
    <div class="col-lg-12">
        <div class="row">
            <div class="col-lg-8">
                <textarea id='word' rows="15" cols="100">
                </textarea>
            </div>
            <div class="col-lg-4">
                <div id='wordResult'></div>
            </div>
        </div>
        <div class="row">
            <div class="col-offset-lg4 col-lg-4">
                <button type='button' id ='retrieve'>Submit</button>
            </div>
        </div>
    </div>
  </body>
</html>

<script>
    $(document).ready(function() {
        $('#retrieve').click(function() {
            var helloName = $('#word').val();

            $.ajax({
                url: "/sayHello",
                type: "POST",
                data: JSON.stringify({ helloName: helloName }),
                contentType: "application/json",
                success: function(response) {
                    $("#wordResult").html(response.html);
                },
                error: function(response) {
                    alert(response);
                }
            });
        });
    });
  </script>
```

Using following command fire up the site in local server http://127.0.0.1:5000/.

```
python app.py
```

## Heroku

Heroku provides custom buildpacks, where developers can deploy apps in any other programming language. For this reason, Heroku is said to be a polyglot platform. It lets the developer build, run, and scale applications in a similar manner across all programming languages.

Install the Heroku CLI
Download and install the Heroku CLI.

If you haven't already, log in to your Heroku account and follow the prompts to create a new app. We'll create an app called hello-world-dudes.

```
$ heroku login
```

```
$ heroku git:clone -a hello-world-dudes
$ cd hello-world-dudes
```

Copy all your files in this folder. Add requirement.txt and simply add libraries you need for your project.

```
flask
gunicorn
```

Add web: gunicorn app:app in a text file and save as Procfile without extension.

```
web: gunicorn app:app
```

```
$ git add .
$ git commit -am "make it better"
$ git push heroku master
```

End of the day, file structure should be as follows.

![](/img/HerokuFileStructure.jpg)
