.. Bazooka documentation master file, created by
   sphinx-quickstart on Tue Jan 10 23:28:36 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Introduction to Bazooka
===================================

This is the documentation site for the Bazooka deploy system. If you were searching for the `main site go here <http://bazookadeploy.github.io/Bazooka/>`_ while the source `can be found here <http://bazookadeploy.github.io/Bazooka/>`_

What is Bazooka?
----------------

Bazooka is an **Application Release Automation (ARA)** Tool, which helps you to deploy your applications in an automated, repeatable and reliable way managing all the error-prone steps usually done by a human.


Why Bazooka?
----------------

Manually deploying an application is a complex and error-prone multi-step process:

1. Getting all your application source files
2. Building the application with your build system
3. Copying the build output to the desired server/network share
4. Modifying the configuration files for the enviroment, changing connection strings and other parameters,
4. Executing all other needed steps such as configuring site options, updating the database, …


As you can see there are multiple steps and each one is subject to error:

1. You may forget to update your local source code copy with the latest changes from your VCS or you have locally some files which were not checked in, so the application you’re building is different from the one everyone else was testing
2. You may have subtle differences in your local configuration like a different compiler or may forget to run a part of the build, like javascript minification and concatenation
3. You may not have access to the folder used for publishing or the one who has is currently on vacation
4. Changing the configuration files manually for each enviroment has some risks like forgetting to change a connection string that now points to a database in another enviroment, or worse you don’t remember all the modifications to the configuration so you never touch the configs
5. You may forget to update the database with the new table or stored procedure you have just created or forget to restart the web server.

While points **3**, **4** and **5** may seem severe as your deployment is stopped or your application is throwing exceptions due to wrong application or system configurations point **1** and **2** are the real problem as the deployed application is now a snowflake that cannot be recreated for testing or rollback in case of emergency.

As you can easily see each of these steps introduce complexity in your deployment process and a risk of making an error, especially when tired or under pressure.

Now multiply these steps for maybe three or four enviroments (Test, UAT, Staging and Production) and for ten to twenty applications (not too many, for a mid-size business) and you have a problem on your hands not to mention all the time subtracted to other activities.

The only solution to this problem is to completely automate your application deployment, with the objective of being able to go from a version in your VCS to deploying your application without any manual intervention.

Bazooka was created for this precise situation, to be able to package an application and deploy it reliably and automatically across different enviroments without any manual intervention.


How does it work?
------------------

The idea behind how Bazooka works is really simple:

1. Package your application after it has been built by your build system in a format that allows versioning (as it turns out NuGet packages work very well for this)
2. When you want to deploy your application select the version you want to publish and let Bazooka deploy it according to the configured steps


.. toctree::
   :maxdepth: 2
   :caption: Contents:

   Installing
   Configuration
   Walktrough
