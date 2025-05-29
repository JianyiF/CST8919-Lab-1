# CST8919 Lab 1: Implementing User Login with Flask and Auth0

## 1. create an Auth0 Account and configure you login box
![image](https://github.com/user-attachments/assets/a33f00c5-18ec-45df-94e0-0b3eae896b57)
take the log in portal and it will log you in with the created username and password
![image](https://github.com/user-attachments/assets/f735189a-d867-4f2e-9fdc-e4aeb1a143ab)
and this is the default APP information
![image](https://github.com/user-attachments/assets/d1364195-0634-405c-b59c-2524f199f878)



## 2. Getting Started with local

Download Sample locally

Set Allowed Callback URLs
```bash
http://localhost:3000/callback
```
Set Allowed Logout URLs
```bash
http://localhost:3000
```
Run Docker image to build up the environment
```bash
sh exec.sh
```

## 3. setup local enironment

To get app secret key, you will need to run code 
```bash
openssl rand -hex 32
```
and then copy the output into .env

To add protected page, first create a protected.html in templkate folder, and add /protected command in python file
```html
<!DOCTYPE html>
<html>
<head>
    <title>Protected Page</title>
</head>
<body>
    <h1>This is a protected page.</h1>
    <pre>{{ pretty }}</pre>
    <a href="{{ url_for('logout') }}">Logout</a>
</body>
</html>
```

```python
def requires_auth(f):
    @wraps(f)
    def decorated(*args, **kwargs):
        if "user" not in session:
            return redirect(url_for("login", next=request.path))
        return f(*args, **kwargs)
    return decorated



@app.route("/protected")
@requires_auth
def protected():
    return render_template(
        "protected.html",
        session=session.get("user"),
        pretty=json.dumps(session.get("user"), indent=4),
)
```
Then you will build up and test the log in page.


## Video demo 
YouTube video demo Link:
https://youtu.be/cZb1gaqdqYc
