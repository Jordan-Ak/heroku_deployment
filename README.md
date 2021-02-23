# heroku_deployment
This minor django project is to cover the steps that will help you deploy a django project to heroku.

Put the following commands in your command line.
1. create your virtual env with "python -m venv {virtual_environment_name}" # To create the virutal environment
2. "{virtual_environment_name}\scripts\activate" # To activate the virutal environment
3. pip install django # To install Django in your virtual environment
3. "django-admin startproject {project_name} ." #To start your project freshly
4. "python manage.py startapp {app_name}" # To start an app within the project.
5. make a new file urls.py in {app_name} #To give the apps a separate urls.py file
6. follow instructions in {project_name} urls.py to include the {app_name} urls.py in the project #So the url path of the app is included in the project.
7. in settings.py in the {project_name} directory add {app_name} to  installed apps as a string format. # This ensures the app works with the project
8. in {app_name} views.py make following importation "from django.views.generic import TemplateView" #This helps to import a generic view for quicker development.
9. add urls you want to use in the page in your {app_name} urls.py #If you don't know how to do this step check out my own urls.py in my 'deploys' app.
10. In views implement the TemplateView to make a class or 2 and supply the template name #YOu can check out my code.
11. make a new directory templates in your {app_name} directory and within that directory make a new directory with the name of your app
12. Inside the {app_name} of the templates put your templates file.#
13. type in your cmd "Python manage.py runserver" #This should run your site on your local server.

Now that you have confirmed that everythin is in check it is time to configure your app to deploy to heroku.

For deploying a python file you need to make the following configurations (I will also list what should be contained within them):
1. A "Procfile": This file should be spelt exactly the way I did with no extensions. Capital P and nothing at the end (I mean no ".txt" or ".py")
      The contents of the "Procfile" is as follows : "web: gunicorn {project_name}.wsgi --log-file -".This file should be at the root directory of your project(The directory that       contains manage.py) That is all for the Procfile.

2. A "runtime.txt": This file just contains the python version that would run your application. It should be typed as follows.
      "python-3.7.9" There should be no spaces and the 'p' is lowercase. On the heroku site you should see a list of acceptable python versions, choose the one closest to your           current python version. This file should be at the root directory of your project(The directory that contains manage.py)
 
3. You need gunicorn: to install gunicorn in your virtual environment type: "pip install gunicorn." This would install gunicorn for you to use.

4. This next step depends on if you have static files in your project or not. Follow this part closely as it is not included in my source code or go to this link to see my project deployed with static files "https://github.com/Jordan-Ak/Blog". If you are sure you don't need this skip to the next step
    So to handle static files "Whitenoise" is a package we use. Before installing whitenoise ensure there is a folder called 'static' in your root directory.
    so type in your terminal "pip install whitenoise". after it installs you have to include it in you middleware and installed apps in your settings.py file in your main            project folder.
    so type "whitenoise.middleware.WhiteNoiseMiddleware" in the middleware section and "whitenoise.runserver_nostatic" in the installed apps section in your settings.py file.
    At the bottom of the settings.py file type the following for the filepath and storage of static files: "STATICFILES_DIRS = "[str(BASE_DIR.joinpath('static'))]"
    Also type at the bottom of the settings.py file: "STATIC_ROOT = str(BASE_DIR.joinpath('staticfiles'))"
    Lastly also type at the same location: "STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'"
    This is all for whitenoise I promise!

5. Another file we would need is the "requirements.txt" file. The contents of this file are the dependencies heroku would need to run your application on their server.
    So to get the contents of this file easily type in your command line: "pip freeze > requirements.txt". This command creates the file in the current directory(Which should be     your project_root directory) and also its contents. so you should see things like: "django == 3.1.6, whitenoise ==5.2.0, etc"

At this point activate your version control system for me that is git. Note that you can activate this at any point you want at your project. so type in your cmd "git init" or whatever initializes your version control system if you aren't using git.
 
 After that you now have all the additional files you need for heroku deployment but the next thing is to download your heroku toolbelt. If you have to type in your commandline concerning heroku ensure that it is on a new command line interface entirely. You want heroku to be available all over your system and not just in your virtual environment.
 
 To donwload the heroku toolbelt go to this link "https://devcenter.heroku.com/articles/heroku-cli" If this link doesn't work then search for how to download the toolbelt.
 
 After this toolbelt is downloaded you can type in your commandline with your virtual environment again.
 Type in your command line "Heroku login". You might enter your credentials in your cmd or in your browser doesn't matter.
 next to type in your command line is "heroku create". you can add a name after that like "heroku create heroku_deployment". but the name has to be unique on heroku if not it wouldn't be created.
 After typing heroku create you should see the link of what you created example: "https://heroku-deployment.herokuapp.com/" 
 After that the next thing is to type "git remote -v " This step is just to check if your heroku link was automatically added as a remote repository for your project. if not type "heroku git:remote -a {heroku-link}" That would include it.
 
 At this point hold on we are almost done.
 in your settings.py file at "ALLOWED_HOSTS" input the name of your site example: "heroku-deployment.herokuapp.com"
 
 Next check the status of your app by typing "git status."
 add files by typing " git add ."
 then commit with a message by typing "git commit -m "Heroku configuration."
 
 *Now if you didn't add static files and skipped no.4 type in your command line "heroku config:set DISABLE_COLLECTSTATIC=1" as the name implies it disables static files.*
 
 Next type in your cmd  "git push heroku master" and after the push type "heroku ps:scale web=1"
 lastly type heroku open to see the deployed project in your browser.
 
 That is all for deploying your project on heroku
 
 The source code for this repository covers non-static files.
 To see my source code for a static filed project go to this link "https://github.com/Jordan-Ak/Blog" 
                          
    
    


