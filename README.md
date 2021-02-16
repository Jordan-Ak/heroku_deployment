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

https://www.codementor.io/@jamesezechukwu/how-to-deploy-django-app-on-heroku-dtsee04d4
follow this link for remaining steps to deploy to heroku server.

