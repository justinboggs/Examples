How to deploy a Flask app to Heroku

https://pybit.es/deploy-flask-heroku.html

https://medium.com/the-andela-way/deploying-a-python-flask-app-to-heroku-41250bda27d0

1. YOUR MACHINE: Build your Flask app and get it working. Make sure to use `app.py`
2. HEROKU: Create a new Heroku app (`MyApp`) and choose `Heroku CLI` - this will create a repository as well
3. YOUR MACHINE: Install Heroku CLI
4. YOUR MACHINE: Log in to CLI 
5. YOUR MACHINE: Clone your repo to a local folder:
	cd MyFolder 
	git clone https://heroku.com/bigtoga/repos/MyApp.git 
6. YOUR MACHINE: Copy your app files to this new directory
7. YOUR MACHINE: git add .; git commit -am `Msg`; git push heroku aster
8. YOUR MACHINE: In the folder, run `pip install gunicorn`
9. YOUR MACHINE: In the folder, run `pip freeze > requirements.txt`
10. YOUR MACHINE: In the folder, create a file named `Procfile` w/ one line: `web: gunicorn app:app`. The `app:app` says `I have a Python script named app.py - run that using python`
11. YOUR MACHINE: Re-do the git add/commit/push to get all files up there
11. YOUR MACHINE: spin up the app! `heroku ps:scale web=1` # starts a heroku `dyno` - a worker
12. YOUR MACHINE: heroku open

### Do I have any workers currently running?
~~~
>>> heroku ps
Free dyno hours quota remaining this month: 550h 0m (100%)
Free dyno usage for this app: 0h 0m (0%)
For more information on dyno sleeping and how to upgrade, see:
https://devcenter.heroku.com/articles/dyno-sleeping

=== web (Free): gunicorn app:app (1)
web.1: up 2020/03/28 10:55:39 -0500 (~ 4m ago)
~~~

### If your app crashed
I had a lot of trouble w pip freeze - it simply was not accurately capturing the dependencies (used Anaconda prompt on Windows 10). I created my requirements.txt, then added additional items that were imported in app.py

** You can look at logs (below) to see Import failures **

### Heroku sets up logging automatically - it retains recent 1,500 lines of your consolidated logs, which expire after 1 week
~~~
heroku logs 

# Last 10 log entries: 
heroku logs -n 10

# "live" log:
heroku logs --tail
~~~