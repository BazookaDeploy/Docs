Installation
===================================

System overview
-----------------

Bazooka is a web application composed ot three main parts:

- a **Web site** which will allow you configure the system and deploy applications
- a **Controller** which is the windows service dedicated to running tasks and scheduled deployments
- one or more **Agents** to be installed on the machines where you will deploy your applications. They will execute all the needed steps for every deploy as configured

To install Bazooka you must first download the  `latest release <https://github.com/BazookaDeploy/Bazooka/releases>`_ from Github and then we can start.

Database
-----------

The first thing to install will be the database. SQL Server 2008 ad 2012 have been extensively tested but newer versions should be fine nonetheless.

To install the database, simply create a new Database in you SQL Server instance and then apply the *dacpac* file inside the **database** package downloaded from Github (If yu don't know how to apply a dacpac file a guide can be found  `here<http://blogs.msmvps.com/deborahk/deploying-a-dacpac-with-sql-server-management-studio/>`_).

Controller
-----------

Web site
----------

Agent
----------

