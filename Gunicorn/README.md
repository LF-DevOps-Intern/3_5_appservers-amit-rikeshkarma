# Gunicorn Task Solution:
1. Create Django starter project in a separate virtual environment.
   - Install virtualenv using following commands:
     - `pip3 install virtualenv`
   - Now create a virtual environment using the command:
     - `python3 -m virtualenv django_sp_env`
   - Then activate the virtual environment using the command:
     - `source ./django_sp_env/bin/activate`
   - Now we install django in the virtual environment:
     - `pip3 install django`
   - Lastly we create a Django Project, lets call our project *django_starter_project* using the command:
     - `django-admin startproject django_starter_project`   
    ![Screenshot]()   
    We have created a Django starter project in a virtual environment.   

2. Deploy the 3 instance of application using Gunicorn in 8089 port.
   - Activate the virtual environment and install gunicorn:
     - `pip3 install gunicorn`
   - Lets add our IP address to the ALLOWED_HOSTS variable in the path _django_starter_project/settings.py_
    ![ALLOWED_HOSTS Snapshot]()
   - Now we run migrations:
     - `python3 manage.py makemigrations`
     - `python3 manage.py migrate`
   - Then let's test the sample project by running the following command:
     - `sudo ufw allow 8089`
     - This opens port:8089 by allowing it over the firewall. Let's check our Django server to test the setup so far using the command:
       - `python3 manage.py runserver 0.0.0.0:8089`
    ![Migrations and Runserver Snapshot]()
   - **Now we configure gunicorn**
     - Firstly, let’s make a configuration file for gunicorn server using following commands:
       - `mkdir gunicorn_conf`
       - `nano config.py`
       - Then add the following in the file:
         - command='./django_sp_env/bin/gunicorn'
         - pythonPath='./'
         - bind = '192.168.254.141:8089'
         - workers = 3
     - After we configure the configuration file we need to run the following command which will deploy 3 instance of application using Gunicorn in 8089 port:
       - `gunicorn -c gunicorn_config.py django_starter_project.wsgi`
     - Now we can test the server in the browser by using `192.168.254.141:8089`
    ![Gunicorn deployed snapshot]()
    ![Gunicorn deployed snapshot on browser]()


3. Dump access log in a file in non-default pattern.
4. Dump error log in a file.
   - We can use following command to dump the log files:
     - `gunicorn app_py:django_starter_project --error-logfile gunicorn.error.log --access-logfile gunicorn.log --capture-output`
   - And we can ls to check the files inside
     - `We can see ‘gunicorn.error.log’ and ‘gunicorn.log’ files now.
    ~[Log Files]()
