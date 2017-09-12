Deploy
===================================

Bazooka allows you to define your application deploy process by composing different tasks. Each task can be of a different type and have different options to allow you to customize your deploy.

Deploy task
---------------------------

The Deploy task is the most common task used in Bazooka. It will allow you to copy a nuget package in the specified directory to the specified machine (Agent).

This task will 

- copy the package in the specified golder on the target machine
- extract its contents
- search and apply an enviroment specific transform if present. (For example if we're deploying to the Test enviroment and a web.Test.config file is present il will be considered and XDT transform and applied to the web.config file)
- if a file named Install.ps1 is found it will be executed  to complete the install

Note that if a package is already present it will first proceed to

- execute a Uninstall.ps1 script if found
- delete the existing package contents

before attempting to install the new version.

Mail task
---------------------------

The mail task is a task designed to send a mail to one or more recipients to warn them of a deploy. This task allows you to specify a mail Text, a sender, and one or more recipients separated by a semicolon. 

Local script task
---------------------------

The local script task is simply a way to make the Controller xecute a Powershell script. the only parameters are the name of the task and the script to execute. 

Remote script task
---------------------------

The remote script task is a variant of the local script task. In this case the script will be executed by a specific agent.

Database task
---------------------------

The last type of task is the **Database** task. This task will allow you to deploy a **dacpac** file contained in a package to a specified database. Once this task executes the specified package will be fetched, its contents will be searchd for a dacpac file then it will be applied to the specified database aligning its structure to the one specified in the dacpac file.


This task accepts the following parameters:

**Name**
  The name of the task
**ConnectionString**
  The connection string to the database to the deploy
**Package**
  The name of the package containing your dacpac file
**DatabaseName**
  The name of the database to deploy
**Agent**
  The agent which will execute the deploy. Note that this agent must have suitable permissions to access and modify the database



Templated task
---------------------------

The most recent type of task added. By configuring a template for your task in the **Configuration** section or using one of the already defined ones you can specify the needed parameters to execute a task based on a task template.

You will have to specify the following parameters:

**Name**
  The name of the task
**Task**
  The task template to use
**Package**
  The name of the package containing your application
**Repository**
  The repository where the package can be found
**Agent**
  The agent which will execute the deploy.
  
Along with all the parameters specified by the task template


