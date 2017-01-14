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

.. Note:: Make sure that the account running the service can connect to SQL server and the database. Your system administrator may want to create a dedicated user to tailor its permissions

Web site
----------

The Web site is a common MVC Application so to install it you will first need to configure an IIS Web Site to install it. After having configured the website you can simply unzip the content of the **Web** archive in the publish directory and proceed to modify the Web.config file to suit your needs. 

The most important parameters to configure are:

DataContext 
  The connection string to the database. Change it to point where you created the database
activeDirectory
  Activates active directory authentication instead of the standard form authentication. 
adDomain
  If you choose to authenticate with active directory this must be set to the Active Directory Domain you users will belong to

Agent
----------

The last part of the system is the **Agent** which will have to be installed on every machine where you will deploy your apps. Its role is simple: it will listen for commands from the controller and execute them to complete the deploys.

.. Note:: You may want first to discuss with your system administrator under what account the Agent will run. As it will need to execute scrips and access specific directories he may want to taylor the necessari permission with dedicated accounts

To install an Agent on a machine the first thing to do is reserve the 9000 port which it will use to listen for commands from the controller. This can be done with the  `netsh command <https://msdn.microsoft.com/it-it/library/windows/desktop/cc307223.aspx>`_.

Once reserved the port the service can be installed in the same way the **Controller** was installed




