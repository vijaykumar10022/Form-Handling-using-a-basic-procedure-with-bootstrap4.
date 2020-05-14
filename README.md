# Form-Handling-using-a-basic-procedure-with-bootstrap4.
## What is The Form?
* Form (HTML) A webform, web form or HTML form on a web page allows a user to enter data that is sent to a server for processing. Forms can resemble paper or database forms because web users fill out the forms using checkboxes, radio buttons, or text fields.
## Where Forms are using?
* HTML Forms are required when you want to collect some data from the site visitor.
	* For example during user registration you would like to collect information such as name, email,address, credit card, etc.
	* A form will take input from the site visitor and then will post it to a back-end application such as Django,Flask,CGI, ASP Script or 			PHP script etc.
* The back-end application will perform required processing on the passed data based on defined business logic inside the application.
## Django Forms:
  * Django using models to store form information .

  * It is similar to the ModelForm class that creates a form by using the Model, but it does not require the Model.

  * Each field of the form class map to the HTML form &lt;input&gt; element and each one is a class itself, it manages form data and  
  performs validation while submitting the form.
  ![IMAGE ALT TEXT HERE](https://github.com/vijaykumar10022/Form-Handling-using-a-basic-procedure-with-bootstrap4./blob/master/total%20image.JPG)
  
  * Here we are find to analyse to complete Form working mechanism in django  is shown in above image
  
  
  * Here we use forms to communicate between user to model
  
  * User do the action is GET it going to Url and than it navigate to views, Views is finding the templates is avialable navigation is done to the templates and then template having form here user to POST the information from template in form to views and then those information is stored to models and finally user want to get those information agine user send request to urls it navigate to views and view to models if models contains user information those information send to views and then it navigate to tempaltes for the purpose of displaying 
## Building a Form in Django
### Lets see an example, in which we are creating some fields too.

* Suppose we want to create a Model to get User information, use the following code.
~~~ python
from django.db import models


class Register(models.Model):
	firstName=models.CharField(max_length=30,null=True)
	lastName=models.CharField(max_length=30,null=True)
	email=models.CharField(max_length=30,null=True)
	password=models.CharField(max_length=30,null=True)
	birthDate=models.CharField(max_length=30,null=True)
	phoneNumber=models.CharField(max_length=30,null=True)
 age=models.CharField(max_length=30,null=True)
	Gender=models.CharField(max_length=30,null=True)
	def __str__(self):
		return ""
~~~

* Put this code into the models.py file.

* A User  is created that contains  fields of CharField type. Charfield is a class and used to create an HTML text input component in the form
* The label is used to set HTML label of the component and max_length sets length of an input value.


* after that we have to pass two commad to insert data to database
  * python manage.py makemigrations
  > to pass this command in particular project path
  * makemigrations : It is used to create a migration file that contains code for the tabled schema of a model.
  ![IMAGE ALT TEXT HERE](https://github.com/vijaykumar10022/Form-Handling-using-a-basic-procedure-with-bootstrap4./blob/master/makemigrations.JPG)
 
  * python manage.py migrate
  > this command is used to intrat with models to database
  * migrate : It creates table according to the schema defined in the migration file.
  ![IMAGE ALT TEXT HERE](https://github.com/vijaykumar10022/Form-Handling-using-a-basic-procedure-with-bootstrap4./blob/master/migrate.JPG)
  
  
  ## Instantiating Form in Django
  * Now, we need to instantiate the form in views.py file. See, the below code.
  ### // views.py
  ~~~ python
  from django.shortcuts import render,redirect
  from form.models import Register
  def form(request):
   if request.method == "POST":
    Register.objects.create(firstName=request.POST['firstName'],lastName=request.POST["lastName"],email=request.POST['email'],password=request.POST['password'],birthDate=request.POST['birthDate'],phoneNumber=request.POST['phoneNumber'],Gender=request.POST['Gender'])
    return redirect('/display')
   return render(request,'form/data.html')

  def display(request):
   data=Register.objects.all()
   return render(request,'form/display.html',{'data':data})
  ~~~
  
* Passing the context of form into index template that looks like this:
## // data.html
~~~ html
<!DOCTYPE html>
<html>
<head>
	<title>::Forms-apssdc::</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
</head>
<body>
<div  >
            <form class="form-horizontal" role="form" method="POST" action="{% url 'form' %}">
            	{% csrf_token %}
                <h2 align="center">Registration</h2>
                <div class="form-group">
                    <label for="firstName" class="col-sm-3 control-label">First Name</label>
                    <div class="col-sm-9">
                        <input type="text" id="firstName" placeholder="First Name" class="form-control" name= "firstName"autofocus>
                    </div>
                </div>
                <div class="form-group">
                    <label for="lastName" class="col-sm-3 control-label">Last Name</label>
                    <div class="col-sm-9">
                        <input type="text" id="lastName" placeholder="Last Name" class="form-control" name ="lastName" autofocus>
                    </div>
                </div>
                <div class="form-group">
                    <label for="email" class="col-sm-3 control-label">Email* </label>
                    <div class="col-sm-9">
                        <input type="email" id="email" placeholder="Email" class="form-control" name= "email">
                    </div>
                </div>
                <div class="form-group">
                    <label for="password" class="col-sm-3 control-label">Password*</label>
                    <div class="col-sm-9">
                        <input type="password" id="password" placeholder="Password" class="form-control" name="password">
                    </div>
                </div>
                <div class="form-group">
                    <label for="birthDate" class="col-sm-3 control-label">Date of Birth*</label>
                    <div class="col-sm-9">
                        <input type="date" id="birthDate" class="form-control" name="birthDate">
                    </div>
                </div>
                <div class="form-group">
                    <label for="phoneNumber" class="col-sm-3 control-label">Phone number </label>
                    <div class="col-sm-9">
                        <input type="phoneNumber" id="phoneNumber" placeholder="Phone number" class="form-control" name="phoneNumber">
                        <span class="help-block">Your phone number won't be disclosed anywhere </span>
                    </div>
                </div>
                <div class="form-group">
                    <label class="control-label col-sm-3">Gender</label>
                    <div class="col-sm-6">
                        <div class="row">
                            <div class="col-sm-4">
                                <label class="radio-inline">
                                    <input type="radio" id="femaleRadio" value="Female" name="Gender">Female
                                </label>
                            </div>
                            <div class="col-sm-4">
                                <label class="radio-inline">
                                    <input type="radio" id="maleRadio" value="Male" name="Gender">Male
                                </label>
                            </div>
                        </div>
                    </div>
                </div> <!-- /.form-group -->
                <div class="form-group">
                    <div class="col-sm-9 col-sm-offset-3">
                        <span class="help-block">*Required fields</span>
                    </div>
                </div>
                <button type="submit" class="btn btn-primary btn-block">Register</button>
            </form> <!-- /form -->
        </div> <!-- ./container -->
</body>
</html>
~~~
* Provide the URL in urls.py
~~~ python
from django.contrib import admin
from django.urls import path
from form import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('register/',views.form,name="form"),
    path('display/',views.display,name="display"),
]
~~~
## Run Server and access the form at browser by localhost:8000/register, and it will produce the following output.

![IMAGE ALT TEXT HERE](https://github.com/vijaykumar10022/Form-Handling-using-a-basic-procedure-with-bootstrap4./blob/master/registeroutput.png)


* User Get the Registration for show  above pic

* when ever user Get This form to fill all the deatils  listed above and then to submit those data to views
* in views to store respective information into respective fields into model
* And than Rediect to Display  funtion in views
* display funtion is to get all stored data into one variable
* after that those data to convert dictionary because of easy to access data 

## //Display.html
~~~ html
<!DOCTYPE html>
<html>
<head>
	<title>::Display::</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
</head>
<body>
<div class="container">
<table class="table">
  <caption>List of users</caption>
  <thead>
    <tr>
      <th scope="col">FirstName</th>
      <th scope="col">LastName</th>
      <th scope="col">Email</th>
      <th scope="col">Password</th>
      <th scope="col">Date of Birth</th>
      <th scope="col">Phone Number</th>
      <th scope="col">Height</th>
      <th scope="col">Weight</th>
      <th scope="col">Gender</th>
    </tr>
  </thead>
  <tbody>
  	{% for i in data %}
    <tr>
      <td>{{i.firstName}}</td>
      <td>{{i.lastName}}</td>
      <td>{{i.email}}</td>
      <td>{{i.password}}</td>
      <td>{{i.birthDate}}</td>
      <td>{{i.phoneNumber}}</td>
      <td>{{i.height}}</td>
      <td>{{i.weight}}</td>
      <td>{{i.Gender}}</td>
    </tr>
    {% endfor%}
  </tbody>
</table>
</div>
</body>
</html>
~~~

* here we have to  display all the information passed from the display funtion in views  in tabler format by using table html tags with bootstrap shown in below like that


![IMAGE ALT TEXT HERE](https://github.com/vijaykumar10022/Form-Handling-using-a-basic-procedure-with-bootstrap4./blob/master/displaydata.png)

