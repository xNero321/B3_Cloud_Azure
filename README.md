# B3_Cloud_Azure
Technical documentation for Azure Deployment

## Summary
### Part 1: Azure deploiment
- Preconditions
- Azure Deploiment by **Template**
- Azure Deploiment by **Container**
- Azure Deploiment by **Services**
  - Using **SQL Database**
  - Using **MySQL Database**
  - **Connect** WordPress and the Database
### Part 2: VM creation

# Part 1: Azure deploiment
## Preconditions
[Download](https://fr.wordpress.org/download/) a WordPress archive.

Create a free Azure account to get free credits.

![Creating free Azure account](/assets/prerequis/create_free.jpg)

Go to the main page and create a **Ressource Group**.

![Creating ressource group](/assets/prerequis/2-Creer_groupe_ressource.PNG)

**Complete** this ressource group with a name (for the *region*, we will always use **Western Europe** because some services are not available according to the regions).

![Completing ressource group](/assets/prerequis/4-completer_groupe_ressource.PNG)

Create an **App Service Plan**.

![Creating App Service Plan](/assets/prerequis/6-creer_plan_app_service.PNG)

**Complete it** with the Ressource Group and a name and then **Deploy** it.

![Completing App Service Plan](/assets/prerequis/7-completer_plan_1.PNG)
![Completing App Service Plan2](/assets/prerequis/7-completer_plan_2.PNG)

## Azure Deploiment by Template
Create a **New Resource**.

![Creating new resource](/assets/WPwTemplate/1-creer.PNG)

Search for **WordPress** and click on **Create**.

![Search WordPress](/assets/WPwTemplate/2-chercher.PNG)
![Create WordPress](/assets/WPwTemplate/3-cliquer_creer.PNG)

**Complete** it with a name, your App Service Plan and the type of Database.

![Completing WP1](/assets/WPwTemplate/4-remplir_1.PNG)

**Re-use** your App Service Plan or Create a new one (make sure you're using the **F1 free** *tariff level*).

![Completing WP2](/assets/WPwTemplate/5-remplir_2.PNG)

**Create** the MySQL Database with a name, the admin user informations and a password.

![Completing WP3](/assets/WPwTemplate/5-remplir_3.PNG)

Go to ***YourWordpressName*.azurewebsites.net** and it should be working!

![Working](/assets/prerequis/21-izoké.PNG)
![Working2](/assets/prerequis/21-izoké_2.PNG)

Don't forget to **delete the MySQL Database** in order to keep your credits!

## Azure deploiment by Container

Create a ressource called **Container service**

![Create App service](/assets/WPwDocker/Create.PNG)

Then fill the master configuration field:

- Orchestrator (Swarm)
- DNS
- Username
- SSH public key

![Create App service](/assets/WPwDocker/Config.png)

After finishing theese steps you should have a overall info page

![Create App service](/assets/WPwDocker/Done.png)

It should take approximately 10 minutes for the VM to be up and running. When it's done you should see in your ressources Azure page a Swarm master cluster.

![Create App service](/assets/WPwDocker/Ressource_list.png)

There to connect via SSH on the master node, you'll need to retrieve the public IP address and the DNS.

![Create App service](/assets/WPwDocker/swarm_cfg.png)

Launch PuTTY and paste the DNS name on the clipboard into the Host Name (or IP address) box. Set the port number to 2200.

Click the Save button to save these settings under that name.
Why port 2200 instead of port 22, which is the default for SSH? Because the load balancer you're connecting to listens on port 2200 and forwards the SSH messages it receives to port 22 on the master VM.

![Create App service](/assets/WPwDocker/putty_cfg.png)

In the treeview on the left, click the + sign next to SSH, and then click Auth. Click the Browse button and select the private-key file.

![Create App service](/assets/WPwDocker/SSH_auth.png)

Select Tunnels in the treeview. Then set Source port to 22375 and Destination to 127.0.0.1:2375, and click the Add button.

The purpose of this is to forward traffic transmitted through port 22375 on the local machine (that's the port used by the docker command you will be using shortly) to port 2375 at the other end. Docker Swarm listens on port 2375.

![Create App service](/assets/WPwDocker/Tunnels.png)

An SSH window will open and prompt you to log in. Enter the user name ("dockeruser") Step 2. Then press the Enter key. Once connected, you'll see a screen that resembles the one below.

Observe that you didn't have to enter a password. That's because the connection was authenticated using the public/private key. Key pairs tend to be much more secure than passwords because they are cryptographically strong.

Since Docker-compose 3.0 is not supported, you must use a docker-compose or dockerfile below this version.

Once you have your dockerfile/Dockercompose file done you can run it on the VM.

## Azure deploiment by Services

Create an **App Service**

![Create App service](/assets/WPwBDD/10-creer_app_service.PNG)

**Complete** it with your Ressource Group, a name and your Plan App Service.

![Complete App service](/assets/WPwBDD/11-completer_app_services_1.PNG)
![Complete App service2](/assets/WPwBDD/11-completer_app_services_2.PNG)

In your App Service, look for the **Deploiment Center**. You will find all the information in order to connect to it by **FTP**.

![Logs ftp](/assets/WPwBDD/12-acces_logs_ftp.PNG)
![Logs ftp2](/assets/WPwBDD/12-acces_logs_ftp_2.PNG)

Using a FTP Client (I'm using FileZila), **copy** all the WordPress's files from the archive to the *wwwroot* folder of your App Service.

![copy ftp](/assets/WPwBDD/13-copie_fichiers_ftp.PNG)

Go to ***YourAppServiceName*.azurewebsites.net**. WordPress is working but it need a Database.

![Working without db](/assets/WPwBDD/14-test_sans_db.PNG)

### Using SQL Database

Create a **SQL Database**

![creating sql db](/assets/WPwBDD/viaSQL/15-creerSQL.PNG)

**Complete** it with your Ressource Group and a name.

![completing sql db](/assets/WPwBDD/viaSQL/16-completer_sql.PNG)

**Create** a server with a name and the admin user informations.

![completing sql db2](/assets/WPwBDD/viaSQL/16-completer_sql_2.PNG)

![completing sql db3](/assets/WPwBDD/viaSQL/16-completer_sql_3.PNG)

Your SQL Database is ready.

### Using MySQL Database

Create a **Azure server for MySQL database**

![creating mysql db](/assets/WPwBDD/viaMySQL/15-cration_mysql.PNG)

**Complete** it with your ressource group, a name, the admin user informations and the server configuration (it's the server configuration that will be the most expensive).

![completing mysql db](/assets/WPwBDD/viaMySQL/16-completer_mysql_1.PNG)

![completing mysql db2](/assets/WPwBDD/viaMySQL/16-completer_mysql_2.PNG)

Look for *security of the connection* in the control panel of the Azure server for MySQL database and clikc on **add a client IP address**. This will allow your PC to connect to the Database. Then, **add a new rule** with the IP address of your Database (I created a rule allowing all connections since it is only a tutorial).

![config mysql db](/assets/WPwBDD/viaMySQL/16-config_ip_mysql.PNG)

Use MySQL Workbench to **connect to your database**. You'll find all the informations of conexion into the *properties* section of the control panel of the Azure server for MySQL database. Once you're connected, **create** a new diagram.

![log mysql db](/assets/WPwBDD/viaMySQL/18-trouver_connexion_1.PNG)

![log mysql db2](/assets/WPwBDD/viaMySQL/18-trouver_connexion_2.PNG)

![create diagram mysql db2](/assets/WPwBDD/viaMySQL/19-creer_schema.PNG)

Your MySQL Database is ready.

## Connect WordPress and the Database

Return to ***YourAppServiceName*.azurewebsites.net** and complete the informations of your Database.

![connect db](/assets/WPwBDD/20-lier_bdd.PNG)

That's it, your WordPress is running!

![Working](/assets/prerequis/21-izoké.PNG)
![Working2](/assets/prerequis/21-izoké_2.PNG)

# Part 2: VM creation

## What is the difference between a creation of VM Classique or with Resource manager?
Classic -> we have to configure everything
Resource Manager -> Possibility of having a pre-defined configuration

## Are the VM profiles identical according to the location chosen (describe the possibilities for the two types of VM provisioning: Classic and Resource Manager)?
No, in some cases only the price changes, in others we cannot create a vm, no profile is available (ex: France). Other cases: United Arab Emirates: your subscription does not take the creation of a vm.

## In the context of the lab, define what is the least expensive profile?
B1ls 6.15 usa east

## What are the constraints in the choice of geographic location?
The farther the data center, the more travel and therefore the possible latency

## What is the purpose of the VMS disk storage account?
Can store different types of files: blobs, tables, queues, files...

## Replication, LRS / GRS / RA-GRS: describe the differences
Locally redundant storage (LRS): three replicates in the same place
Geo-redundant storage (GRS): replication hundreds of kilometers away
Geo-redundant storage with read access (RA-GRS): replication at hundreds of kilometers + remote read access

## By changing replication, is there a difference in cost?

## Cloud service: what is the use of the Cloud service?

## Virtual network: why two networks (virtual network and subnet)?
One is used for inter-VM communication and the other for communication with the internet

## Endpoints (NSG): describe in detail the purpose and operation of NSG
Network Security Group:
Contains the number of rules desired. Each rule includes:
Last name
Priority: between 100 and 4096, processed in ascending order
Source or destination: all, IP address, CIDR ...
Protocol: TCP, UDP, ICMP ...
Direction: enter or exit
Action: Allow or deny

## Activate during the creation of the VM the startup and operating system diagnostics, then describe their usefulness
Lets find out why a VM enters a non-bootable state thanks to console outputs or screenshots.

## Diagnostic storage account: what is it for?
It stores diagnostic logs in a blob container named $ logs

## Decline and describe the 3 VM availability options

## What type of virtual machine generation to choose currently in Azure?
2nd generation VMs.

## Describe the use of labels when creating a VM

## How to connect a VM?

## How to configure a static IP on a VM?
With Azure PowerShell:
Stop-AzureVM -Name [VM_Name]
$VM = Get-AzureVM -ServiceName [VM_ServiceName] -Name [VM_Name]
Set-AzureStaticVNetIP -VM $VM -IPAddress [IP_Address] | Update-AzureVM

## In the VM, can we configure the network (check the config with ipconfig)?

## Is it possible to create an image of the VM and generalize it (Sysprep)?
https://docs.microsoft.com/fr-fr/azure/virtual-machines/windows/capture-image-resource

## Test and describe the takeover of the VM (IAM) from Azure AD users
Go to "All services", "Subscriptions", "Access control (IAM)", "Check access" and there you can manage the Azure users who have the right to modify your VMs.

## How do I add a data disk to a VM? Why not use the already existing disc?
https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/virtual-machines/windows/attach-managed-disk-portal.md

## Describe the different types of disk sources
Data disk: Store application data or other data that you need to keep.
Operating system disk: contains the boot volume.
Temporary disk: short-term storage for applications and processes, and is intended to store only data such as paging or swap files.

## How to set up the HA of a VM?
https://docs.microsoft.com/en-us/azure/virtual-machines/windows/tutorial-availability-sets
