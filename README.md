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

# Azure deploiment by Container

# Azure deploiment by Services

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

## Using SQL Database

Create a **SQL Database**

![creating sql db](/assets/WPwBDD/viaSQL/15-creerSQL.PNG)

**Complete** it with your Ressource Group and a name.

![completing sql db](/assets/WPwBDD/viaSQL/16-completer_sql.PNG)

**Create** a server with a name and the admin user informations.

![completing sql db2](/assets/WPwBDD/viaSQL/16-completer_sql_2.PNG)

![completing sql db3](/assets/WPwBDD/viaSQL/16-completer_sql_3.PNG)

Your SQL Database is ready.

## Using MySQL Database

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
