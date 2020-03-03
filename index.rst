.. title:: Nutanix NHT SE Hands-On Lab 

.. toctree::
  :maxdepth: 2
  :caption: Day 1 - Basic Labs
  :name: _labs1
  :hidden:

  rx/rx
  nutanix101/nutanix101
  ncc-ui/ncc-ui
  ncc-cmdl/ncc-cmdl
  stage_script/stage_script
 


.. toctree::
  :maxdepth: 2
  :caption: Day 2 - Labs of Choice
  :name: _labs2
  :hidden:

  files/files
  calm/calm
  flow/flow
  era/era
  karbon/karbon

.. toctree::
  :maxdepth: 2
  :caption: Appendix
  :name: _labsA
  :hidden:

  tools_vms/linux_tools_vm
  tools_vms/windows_tools_vm
  taskman/taskman


.. _getting_started:

-------------------------
SE NHT Hands-on Lab (HoL)
-------------------------


Welcome to Nutanix New Hire Training! Carefully review the **Overview** section of each lab before proceeding with the exercise.

.. note::
  Shown screenshots are there for example purposes! Use **your** information!

This workshop is for having a combined Hands-on on RX manager, HPOC and how to setup the reserved SNC using the staging script build by the Technical Enablement department. Almost all steps are also valid for a four/three node cluster reservation in the HPOC environment.

Requirements
------------

To run this workshop a few items need to be ready. These items are:

1. Running VPN
2. Login credentials for Okta
3. Approx 60 minutes effective time to run the first day's workshop. 45 Minutes waiting for the RX environment to provide the HPOC system. 


Remarks
-------

1. This workshop is using a Single Node Cluster (SNC) on the HPOC environment.
. The second day HoLs are fully optional.

.. _cluster_details:

Cluster Access
--------------

As you will be reserving a SNC yourself, cluster assignments can not be provided at this time.

The Nutanix Hosted Proof of Concept (HPOC) environment can only be accessed via VPN or by connecting to the **Nutanix Corporate** network.

GlobalProtect VPN Access
........................

Browse to https://gp.nutanix.com.

Log in with your OKTA credentials.

Download and install the appropriate GlobalProtect agent for your operating system.

Launch GlobalProtect and configure **gp.nutanix.com** as the **Portal** address.