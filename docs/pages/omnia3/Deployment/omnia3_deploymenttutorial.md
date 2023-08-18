---
title: Platform Deployment Tutorial
keywords: omnia3
summary: "All you need to know about deploying our platform"
sidebar: omnia3_sidebar
permalink: omnia3_deploymenttutorial.html
folder: omnia3
---


## 1. Prerequisites

- Create a Linux server (Ubuntu 20.04 LTS), with an **omnia** user, who will be responsible for running the application.

    Ensure the firewall has its port 80 and 443 (HTTP and HTTPS) open to the exterior, so you will be able to access the application.

- Have a way to access the server and copy files to it. We suggest [MobaXTerm](https://mobaxterm.mobatek.net/){:target="\_blank"} if you are doing the setup from a Windows machine.

- Install .NET Core **3.1** SDK (current recommended version: SDK 3.1.201), by following the official Microsoft [instructions](https://docs.microsoft.com/en-us/dotnet/core/linux-prerequisites?tabs=netcore3x){:target="\_blank"}. Go to the Ubuntu section, and follow the instructions for your version of Ubuntu.

- Install NGINX on the server, by running ```sudo apt-get install nginx```.

- Obtain a version of the OMNIA binaries.

## 2. The binaries

For every version of the platform, two zip files are produced and distributed:
- ```OmniaPlatform.Full.<versionnumber>.zip```
    Contains a bin/ folder containing the binaries of the platform, a setup/ folder containing a series of files necessary for setup, and a database/ folder containing the database schema.
- ```OmniaPlatform.Binaries.<versionnumber>.zip```
    Contains only the contents of the bin/ folder. To be used in updates.

This tutorial assumes we are using the **Full** zip, extracted to a local folder in our machine.

## 3. Configuring the database
- Create a database with name **omnia**, with any username & password you want, in a PostgreSQL database server (version 14.5 or above supported).

    Ensure you can access the database server through the firewall, via a tool such as [pgAdmin](https://www.pgadmin.org/){:target="\_blank"}, so you can perform management operations, from the machine you are using.

    Also ensure you can access the database server through the firewall, from the server you are installing the platform on.

- Using a tool such as pgAdmin, execute the setup script in setup/database/dbschema.sql to set the database up.

## 4. Installation 

### 4.1. Copying the binaries & installer
- Copy all of the contents from the extracted zip over to the target machine, to the ```/home/omnia/``` folder (create it if it doesn't exist).

### 4.2. Installing the services
Execute the following commands on the target machine.

```
sudo cp /home/omnia/setup/services/*.service /etc/systemd/system/
sudo systemctl daemon-reload
cd /etc/systemd/system/
sudo systemctl enable omnia omnia-*
```

- The services will now be configured for launch.

## 5. Configuring the services

### 5.1. Configure OMNIA

- Edit /home/omnia/config/omnia.json, using `nano` or a similar tool, and fill in the following parameters:
    - ConnectionStrings > PostgreSQL: insert your database connection string, by replacing the parameters that are in ALLCAPS with your own information;
        _NOTE: If you are using an Azure database, remember to input your user in a compatible format, i.e. myusername@myservername_.
    - Hostname: Platform hostname, i.e. omnia.example.com;
    - IdentityServiceUrl: Platform hostname, prefixed with HTTP or HTTPS depending on what you are running, i.e. http://omnia.example.com/. See [this section](omnia3_deploymenttutorial.html#53-configure-https) for information on configuring HTTPS;
    - SMTP: A valid SMTP server configuration. **Essential** for the execution of Step 7;
    - (Optional) RedisConnectionString: A valid Redis connection string. In a format like `"redis-server.example.com:12345,password=abcdef"`. See [this section](omnia3_deploymenttutorial.html#54-configure-redis) for more information.

### 5.1.1 File storage

By default the platform uses the local file system as the file storage. In case you want to use the Azure Blob Storage or AWS S3, the platform can be configured to do that, just add one of the following statements to the config file.

**Azure Blob Storage:**
```
"FileStorage":{
	"Name": "AzureBlobStorage",
	"Arguments":{
		"ConnectionString":"AZURE_BLOB_CONNECTIONSTRING"
	}
  }
```

**AWS S3:**
```
"FileStorage":{
	"Name": "AWSS3",
	"Arguments":{
		"AccessKey":"KEY",
		"SecretKey":"SECRET KEY",
		"Region":"REGION",
		"BucketName":"BUCKET"
	}
  }
```

### 5.2. Configure NGINX
- Perform the following command to replace NGINX's default configurations with the ones we provide.
```
sudo cp /home/omnia/setup/nginx/* /etc/nginx/ -r
```

- Edit `/etc/nginx/sites-enabled/default`, using `sudo nano` or a similar tool, and replace the **server_name** parameter with the public hostname of your site.

### 5.3. Configure HTTPS

In the nginx site configuration (`/etc/nginx/sites-enabled/default`), there is a series of commented out lines. 

If you have a valid SSL certificate, follow the instructions in the file to set the site to run in HTTPS-by-default mode, which is **the only supported mode** of running the platform.

If you don't have a certificate, you can choose one of these alternatives:
- If you have a valid DNS name for your site that you own (i.e., not aws, azure, etc.) , you can set up **Let's Encrypt** for a free certificate. See [this DigitalOcean tutorial](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04){:target="\_blank"} for an example of setting it up.

- If you don't, you can use the platform via HTTP. This is **not supported** though, but it can be a solution for a quick trial.

Running the platform without an SSL certificate in production is **not supported,** as well not GDPR-compliant.

Remember to update the configuration in omnia.json! **IdentityServiceUrl** will need to point to the HTTPS version of the site.

### 5.4. Configure Redis

The platform has support for Redis, which is a necessity when deploying **multiple instances**. In order to use it, you only need to provide a connection string in the configuration file, as explained above.

To propertly support scaling out, ASP.NET Core SignalR **requires** the usage of **sticky sessions** in your load balancer. 

### 5.5. Secret Manager

See [this section](omnia3_secretmanager.html).

## 6. Starting the site
- Execute `sudo systemctl start omnia`, which will launch the OMNIA services. To obtain logs, you can check the logs folder `/var/log/omnia/`, or use `journalctl`.

- Execute `sudo service nginx reload`. Verify if the platform is running - it should now be possible to access the site, the swagger api (i.e. omnia.example.com/api/docs), and to perform the initial setup of the platform itself by providing an email.

## 7. Initial Setup
On a web browser, access the site with the defined url (i.e. omnia.example.com).

You will be asked for a platform administrator email. Insert a valid email address and a message will be sent with the instructions for the first login.

The site's configurations **must** contain a valid SMTP configuration, so that emails are sent.

When you receive the email, and perform a first login successfully, the platform is ready to use!

## 8. Logging and Telemetry

### Logging

The platform's logging level can be configured in the subscription configuration file.

Levels:
 - Debug
 - Information
 - Warning
 - Error

```JSON
  "Logging": {
	"Level": "Debug"
  }
```  

### Telemetry

Omnia Platform logs can be registered on Azure Application Insights.

The _AllowTelemetry_ parameter can be used to enable/disable this feature:

```JSON
  //possible values: true, false
  "AllowTelemetry": false
```

In order to view the logs on your Azure Application Insights account, the given Instrumentation Key must be configured on Omnia, as shown below:

```JSON
  //Instrumentation Key is a 32-char guid
  "ApplicationInsights": {
    "InstrumentationKey": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
  }
```
