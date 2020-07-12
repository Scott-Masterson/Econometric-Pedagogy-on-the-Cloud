# Econometric-Pedagogy
 Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists
 
 Authors: Danielle V. Handel, Anson T. Y. Ho, Kim P. Huynh, David T. Jacho-Chávez, Carson H. Rea

<br>

_________________________________________________________________________________________________________

<img align="right"
     src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/workflow_3.png" 
     width="600" height="460" />

### Table of Contents
1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Launching an Instance via AWS](#lauching-an-instance-via-aws)
4. [Anaconda](#anaconda)
   1. [Loading Anaconda](#loading-anaconda)
   2. [JupyterHub](#jupyterhub)
5. [R](#r)
   1. [Adding R](#adding-r)
   2. [Update and Install R Kernel](#update-and-install-r-kernel)
6. [Stata](#stata)
   1. [Adding Stata](#adding-stata)
7. [Disclaimer](#disclaimer)

## Overview 

<br>

The following instructions document a step-by-step guide to setting up a virtual “Econometrics Lab” hosted entirely in the cloud. Ultimately, students will be able to connect to the Lab with a username and password and have access to the distribution Anaconda for use of JupyterLab and Jupyter Notebooks with Python, R, and Stata kernels. 
A Professor would be able to post any form of assignment for their students to be completed on the instance using the tools provided. A group video chat service provider such as MS teams or Google hangout can be used alongside for synchronous instruction.

The following instructions are guidelines used to successfully set up the service documented above, although they can be modified for any particular teaching style or need.

The guide below corresponds to Workflow 3 outlined in “Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists” which may be referred to for further details. 


## Prerequisites
<details>
  <summary>Click to expand</summary>

<br>
 
The guide assumes that the following steps have already been adhered to:

* An up-to-date personal computer is available for use.
* A classroom was created in AWS Educate.
* Stata or the department’s IT services were contacted for the proper Stata licensing.  

[Back to Top](#econometric-pedagogy)
 
</details>

## Launching an Instance via AWS <a name="lauching-an-instance-via-aws"></a>
<details>
  <summary>Click to expand</summary>

  <br>

|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/1_nav_to_console_.gif" width="800" height="370" />|
|---|

  Log into your AWS Educate account. The "My Classrooms" tab on the top banner in the interface directs to the complete list of classrooms supported on the account. From there,   select the desired classroom by clicking the blue "Go to classroom" button. The third party, Vocareum, will launch, allowing the management of the classroom. To launch an      instance, select "AWS console". TO launch the instance, select EC2 from the list of services AWS provides. 

  <br>
  
|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/2_start_instance.gif" width="800" height="370" />|
|---|

  Launching an instance supported by EC2 is a seven step process. Follow the following instructions to ensure the instance has the maximum security and memory for the free teir   offered by AWS. 

  First, select an Ubunto server as the desired Amazon Machine Image (AMI). 20.4 was selected in this demonstration, although any can be selcted, given Ubunto is the AMI. 

  The next tab requests an instance type to be selected. The "general purpose" option will be preselected and be elgible for AWS's free tier. Click "Next: Configure Image" to   continue.
 
  Immediately continue to "Next: Add Storage".

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/3_security_group.gif"  width="800" height="370" />|
|---|
  
  Change the storage from the default to the maximum the free tier provides, 30 GiB. Continue to “Next: Add Tags”.

Tags are an optional feature to allow for categorization and organization. Continue to "Next: Configure Security Groups".

The SSH rule there by default will have the standard Port Range of 22 and a “Custom” source. Change the source to “Anywhere” Add a second custom TCP security rule by clicking the “Add Rule” button. Modify the rule to have a port range of 8000; notice the source change to “Custom” from “Anywhere”. Add a description of “JupyterHub”. Continue to the final stage by clicking the blue “Review and Launch” button. 

Given all steps have been followed by this point, select “Launch”.

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/5_launch_and_key.gif"  width="800" height="370" />|
|---|
  
  Selecting “Launch” will prompt the user to select an existing key pair or create a new one. A key pair serves as a sort of password to connect the instance to a SSH server or client. Name and download your key pair. 

:warning: Do not lose the key, or all progress will be lost. Keep track of where the key is stored, as it will need to be accessed later. :warning:

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/4_IP_into_bitvise.gif"  width="800" height="370" />|
|---|

The instance should now be visible in the EC2 homepage. Located towards the bottom of the screen, the description of the instance should be visible. Download and open Bitvise as an SSH client. Copy the IPv4 Public IP address and paste it into “Host” on Bitvise. Insert 22 as the port. 

:bulb: MacOS users may choose to use the Terminus App off of the AppStore in lieu of Bitvise.

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/6_put in key.gif"  width="800" height="370" />|
|---|
  
  The proper username to connect Bitvise to the instance is “ubuntu”. Change the following line “Initial method” to Publickey. Select the proper key in from the newly created “client key” line. Click log in to selct the key downloaded earlier. An optional comment can be left for organization purposes if desired.

The instance is now launched and hosted on a client. 
Continue reading the “Anaconda” section to download the distribution onto the newly created instance. 

[Back to Top](#econometric-pedagogy)
  
</details>

## Anaconda
<details>
  <summary>Click to expand</summary>

  
  #### Loading Anaconda <a name="loading-anaconda"></a>
  
  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  To request root access:
  
  ```console
  ubuntu@ip-xx-xxx:~$ sudo -i
  ```
  After launching an instance with your selected cloud service provider, update the Ubuntu repository and upgrade packages by:
  
  ```console
  ubuntu@ip-xx-xxx:~$ apt-get update
  ubuntu@ip-xx-xxx:~$ apt-get upgrade
  ```
  To install Anaconda:
  ```console
  ubuntu@ip-xx-xxx:~$ wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
  ubuntu@ip-xx-xxx:~$ bash Anaconda3-2020.02-Linux-x86_64.sh
  ```
  When prompted with
  ```console
  [/root/anaconda3] >>>
  ```
  enter `/usr/anaconda3`.
 
  ```console
  ubuntu@ip-xx-xxx:~$ source .bashrc
 
  #Open a text editor (nano is used here):
  ubuntu@ip-xx-xxx:~$ nano /etc/profile
  
  #enter the following:
  export PATH="/usr/anaconda3/bin:$PATH"
  ```
  
  <br>
  
  #### JupyterHub: 
  
  ```console
  # Install jupyter hub 
  # https://jupyterhub.readthedocs.io/en/stable/quickstart.html

  # Update to the latest conda version
  ubuntu@ip-xx-xxx:~$ conda update -n root conda

  # Update all packages in the current environment to the latest version 
  ubuntu@ip-xx-xxx:~$ conda update --all
  ubuntu@ip-xx-xxx:~$ conda install -c conda-forge jupyterhub
  ```
  ```console
  # Create jupyter hub configuration file
  ubuntu@ip-xx-xxx:~$ mkdir /etc/jupyterhub/
  ubuntu@ip-xx-xxx:~$ cd /etc/jupyterhub/
  ubuntu@ip-xx-xxx:~$ jupyterhub --generate-config
  ubuntu@ip-xx-xxx:~$ nano jupyterhub_config.py
  
  # enter the following in the file:
  # open jupyter lab by default
  c.Spawner.default_url = '/lab'
  # allow admin to access other users' accounts 
  c.JupyterHub.admin_access = True
  # specify system user as administrator
  c.Authenticator.admin_users = {'admin'}
  # shutdown user servers on logout
  c.JupyterHub.shutdown_on_logout = True
  # prevent the user-owned configuration files from being loaded
  c.Spawner.disable_user_config = True
  
  ```
  ```console
  #
  ubuntu@ip-xx-xxx:~$ nano /etc/jupyterhub/jupyterhub.service
  
  #enter the following:
  [Unit]
  Description=JupyterHub
  After=syslog.target network.target

  [Service]
  User=root
  Environment="PATH=/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/usr/anaconda3/bin"
  ExecStart=/usr/anaconda3/bin/jupyterhub --no-ssl -f /etc/jupyterhub/jupyterhub_config.py

  [Install]
  WantedBy=multi-user.target
  
  ```
  Now, enable this:
  ```console
  ubuntu@ip-xx-xxx:~$ ln -s /etc/jupyterhub/jupyterhub.service /etc/systemd/system/jupyterhub.service

  ubuntu@ip-xx-xxx:~$ systemctl daemon-reload
  ubuntu@ip-xx-xxx:~$ systemctl enable jupyterhub.service
  ubuntu@ip-xx-xxx:~$ systemctl start jupyterhub.service
  ubuntu@ip-xx-xxx:~$ systemctl status jupyterhub.service
  ```
  
  [Back to Top](#econometric-pedagogy)
  
</details>

## R
<details>
  <summary>Click to expand</summary>
 
  
  #### Adding R <a name="adding-r"></a>
  Install R:
  ```console
  ubuntu@ip-xx-xxx:~$ apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
  ubuntu@ip-xx-xxx:~$ add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
  ubuntu@ip-xx-xxx:~$ apt update
  ubuntu@ip-xx-xxx:~$ apt install r-base r-base-dev
  
  #Start R
  ubuntu@ip-xx-xxx:~$ R
  ```
  
  <br>
  
  #### Update and Install R Kernel <a name="update-and-install-r-kernel"></a>
  ```r
  
  # update, without prompts for permission/clarification
  update.packages(ask = FALSE)
  install.packages('IRkernel', lib = '/usr/local/lib/R/site-library')
  
  #Make Jupyter see the newly installed R kernel by installing a kernel spec.
  #For system-wide installation, set user to False in the installspec command:

  IRkernel::installspec(user = FALSE)

  # Additional Ubuntu linux packages are needed for 'tidyverse' in R
  apt install libcurl4-openssl-dev libssl-dev libxml2-dev

  # Install tidyverse for all users
  install.packages("tidyverse", dependencies = TRUE, INSTALL_opts = '--no-lock')

  # Examples of other packages
  install.packages("openxlsx", lib = '/usr/local/lib/R/site-library', dependencies = TRUE, INSTALL_opts = '--no-lock')
  install.packages("knitr", lib = '/usr/local/lib/R/site-library', dependencies = TRUE, INSTALL_opts = '--no-lock')
  
  #When ready, quit
  q()
  ```
  
  [Back to Top](#econometric-pedagogy)

</details>

## Stata
<details>
  <summary>Click to expand</summary>
 
 <br>
 
 :bulb: Instructors should contact Stata to discuss the best licencing options. A Stata Labs licences may be best for this particular workflow, with the lab size corresponding to the number of students in the lab.
  
  #### Adding Stata <a name="adding-stata"></a>
  Download Stata for Linux from https://www.stata.com/support/faqs/unix/install-download-on-linux/
  Download Stata kernel for Jupyter Notebook from https://kylebarron.dev/stata_kernel/
  
  
  
  [Back to Top](#econometric-pedagogy)
  
</details>

## Disclaimer 
<details>
  <summary>Click to expand</summary>
 
   <br>
 
The instructional guide is part of a demonstration used for “Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists”. There is no guarantee this methodology works for others. For personal help, independently research any specific needs. 

AWS Educate and corresponding services are trademark of Amazon Web Services.

Stata is trademark of Stata Corporation.

Look into: Python, R, Jupyter Hub for open source citation. 

[Back to Top](#econometric-pedagogy)
  
</details>

