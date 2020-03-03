.. _stage_script:

----------------------
Staging a cluster
----------------------

*Estimated time to complete:* **5 Minutes preparation** *and* **120 minutes run time**

Overview
++++++++

Now that you know your way a bit in the PRISM interface, let's stage the cluster using a script. This script can be used during Bootcamps Hands-on Labs. This module will use the staging script that the Technical Enablement team has created and maintains. The purpose of the script is to configure and setup the cluster to a well known stage. The script does install and configure the following:

For Prism Elements (PE):

#. Accept the EULA
#. Disable Pulse
#. Sets the email server and sends an example email
#. Installs and configures two networks
#. Delets the default RX Manager's installed network
#. Installs a Samba 4 Domain Controller
#. Registers the AD into the cluster so AD authentication can be used
#. Installs Prism Central on the Cluster
#. Installs a File server
#. Installs and configures File Analytics

For Prism Central (PC):

#. Sets the password to the same password as the PE password
#. Changes the background of PC
#. Registers the cluster in PC
#. Registers the AD into the PC for Domain Authentication
#. Sets the email server and sends an example email
#. Enables the following services:

     #) Calm
     #) Karbon
     #) Objects
     #) Flow

#. Runs LCM so the latest versions are running for

     #) Calm
     #) Karbon
     #) Objects

#. Configures Calm projects
#. Upload of blueprints in Calm

     #) Citrix Infra
     #) Era
     #) Karbon
     #) CI/CD

#. Runs blueprints

     #) Citrix Infra
     #) Era blueprint
     #) Karbon blueprint

#. Creates an extra virtual PC for PRISM Pro / X-Play workshops
#. Uploads needed images
   

Usage of the script
-------------------

The script can be run in two ways.

#. Use the script from the CVM (low amount of clusters to deploy)
#. Run the script from a local Linux/MAC machine (mass deployment or low amount of clusters)
   
This module will show the steps for each of the two possibilities. The last one is being used during the Tech Summit for example, or a bigger installation where the deployment is run from a centralised machine that deploys the clusters.

From CVM
--------

Follow these steps to run the staging script from within on of the CVMs in your cluster.

#. Use any terminal or emulator to login as the user ``nutanix`` to your cluster over the ``ssh`` protocol using the VIP of the cluster. This is normally for a 3 or 4 node HPOC cluster the **.37** address. The password is mentioned in your reservation email unless you have defined it yourself during the reservation of your cluster. Example ``ssh nutanxi@10.38.11.71``.
   
	.. figure:: images/01.png

	.. note::

   		To be 100% sure you are in the CVM make sure you see the text **Nutanix Controller VM** as shown in the red box in the picture.

#. After you've logged into the CVM, run the following command to start the staging script 
   
   .. code-block:: bash

   		curl --remote-name --location https://raw.githubusercontent.com/nutanixworkshops/stageworkshop/master/bootstrap.sh && sh ${_##*/}


#. This command will trigger the CVM to pull content from a github repository and start the process.
#. Fill out the required fields

     #) admin user name
     #) password (twice)
     #) person who should recieve the example email
     #) which workshop to be run
        
#. As we are running on a SNC we have to select option 2 or 4. Option 4 will be an older version of the script. So we choose option 2
   
   .. figure:: images/02.png

#. For the last question; if you type a "Y" the script will start and the only way back is re-image (using RX Manager) your cluster.
#. You will be prompted with some information on how to follow the process...
#. In the SSH session use the command ``tail -f snc_bootcamp.log`` to follow the progress of the script.

	.. figure:: images/03.png

#. The progress can also be followed in the Prism interface.
   
   .. figure:: images/04.png

   .. note::

   		If you are using Chrome on Mac OS Catalina, use the ``thisunsafe`` method as described in theis article: https://miguelpiedrafita.com/chrome-thisisunsafe/

#. After approx. 20-25 minutes you shoule receive a test email from the PC installaiton script. Also in the tail screen there will be a line showing something like 
   
	.. code-block:: bash

   		Remote asynchroneous launch PC configuration script... EMAIL=USERNAME@nutanix.com     PC_HOST=IP-ADDRESS_PC PE_HOST=IP-ADDRESS_PC PE_PASSWORD=PE_PASSWORD     PC_LAUNCH=snc_bootcamp.sh PC_VERSION=5.11.2 nohup bash /home/nutanix/snc_bootcamp.sh PC
   
   This means that the installation on the PC has started.
#. Disconnect from the CVM and connect to the IP address mentioned for the PC using ``ssh``. The IP Address is mentioned in ``PC_HOST``.
#. Use the command ``ssh nutanix@<PC_HOST_IP_ADDRESS>`` to connect to the PC CVM. 

	.. note::
		For the password use **nutanix/4u**. Not your defined/given password!

#. Use ``tail -f snc_bootcamp.log`` to follow the progress of the PC installation/configuration.

	.. figure:: images/05.png

#. The installtion and configuration of the PC can take up to **60 minutes**!
#. The progress can also followed using the PC UI. Login to the UI using the **admin** username and the earlier set **password**. Then go to the **Tasks** view as shown below in the screenshot.

     .. figure:: images/06.png

#. The last part is uploading images. All images are pulled from a local Distributed Files Share parrallel to each other, it will take up to **90 minutes** to get all images in the PC environment.
#. When you see a line mentioning 
   
   .. code:: bash

   		|finish|/home/nutanix/snc_bootcamp.sh ran for 3475 seconds._____________________`` 

   the script is ready. Just remember that images are still being pulled into the PC environment by that time. 

	.. figure:: images/07.png

#. Log out of your PC
#. Your environment is ready to be used.

------

Mass deployment
---------------

When you have more then one cluster to be deployed, like during an event of some sorts, going from CVM to CVM isn't the easiest way of deploying the clusters. For that purpose a stage_workshop script has been created to help in those situations. This script is a centralized way of deploying the staging script from a centralized location to multiple clusters.

Follow these steps to get the script to deploy your clusters.

.. note::
	
	To have the script running from your MAC/Linux machine it maust have git installed. Based on your O/S use the correct way of installing it.

#. On a MAC/Linux machine, open a terminal window and create a directory in a location of your choice. Example ``GitHub``
#. Change to the just created location. Example: ``cd GitHub``
#. Run the following command to clone the github repo for the staging script

	.. code:: bash

		git clone https://github.com/nutanixworkshops/stageworkshop


	.. note::

		If you cloned the script earlier, please use the command ``git fetch --all`` to get the latest version on your machine ``before`` proceeding. This way you'll have the latest versions of the script!

#. After the clone has finished, create a file that holds the following parameters:

     #) IP Address of the to be deployed cluster
     #) admin password
     #) email address

   The parameters must be seperated by a "|" pipe symbol. Example looks like:

	.. code:: bash

		10.10.10.37|PASSWORD|username@nutanix.com

#. Save the file.
#. Run the command ``./stage_workshop.sh`` to run an interactive session of the script. It will ask for a file that holds the parameters for the cluster that needs to be deployed.

	.. figure:: images/08.png

#. Provide the name of file that you just created
#. Provide the number of the workshop for the cluster(s) that you want to have deployed.
   
   .. note::

   		If you have selected a none SNC cluster deployment, the script will fail during the installation of PC and registration of the cluster in PC. This is due to network changes that need to be made. The network subnets are different in a "normal" cluster vs. a SNC!!!

#. As with the earlier discussed "CMV" deployment, answering the last question with "Y" will start the dployment to the clusters in the file created earlier! Only a foundation (RX Manager Re-Image) will "reset" the cluster.
#. The script will then do a few things to each cluster in the parameters file.

     #) Copies the needed file to the cluster using ssh to the provided ip address
     #) Start a remote ssh session using the provided pasword from the file
     #) Start on the cluster the script to install/config PE and PC. Emails will be sedn to the provide email address in the file.
     #) Shows in the terminal interface how to connect to the cluster and follow the deployment process as described earlier.
     #) Repeat for the next cluster if there are any left from the file.

#. The script will return to the default prompt on your machine.
   
   .. note::

		There is **no centralized** progress monitor. If you want to know the progress of the script per cluster, you have to look for emails that are being sent from the clusters or follow them one by one.

#. To start the script using the earlier created file of clusters and you know the workshopnumber use the following command to run the mass deployment:
   
   .. code:: bash

   		cd GitHub/stage_workshop
   		./staging_workshop.sh -f cluster.txt -w 2

   Where the ``-f cluster.txt`` stands for: use the file (-f) that holds the parameters and ``-w 2`` stands for: use workshop number (-w) 2 (as in number two from the workshops). 

   .. note::

   		If you don't know the number of the workshops, but have the file created, you can use just the -f parameter. The workshop will then be asked interactively.


------

Take aways:
-----------

As the way of installation is always pulling the last version of the script, any updates to the logics and/or options are always used.

#. Easy installation per CVM
#. Follow the progress of the PE and PC installation/configuration via a SSH session
#. Easy mass deployment of multiple clusters
#. Use parameters to run a mass deployment without going through a interactive session of teh script
#. 