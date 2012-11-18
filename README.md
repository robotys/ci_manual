Codeigniter Workshop manual
===========================

This is to help with Codeigniter workshop as conducted by me. 

The What
--------

CodeIgniter is an Application Development Framework - a toolkit - for people who build web sites using PHP. Its goal is to enable you to **develop projects much faster** than you could if you were writing code from scratch, by providing a rich set of libraries for commonly needed tasks, as well as a **simple interface** and **logical structure** to access these libraries. CodeIgniter lets you creatively focus on your project by minimizing the amount of code needed for a given task.

The Why
-------

CodeIgniter is right for you if:

- You want a framework with a **small footprint**.
- You need **exceptional performance**.
- You need **broad compatibility with standard hosting** accounts that run a variety of PHP versions and configurations.
- You want a framework that requires **nearly zero configuration**.
- You want a framework that **does not require you to use the command line**.
- You want a framework that **does not require you to adhere to restrictive coding rules**.
- You do not want to be forced to learn a templating language (although a template parser is optionally available if you desire one).
- You eschew complexity, favoring **simple solutions**.
- You need clear, **thorough documentation**.

Session 0 : Installation and Folder Structure Example
--------------------------------------------------

Download Codeigniter [here](http://codeigniter.com/download.php)

Extract (unzip) to home folder (www or htdocs) so it looks like this:

		-www
		  -codeigniter
			-application
			-system
			-user_guide
			-index.php

If you like, change the name codeigniter into CI, so its simple to be called afterwards.

		-www
		  -ci
			-application
			-system
			-user_guide
			-index.php

However, we can change the folder structure to whatever we like. Structure as depicted below are quite widely used for codeigniter:
		
		-www
		  -app_name
			-application
			-index.php
		  -another_app
			-application
			-index.php
		  -ci_system

Just make sure we specify the location of systems file for the application to approriate location. Open the index.php file and change the system path to the new one:

		$system_path = '../ci_system';

This folder structure can cater multiple application within one domain with only one codeigniter core files (system). 

This make the upgrading easier and faster. To use multiple Codeigniter core for multiple application, so that we can fallback gracefully should something happen, we can use folder structure as below:

		-www
		  -app_name
			-application
			-index.php
		  -another_app
			-application
			-index.php
		  -ci_system_v21
		  -ci_system_v22

... and specify which application to use which version of codeigniter in its own index.php.

Test the installation by loading the app via url: http://localhost/app_name

Latest 'test page' design should be like below:

> image here!

And thus your installation is now complete! For some *nightmare* you can open application folder and wonder what is all the folder and files are doing. 

(Or you can always open the user_guide folder tor the helpful documents.)

/debug

Session 1: Model - View - Controller
------------------------------------

Codeigniter force the codes into MVC pattern. MVC separate the concerns of codes into 3 distinct function namely:

1. 	**Models**   
	Models are where the heavy processing is done. All the business process, database operation (CRUD) is done here. We always prefer Fat Models over Fat Controller
2.	**Controller**   
	Controller is the one who route the url to specified php class and method. Controller acts like traffic light which control the flow of data to be processed and flow of page to be display as view.
3.	**View**   
	View only manage the front-end aspect of our web app. All the designs/htmls and CSS are manage by view part of MVC.

The simplest flow of information for CodeIgniter app are as followed:

1.	A page is requested via url. Lets say Dashboard page. The url used is http://localhost/app_name/index.php/dashboard
2.	Codeigniter System will translate the uri and run the method **index** in class **Dashboard** form php file named **dashboard.php** inside *app_name/application/controller* folder.

		-www
		  -app_name
			-application
				-controllers
					-dashboard.php
			-index.php
		  -ci_system

		[dashboard.php]--------------------------
		class Dashboard extend CI_Controller{	
			function index(){
				echo 'Welcome To Dashboard';
			}
		} 

	here we can see that Codeigniter will run and display 'Welcome To Dashboard'. No Models and Views involved in this example.

More complex example when the data, lets say the string 'Welcome To Dashboard' is processed from models and the send to view files.

For this example we will create two new files at *application/models/m_dashboard.php* and another one at *application/view/v_dashboard.php*:

		-www
		  -app_name
			-application
				-controllers
					-dashboard.php
				-models
					-m_dashboard.php
				-views
					-v_dashboard.php
			-index.php
		  -ci_system