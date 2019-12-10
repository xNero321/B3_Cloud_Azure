# B3_Cloud_Azure
Technical documentation for Azure Deployment

## Summary
- Preconditions
- Azure Deploiment by **Template**
- Azure Deploiment by **Container**
- Azure Deploiment by **Services**
  - Using **SQL Database**
  - Using **MySQL Database**
  - **Connect** WordPress and the Database

# Preconditions
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

# Azure Deploiment by Template
Create a **New Resource**.

Search for **WordPress** and click on **Create**.

**Complete** it with a name, your App Service Plan and the type of Database.

**Re-use** your App Service Plan or Create a new one (make sure you're using the **F1 free** *tariff level*).

**Create** the MySQL Database with a name, the admin user informations and a password.

Go to ***YourWordpressName*.azurewebsites.net** and it should be working!

Don't forget to **delete the MySQL Database** in order to keep your credits!

# Azure deploiment by Container

# Azure deploiment by Services

Create an **App Service**

**Complete** it with your Ressource Group, a name and your Plan App Service.

In your App Service, look for the **Deploiment Center**. You will find all the information in order to connect to it by **FTP**.

Using a FTP Client (I'm using FileZila), **copy** all the WordPress's files from the archive to the *wwwroot* folder of your App Service.

Go to ***YourAppServiceName*.azurewebsites.net**. WordPress is working but it need a Database.

## Using SQL Database

Create a **SQL Database**

**Complete** it with your Ressource Group and a name.

**Create** a server with a name and the admin user informations.

Your SQL Database is ready.

## Using MySQL Database

Create a **Azure server for MySQL database**

**Complete** it with your ressource group, a name, the admin user informations and the server configuration (it's the server configuration that will be the most expensive).

Look for *security of the connection* in the control panel of the Azure server for MySQL database and clikc on **add a client IP address**. This will allow your PC to connect to the Database. Then, **add a new rule** with the IP address of your Database (I created a rule allowing all connections since it is only a tutorial).

Use MySQL Workbench to **connect to your database**. You'll find all the informations of conexion into the *properties* section of the control panel of the Azure server for MySQL database. Once you're connected, **create** a new diagram.

Your MySQL Database is ready.

## Connect WordPress and the Database

Return to ***YourAppServiceName*.azurewebsites.net** and complete the informations of your Database.

That's it, your WordPress is running!
