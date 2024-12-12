from flask import Flask, request

app = Flask(__name__)


@app.route("/robot", methods=["POST"])
def robot():
    form = request.form
    if form['metal'] == "Yes":
        return "You're a robot!"
    elif "error" in form["infinity"].lower():
        return "You're a robot!"
    elif form["food"] == "synthetic oil":
        return "You're a robot!"
    else:
        return "Hi there fellow human"


@app.route('/')
def index():
    page = ""
    with open("form.html", "r") as f:
      page = f.read()
    return page

app.run(host='0.0.0.0', port=81)
