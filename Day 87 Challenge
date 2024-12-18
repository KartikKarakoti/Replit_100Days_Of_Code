import os

from flask import Flask, redirect, request, session
from replit import db

# TODO: change this to your replit username
replit_username = "DavidAtReplit"

app = Flask(__name__, static_url_path="/static")
app.secret_key = os.urandom(24)

db["user"] = {"username": "david", "password": "Baldy1"}


def getBlogs():
  entry = ""
  with open("entry.html", "r") as f:
    entry = f.read()
  keys = db.keys()
  keys = list(keys)
  content = ""
  for key in reversed(keys):
    thisEntry = entry
    if key != "user":
      thisEntry = thisEntry.replace("{title}", db[key]["title"])
      thisEntry = thisEntry.replace("{date}", db[key]["date"])
      thisEntry = thisEntry.replace("{body}", db[key]["body"])
      content += thisEntry
  return content


@app.route('/')
def index():
  userid = request.headers['X-Replit-User-Name']
  if userid == replit_username:
    return redirect("/edit")
  page = ""
  with open("blog.html", "r") as f:
    page = f.read()
  page = page.replace("{content}", getBlogs())
  return page


@app.route('/loginForm')
def loginForm():
  userid = request.headers['X-Replit-User-Name']
  if userid == replit_username:
    return redirect("/edit")
  page = ""
  with open("login.html", "r") as f:
    page = f.read()
  return page


@app.route('/login', methods=["POST"])
def login():
  userid = request.headers['X-Replit-User-Name']
  if userid == replit_username:
    return redirect("/edit")
  form = request.form
  if form["username"] == db["user"]["username"] and form["password"] == db[
      "user"]["password"]:
    session["user"] = True
    return redirect("/edit")
  else:
    return redirect("/loginForm")


@app.route("/edit")
def edit():
  userid = request.headers['X-Replit-User-Name']
  print(userid)
  if userid != replit_username:
    return redirect("/")
  page = ""
  with open("edit.html", "r") as f:
    page = f.read()
  page = page.replace("{content}", getBlogs())
  return page


@app.route("/add", methods=["POST"])
def add():
  userid = request.headers['X-Replit-User-Name']
  if userid != replit_username:
    return redirect("/")
  form = request.form
  entry = {"title": form["title"], "date": form["date"], "body": form["body"]}
  db[form["date"]] = entry
  return redirect("/edit")


@app.route("/logout")
def logout():
  session.clear()
  return redirect("/")


app.run(host='0.0.0.0', port=81)
