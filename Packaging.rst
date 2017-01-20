Packaging
===================================

Bazooka works on a simple idea: if an application can be packaged with all his dependencies and configurations and versioned then that package can be used to deploy the application in various enviroments in a repeatable way.


Packaging format
---------------------------

To package the applications we had to choose a format. Ideally it should be:

- **versionable** as every package should be easily marked with a version number
- **easy to create and modify** with existing tools as you probably alreaady have a build or CI system and it should be easily to produce the packages from it
- **compact** as it will be necessary to store a good number of versions of the applications and we can't afford to waste too much space
- **easy to manipulate** with existing tool and libraries, as having prebuilt tools avoids having to create an entire ecosystem from scratch

The choice, given these principles, was easy: Nuget.

NuGet born as a format to distribute compiled dlls for the .NET ecosystem allows to package a set of files in a compressed archive and attach some metadata like version, owner, a link to the release info page. With the format have also been created a multitude of libraries and tools to create, manipulate and host Nuget packages allowing us to reuse all that work.

This choiche has been also made by many others with similar requirements like Chocolatey.

Packaging your application
---------------------------

A package should contain everything needed to deploy you application which means:

- all compiled binaries
- all static assets (css, javascript, view files)
- optionally an installation and uninstallation Powershell script (these can be included in the package or configured in the web application)
- configuration files and optionally config transforms for any enviroment (these can be included in the package or configured in the web application)

Creating a package
---------------------------

Creating a package is really straightforward and can be easily automated and included in an automated build. For each package to create (an application may consist of multiple packages, one for the web site, one for a windows service, …) it’s necessary to create a definition file, the **nuspec** file.

A **nuspec** file is simply an xml file with the nuspec extension that tells Nuget how to create the package. To begin you can simply take this as an example and modify it for your project:


.. code:: xml

<?xml version="1.0"?>
<package >
  <metadata>
    <id>MyAwesomeWebSite</id>
    <version>$version$</version>
    <owners>Awesome Inc</owners>
    <description>My Awesome Web Site</description>
  </metadata>
  <files>
    <file src="PATH\TO\FOLDER\**\*.*" target="" />
  </files>
</package>

To adapt this example to your specific case you have to modify:

**id tag**
  change the content of this tag to the name of the application contained in the package (no spaces or characters not allowed in URLS, this is a nuget convention)
**version tag**
  the $version$ syntax means that this is a placeholder that will be replaced when building. Better leave this here and specify it later
**owners tag**
  Specifies the owner of this package. It's only a description and can be omitted.
**description tag**
  A description of the package. It's only a description and can be omitted.
**files tag**
  This tag and all it's children specify what files will be added to the package. You can replacce PATH\TO\FOLDER with the path where all the applications file can be found but leave the trailing \\**\\*.* as that means that all the files will be recursively added.


Once you have created the nuspec file to create the package you just have to call the Nuget executable in this way

  nuget.exe pack YOURNUSPECFILE.nuspec -Properties "version=YOURPACKAGEVERSION"


replacing **YOURNUSPECFILE.nuspec** with the actual name of your nuspec file and **YOURPACKAGEVERSION** with the version of the package you want to build. This command will create a file with the nupkg extension in the current folder that contains all the applications file. If you want to inspect it you can simply change the extension to .zip and open it like a normal compressed archive.


Hosting your packages
---------------------------

Once you have packaged your application in a nuget package it is necessary to host them in a **repository**. A repository can be created in many ways

- you can simply use a shared folder even a network folder
- you can host a Nuget Gallery on your own  `server <https://docs.microsoft.com/it-it/nuget/hosting-packages/overview/>`_.
- you can use one of the services offering to host your NuGet feed


