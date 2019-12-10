# B3_Cloud_Azure
Technical documentation for Azure Deployment

## Summary
- Preconditions
- Azure Deploiment by **Template**
- Azure Deploiment by **Container**
- Azure Deploiment by **Services**

# Preconditions
Create a free Azure account to get free credits.
![Creating free Azure account](https://github.com/xNero321/B3_Cloud_Azure.git/assets/prerequis/create_free)

Go to the main page and create a **Ressource Group**.

**Complete** this ressource group with a name (for the *region*, we will always use **Western Europe** because some services are not available according to the regions).

Create an **App Service Plan**.

**Complete it** with the Ressource Group and a name and then **Deploy** it.

# Azure Deploiment by Template
Create a **New Resource**.

Search for **WordPress** and click on **Create**.

**Complete** it with a name, your App Service Plan and the type of Database.

**Re-use** your App Service Plan or Create a new one (make sure you're using the **F1 free** *tariff level*).

**Create** the MySQL Database with a name, a username, and a password.

Go to ***YourWordpressName*.azurewebsites.net** and it should be working!

Don't forget to **delete the MySQL Database** in order to keep your credits!

# Azure deploiment by Container

# Azure deploiment by Services
