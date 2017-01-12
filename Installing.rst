Installation
===================================

System overview
-----------------

Bazooka is a web application composed ot three main parts:

- a **Web site** which will allow you configure the system, set permissions and deploy applications
- a **Controller** which is a windows service dedicated to running tasks like sccheduled deployments, cache clleanups, periodic health checks and log compactions
- one or more **Agents** to be installed on the machines where you will deploy your applications. They will execute all the commands from the controller allowing deploys to be executed

To install Bazooka you must first download the  `latest release <https://github.com/BazookaDeploy/Bazooka/releases>`_ from Github and then we can start.

Database
-----------

The first thing to install will be the database. SQL Server 2008 ad 2012 have been extensively tested but newer versions should be fine nonetheless.

To install the database, simply create a new Database in you SQL Server instance and then apply the *dacpac* file inside the **database** package downloaded from Github (If you don't know how to apply a dacpac file a guide can be found    `here <http://blogs.msmvps.com/deborahk/deploying-a-dacpac-with-sql-server-management-studio/>`_ ) .

Controller
-----------

The Controller is a console application based on `Topshelf <https://topshelf.readthedocs.io/en/latest/>`_ that can be installed as a Windows service. Running the controller as a caonsole application is only useful to debug configuration errors and it is strongly recommended to run it in service mode. 

To install the Controller simply unpack the Controller archive downloaded previously and copy its content to a folder on the machine where you want to run the controller. After that the servvice can be installed as an Administrator from the command line with  

**Controller.exe install**

For more options you can consult the Topshelf `docs <https://topshelf.readthedocs.io/en/latest/overview/commandline.html>`_ .

After installation you can proceed to edit the configuration file to change the connection string to the previously created database then start the Controller service.

.. Note:: Make sure that the account running the service can connect to SQL server and the database. Your system administrator may want to create a dedicated user

Web site
----------

Agent
----------

