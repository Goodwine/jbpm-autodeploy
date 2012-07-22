JBPM Automatic Deployer
=======================

This Ant will help you to deploy a group of JBPM processes without having to upload one by one.
The only requirements are: 
* Ant (preferably the latest one)
* A server that accepts PAR files.

Get your process directory ready
--------------------------------
Since I've been working with JBPM, whenever we create a process, we store each process in a
different directory, each one including a JPDL, a GPD, a JPG, and an optional metadata.xml

This project includes a `process-directory-example` folder, to be used as a reference when
getting your process directory ready.

Configure the processes path
----------------------------
There is a file in the root directory called `properties.properties`, update the
`process_directory` with the path to your folder with the processes.

### ie:
* `process_directory=~/projects/MyJBPMProject/processes`
* `process_directory=C:\\projects\\MyJBPMProject\\processes`

Choose which processes to deploy
--------------------------------
The property `process_name` lets you specify the name of a process to deploy, you can also add
wildcards to deploy several processes, and you can play with it to avoid deploying other
processes.
### ie:
* `process_name=*`
* `process_name=process*`
* `process_name=processA`

Configure the deployment tarjet
-------------------------------
This is quiet straight forward, open `properties.properties`, modify:
* `server=localhost` -- IP or domain of the server
* `port=8080` -- port...
* `deployer=/jbpm-console/upload` -- path to the service used to deploy PAR files.

How do I use it?
----------------
After configuring everything as stated above, run the ant in this directory. First navigate to
the path of your copy of jbpm-autodeploy, and run `$ ant install`

### Using it on eclipse
If you put JBPM AutoDeploy in Eclipse, you can do the following for the first time:
* Right Click `build.xml`
* Run As > Ant Build...
* Go to "Targets" Tab
* Enable "install" (ONLY install!!)
* Run

For the next time, you will be able to:
* Right Click `build.xml`
* Run

I already have a folder full of PAR files, What do?
---------------------------------------------------
Modify the property `deploy_directory` to the path of your PAR files, they will be uploaded
one by one, and run `$ ant deploy`

BE CAREFUL! Some deployers require the PAR's (zipped) files be named named exactly as:
`processdefinition.xml`, `gpd.xml`, `processimage.jpg`, and `metadata.xml`

What if I want to generate the PAR files without deploying them?
----------------------------------------------------------------
`$ ant build`

Libraries used
--------------
* `DeployProcessToServerTask` -- Thanks to [Kurt Stam @ Fresh Expresso](http://kurtstam.blogspot.com)
* [Ant Contrib](http://ant-contrib.sourceforge.net/)