#Build and Deploying WordPress to 14.4 to Distelli
WordPress is a full content management system with thousands of plugins, widgets, and themes.

Distelli is a DevOps continuous integration and continuous deployment tool.

On the Internet, there are numerous instructions describing installing Wordpress. But many of them often have a step that simply says; "Create a database for WordPress on your web server". Not everyone knows how to do this. Not everyone has a web server. Not everyone wants to learn how to install database software and create a new database and database user.

If you have an Internet connected server and want to get started using Wordpress, this article is for you. This takes advantage of Distelli's powerful deployment system to install and configure:
* Web Server (Nginx)
* Database Server (MySQL)
 - A database
 - A database user
 - A database user password
* WordPress
 - Database connection information
## Step 1. Create a Free Account on Distelli
In your web browser navigate to <a href="https://www.distelli.com/signup" target="_blank">https://www.distelli.com/signup</a> and sign-up for your free Distelli account.

![alt text](https://www.filepicker.io/api/file/G44t2S9LRUirfTpuiTtA)

###Step 2. Get the Deployment Instructions
The Distelli deployment instructions are in a distelli-manifest.yml file.  This file and an nginx configuration file are available in a distelli public GitHub repository here.

Fork this repository to your GitHub account.

### Step 3. Create the Application in Distelli
In Distelli click the **Applications** link at the top of the WebUI. Then click the **New App** button on the top right.

![alt text](https://www.filepicker.io/api/file/o2KKinKSNyP4xLyZi9AG)

Give your application a name. Use the name **distelli_wordpress**. This name has no bearing on your Wordpress site.
[block:callout]
{
  "type": "warning",
  "body": "The application name must match the application name in the distelli-manifest.yml file."
}
[/block]
After entering a name, click the **Use GitHub** button.
[block:callout]
{
  "type": "warning",
  "body": "If the button instead says **Connect GitHub** click that and connect your GitHub account."
}
[/block]
![alt text](https://www.filepicker.io/api/file/0ulLJit6TX63o3mJOAiM)

Select the repository you forked from [Step 2](#step-2-get-the-deployment-instructions) above.

![alt text](https://www.filepicker.io/api/file/oHaOt0BQQHi9azS99ilW)

Choose the **master** branch.

![alt text](https://www.filepicker.io/api/file/2h7kiV2TpK1CA7JfFGWq)

Two environment will be automatically created for you. Click the **All Done** button to continue.

![alt text](https://www.filepicker.io/api/file/XQjPWM7QbQbg13HC5aDQ)

At this point you will pause the *new application workflow* and edit the deployment instructions before continuing.

### Step 4. Edit the distelli-manifest.yml Instructions

You already have a distelli-manifest.yml file provided in the repository you forked earlier. You must edit this file and commit the edit to your repository.

Edit the distelli-manifest.yml file.

![alt text](https://www.filepicker.io/api/file/2Ow5jhi0RJWlZ4rCmm5O)

Set the values as appropriate:
* <SET_ME_DISTELLI_USERNAME> = This should be set to your Distelli username you created when you signed up. For more info see: [Finding Your Distelli Username](doc:finding-your-distelli-username).
* MYSQL_ROOT_PASSWORD: "<SET_ME>" = The root (master) password for the mysql database server.
* DB_NAME: "<SET_ME>" = The name of the Wordpress database you wish to create.
* DB_USER_NAME: "<SET_ME>" = The user that has full permissions to the Wordpress database.
* DB_USER_PASSWORD: "<SET_ME>" = The password for the Wordpress database user.

Leave all the other content in the file alone.

Note: distelli_wordpress is the name of the application. This must match the name you gave the application in Distelli.

Here is an example edited text.

```
johndoe/distelli_wordpress:
    - Env:
    # Set the variables below
    - MYSQL_ROOT_PASSWORD: \"pa55w0rd\"\
    - DB_NAME: \"wordpress_db\"
    - DB_USER_NAME: \"wordpress_user\"
    - DB_USER_PASSWORD: \"wordpress_user_password\"
```    
Save your changes.
Commit the changes to your repository.

### Step 5. Build the Application

Go back to the Distelli WebUI and click the **I've pushed my Repo** button.

Click the **Looks good. Start Build!** button.

![alt text](https://www.filepicker.io/api/file/3ulexcwqQ2KGbnaPvsqn)

The build that is kicked off will validate that you have the correct Distelli user name and your application name matches. After a successful build, a software release will be created. For more information on builds see [Viewing Builds](doc:viewing-builds).

If you are not on the builds list page, click the **Builds** button at the top of the Distelli WebUI.

Your successful build will be at the top of the list. 

Click the **New Deployment** button at the top right to begin a deployment

![alt text](https://www.filepicker.io/api/file/hwL33UtQSRWLMSJaH4pw)

### Step 6. Deploy the Application

In the new deployment wokflow step 1, click **Deploy a Release**.

![alt text](https://www.filepicker.io/api/file/g5raGGQMSD2I2LVUZRFT)

Select the application you wish to deploy. 

![alt text](https://www.filepicker.io/api/file/GKSkldiGTqSgDQpfM2BU)

Select the release you wish to deploy. You should only have the one release created from the successful build.

![alt text](https://www.filepicker.io/api/file/RTabu02eRxuM7Y1vmmJd)

Select the **-prod** environment. If you have been following along with the same application name (distell_wordpress) the environment will be named **distelli_wordpress-prod**, select that.

![alt text](https://www.filepicker.io/api/file/khDLPHKBQnmAXOi61JNJ)

You currently don't have any servers setup in any environments. At this point you will have to login to your server and install the Distelli agent. Click **Add Servers** button.

![alt text](https://www.filepicker.io/api/file/JH92CMu4QX6dnspPiAFH)

### Step 7. Add a Server

To facilitate doing a deploy of the Wordpress software from Distelli, you must install the Distelli agent on the server. Instructions for installing the agent can be found in the [Distelli Agent](doc:distelli-agent) reference guide. 

![alt text](https://www.filepicker.io/api/file/yNHQGVshQeHDzsCJ4fwj)

Now return to the Distelli WebUI and click the **Add Servers** link at the top to refresh the list. When your server populates the list, click on it, then click the **Add Servers** button.

![alt text](https://www.filepicker.io/api/file/wF5bT3UDRD2EVXZUThBs)

### Step 8. Start Deployment

Close the Servers dialog and click the **Start Deployment** button.

![alt text](https://www.filepicker.io/api/file/fvWJB0gnTWO5glK640eE)

Wordpress is now being installed on your server.

### Step 9. Using your Wordpress Site

After the deployment is successful you can begin setting up your Wordpress site. Using your browser, connect to your server.

![alt text](https://www.filepicker.io/api/file/OyZRTWDSJOkhzfcNzu9w)

That is it. You are up and running.
