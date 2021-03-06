---
title: Cloud Foundry Eclipse Plugin
---

The Cloud Foundry Eclipse Plugin is an extension that enables Cloud Foundry users to deploy and manage Java and Spring applications on a Cloud Foundry instance from Eclipse or Spring Tools Suite (STS).

The plugin supports Eclipse v3.8 and v4.3 (a Java EE version is recommended), and STS 3.0.0 and later.

This page has instructions for installing and using v1.5.1 of the plugin, which is compatible with Cloud Foundry v2.

You can use the plugin to:

* Deploy applications from an Eclipse or STS workspace to a running Cloud Foundry instance. The plugin supports Java/JVM applications and framworks, such:
  * Spring
  * Java Web
  * Java standalone
  * Grails
  * Lift
* Create, bind, and unbind services.
* View and manage deployed applications and services.
* Start and stop applications.

v1.5.1 of the plugin provides several new features:

* Custom buildpack support --- When you deploy an application using the plugin, you can supply the URL of a custom buildpack.
* Separately defined host and domain --- In this version of the plugin, you specify the components (host and domain) of an application URL separately, rather than as a complete URL.
* Cloud Foundry server cloning --- v1.5.1 of the plugin makes it easier to work with multiple Cloud Foundry spaces. After configuring a first Cloud Foundry server instance using the plugin, you can use the new **Clone Server** command to create additional server instances that target other Cloud Foundry spaces.   

## <a id='install'></a>Install Cloud Foundry Eclipse Plugin ##

If you have a previous version of the Cloud Foundry Eclipse Plugin installed, uninstall it before installing the new version. To uninstall the plugin:

1. Choose **About Eclipse** (or **About Spring Tools Suite**) from the Eclipse (or **Spring Tools Suite**) menu and click **Installation Details**.  
1. On the **Installation Details**, select the previous version of the plugin and click **Uninstall**. 

Follow the installation instructions appropriate for your environment:

* [Install to Eclipse from Marketplace](#install-to-eclipse)
* [Install to STS from Extensions Tab](#install-to-sts).
* [Install from a Local Repository](#install-local)

### <a id='install-to-eclipse'></a>Install to Eclipse from Marketplace ###

Follow these instructions to install the Cloud Foundry Eclipse Plugin to Eclipse from the Eclipse Marketplace. 

1. Start Eclipse.
1. Select **Eclipse Marketplace** from the Eclipse **Help** menu.
1. On the marketplace window, enter "Cloud Foundry" in the **Find** field, and click **Go**.
1. In the search results, click the **Install** control next to the listing for Cloud Foundry Integration.

  <img src="/images/sts/eclipse-marketplace.png"/>  

1. The **Confirm Selected Features** window lists the plugin --- "Cloud Foundry Integration for Eclipse" --- and the optional "SpringSource UAA Integration" component, which reports tool usage data, anonymously. If you do not want your plugin usage statistics to be reported, de-select the UAA component before clicking **Confirm**.

     <img src="/images/sts/confirm-selected-features.png" />

1. The **Review Licenses** window appears. Click “I accept the terms of the license agremment” and click **Finish**.
1. The **Sofware Updates** window appears. Click **Yes** to restart Eclipse.

     <img src="/images/sts/software-updates.png" />

### <a id='install-to-sts'></a>Install to STS from Extensions Tab ###

Follow these instructions to install the Cloud Foundry Eclipse Plugin to STS from the **Extensions** tab.

1. Start STS.
1. Select the **Extensions** tab from the STS Dashboard.
1. Enter "Cloud Foundry" in the **Find** field.
1. Select **Cloud Foundry Integration for Eclipse** and click **Install**.

  <img src="/images/sts/extensions.png" />

1. The **Install** window lists the plugin --- "Cloud Foundry Integration for Eclipse" --- and the optional "Spring UAA Integration" component, which reports tool usage data, anonymously. If you prefer that your plugin usage statistics not be reported, de-select the UAA component beform clicking  **Next**.

  <img src="/images/sts/install.png"/>

1. On the **Install Details** window, click **Next**.

  <img src="/images/sts/install-details.png"/>

1. The **Review Licenses** window appears. Click “I accept the terms of the license agreement” and click **Finish** to perform the installation. 

1. The **Sofware Updates** window appears. Click **Yes** to restart STS.

     <img src="/images/sts/restart-sts.png" />

1. After STS restarts, you can see new panes in the Editor portion of the screen. See [About the Plugin User Interface](#plugin-ui) below for a description of the plugin tabs and the information in each.
1. Proceed to [Create a Cloud Foundry Server](#cloud-foundry-server).

### <a id='install-local'></a>Install from a Local Repository ###

If you need to install the Cloud Foundry Eclipse Plugin locally, rather than via the Internet, you can download the source and create a repository that you can copy to the target machine and then install from it. 

*Step 1:  Obtain the plugin source from GibHub.* 

* You can download archived source code for released versions of the plugin from https://github.com/SpringSource/eclipse-integration-cloudfoundry/releases.
* If you want the very latest source code for the plugin, clone the project repository:

    ```
    git clone https://github.com/SpringSource/eclipse-integration-cloudfoundry
    ```
<br>

*Step 2: Build repository.* 

Unzip the downloaded archive, change directory to the root directory and run this command in the shell:

`mvn -Pe37 package`

Transfer `org.cloudfoundry.ide.eclipse.server.site/target/site` to the machine where you want to install the plugin. If you zip it up, be sure to unzip prior to installation. 
 
*Step 3: Install from local repository.* 

On the machine running Eclipse or Spring Tools Suite:

1. In Eclipse (or STS), select **Install New Software** from the **Help** menu.
1. On the **Available Software** window, click **Add** to the right of the **Work with** field.
1. On the **Add Repository** window, enter a name for the repository, for example “Cloud Foundry Integration”, and click **Local**.
1. On the **Open** window, browse to `org.cloudfoundry.ide.eclipse.server.site/target/site` and click **Open**.
1. On the **Add Repository** window, click **OK**.
1. On the **Available Software** window checkmark: “Core/Cloud Foundry Integration” and “Resources/Cloud Foundry Integration” and click **Next**.
1. On the **Review Licenses** window, click “I accept the terms of the license agreement” and click **Finish**.



## <a id='cloud-foundry-server'></a>Create a Cloud Foundry Server ##

This section has instructions for configuring a server resource that will represent a target Cloud Foundry space. You will create a server for each space in Cloud Foundry to which you will deploy applications. Once you create your first Cloud Foundry service instances using the instructions below, you can create additional instances using the [Clone Server](#clone) feature.

1. Right-click the **Servers** view and select **New > Server**. 
1. In the **Define a New Server** window, expand the **Pivotal** folder, select **Cloud Foundry**, and click **Next**.  
    
    **Note:** Do not enter values for **Server host name** or **Server Runtime Environment**. These fields are unused and will be removed in a future version of the plugin.

     <img src="/images/sts/define-new-server.png" />

1. On the **Cloud Foundry Account** window, if you already have a Cloud Foundry account, enter the email account and password you use to log on to Cloud Foundry and click **Validate Account**. 

  If you do not have a Cloud Foundry account you can click **Pivotal CF Signup** to get one, and complete this procedure after your account is established.

  **Note:** The **Register Account** function is not supported by public instances of Cloud Foundry v2. You can register accounts for Pivotal CF Hosted using the Pivotal CF portal at [run.pivotal.io](https://console.run.pivotal.io).

     <img src="/images/sts/cloud-foundry-account.png" />

1. The **Cloud Foundry Account** window is refreshed and displays a message indicating whether or not your credentials were valid --- if they were, click **Next**. 

      <img src="/images/sts/new-server.png" />

1. On the **Organizations and Spaces** window, select the space you want to target, and click **Finish**. 

   **Note:** If you do not select a space, the server will be configured to connect to the default space, which is the first encountered in a list of your spaces. 

      <img src="/images/sts/orgs-and-spaces.png" />

1. Once you have successfully configured the Pivotal Cloud Foundry server, it will appear in the **Servers** view of the Eclipse or STS user interface. To familiarize yourself with the plugin user interface, see [About the Plugin User Interface](#plugin-ui). When you are ready, proceed to [Deploy an Application](#deploy-an-application).     

## <a id='plugin-ui'></a>About the Plugin User Interface ##

The paragraphs below describe the Cloud Foundry Eclipse plugin user interface. If you do not see the tabs described below, select the Pivotal Cloud Foundry server in the **Servers** view.

The Cloud Foundry editor, outlined in red in the screenshot below, is the primary plugin user interface.
Some workflows involve interacting with standard elements of the Eclipse user interface, such as the  Project Explorer, Console and Servers views.

Note that the Cloud Foundry editor allows you to work with a single Cloud Foundry space; each space is represented by a distinct server instance in the Servers view (B). Multiple editors, each targeting a different space, can be open simultaneously. However, only one editor targeting a particular Cloud Foundry server instance can be open at a time. 

### <a id='overview-tab'></a>Overview Tab ###

The follow panes and views are present when the **Overview** tab is selected:

* A --- The **Package Explorer** view lists the projects in the current workspace. 
* B -- The **Servers** view lists server instances configured in the current workspace. A server of type "Pivotal Cloud Foundry" represents a targeted space in a Cloud Foundry instance. 
* C -- The **General Information** pane.
* D -- The **Account Information** pane lists your Cloud Foundry credentials and the target organization and space. The pane includes these controls:
    * **Clone Server** --- Use to create additional Pivotal Cloud Foundry server instances. You must configure a server instance for each Cloud Foundry space you wish to target. For more information, see [Create Additional Server Instances](#clone).
    * **Change Password** --- Use to change your Cloud Foundry password.
    * **Validate Account** --- Use to verify your currently configured Cloud Foundry credentials.
    * **Pivotal CF Signup** --- Use to sign up for a Cloud Foundry account.
* E -- The **Server Status** pane shows whether or not you are connected to the target Cloud Foundry space, and **Disconnect** and **Connect** controls.
* F -- The **Console** view displays status messages when you perform an action such as deploying an application.
* G -- The **Remote Systems View** allows you to view the contents of a file that is part of a deployed application. For more information, see [View an Application File](#view-file).

<img src="/images/sts/ui-overview-tab.png" style="width: 1150px;"/>

### <a id='apps-services-tab'></a>Applications and Services Tab ###

The follow panes are present when the **Applications and Services** tab is selected: 

* H --- The **Applications** pane lists the applications deployed to the target space.
* I ---  The **Services** pane lists the services provisioned in the targeted space.
* J ---  The **General** pane displays the following information for the application currently selected in the **Applications** pane:
      * **Name** 
      * **Mapped URLs** -- Lists URLs mapped to the application. You can click a URL to open a browser to the application within Eclipse (or STS); and click the pencil icon to add or remove mapped URLs. See [Manage Application URLs](#manage-urls).
      * **Memory Limit** -- The amount of memory allocated to the application. You can use the pull-down to change the memory limit.
      * **Instances** -- The number of instances of the application that are deployed. You can use the pull-down to change number of instances.
      * **Start**, **Stop**, **Restart**, **Update and Restart** --- The controls that appear depend on the current state of the application.  The **Update and Restart** button appears if there is an accessible workspace project that is linked to one of the deployed applications; this command will attempt to push changed resources before starting the application. 

* K --- The **Services** pane lists services that are bound to the application currently selected in the **Applications** pane. Note the icon in the upper right corner of the pane --- it allows you to create a service, as described in [Create a Service](#create-service). 

<img src="/images/sts/ui-apps-services-tab.png" style="width: 1150px;" />

## <a id='deploy-an-application'></a>Deploy an Application ##

To deploy an application to Cloud Foundry using the plugin: 

1. To initiate deployment either:
  * Drag the application from the **Package Explorer** view onto the Pivotal Cloud Foundry server in the **Servers** view, or
  * Right-click the Pivotal Cloud Foundry server in the **Servers** view, select **Add and Remove** from the server context menu, and move the application from the **Available** to the **Configured** column.

1. On the **Application Details** window, you can enter the URL of an external buildpack if desired. Click **Next** to continue.

      <img src="/images/sts/application-details.png" />

1. On the **Launch Deployment** window:

  **Host** --- By default, contains the name of the application.
  
  **Domain** --- Contains the default domain. If you have mapped custom domains to the target space, they appear in the pull-down list.  **Note**:  This version of the Cloud Foundry Eclipse plugin does not provide a mechanism for mapping a custom domain to a space. You must use the `cf map domain` command to do so. For more information, see [map-domain](/docs/using/managing-apps/cf/index.html#map-domain).
  
  **Deployed URL** --- By default, contains the value of the **Host** and **Domain** fields, separated by a period (.) character.
  
  **Memory Reservation** --- Select the amount of memory to allocate to the application from the pull-down list.
  
  **Start application on deployment** --- If you do not want the application to be started upon deployment, uncheck the box.

      <img src="/images/sts/launch-deployment.png" />

1. The **Services Selection** window lists services provisioned in the target space. Checkmark the services, if any, that you want to bind to the application, and click **Finish**. Note that you can bind services to the application after deployment, as described in [Bind and Unbind Services](bind-service).

      <img src="/images/sts/services-selection.png" />

   As the deployment proceeds, progress messages appear in the **Console** view. When deployment is complete, the application is listed in the **Applications** pane.   

## <a id='create-service'></a>Create a Service ##

Before you can bind a service to an application you must create it. To do so:

1. Select the **Applications and Services** tab.
1. Click the icon in the upper right corner of the "Services" pane.
1. In the **Service Configuration** window:

  * **Name** --- Enter a name for the service.
  * **Type** --- Select the service type from the pull-down list.

      <img src="/images/sts/service-configuration.png" />

The new service appears in the **Services** pane.

## <a id='bind-service'></a>Bind and Unbind Services ##

You can bind a service to an application when you deploy it. To bind a service to an application that is already deployed, drag the service from the **Services** pane to the **Application Services** pane.  (See the area labelled "G" in the screenshot in the [Applications and Services](#apps-services-tab) above.)

To unbind a service, right-click the service in the **Application Services** pane, and select **Unbind from Application**.

## <a id='view-file'></a>View an Application File ##

You can view the contents of a file in a deployed application by selecting it the **Remote Systems View**. (See the areas labelled "I" and "J" in the screenshot in the [Applications and Services Tab](#overview-tab) above.) 

1. If the **Remote Systems View** is not visible:
  * Select the **Applications and Services** tab.
  * In the **Instances** pane, click the **Remote Systems View** link.

2. On the **Remote Systems View**, browse to the application and application file of interest, and double-click the file. A new tab appears in the editor area with the contents of the selected file. 

      <img src="/images/sts/file-contents.png" />

## <a id='undeploy'></a>Undeploy an Application ##

To undeploy an application, right click the appliation in either the **Servers** or the **Applications** pane and clicke **Remove**.

## <a id='scale-application'></a>Scale an Application ##

You can change the memory allocation for an application and the number of instances deployed in the **General** pane when the **Applications and Services** tab is selected.  Use the **Memory Limit** and **Instances** selector lists. 

## <a id='manage-app-urls'></a>Manage Application URLs ##

You add, edit, and remove URLs mapped to the currently selected application in the **General** pane when the **Applications and Services** tab is selected.  Click the pencil icon to display the **Mapped URIs Configuration** window. 

<img src="/images/sts/manage-uris-configuration.png" />


## <a id='clone'></a>Clone a Cloud Foundry Server Instance ##

Each space in Cloud Foundry to which you want to deploy applications must be represented by a server of type "Cloud Foundry". After you have created a Cloud Foundry server instance, as decribed in [Create a Cloud Foundry Server](#cloud-foundry-instance), you can clone it to create another. 

To clone a server:

1. Right-click a Cloud Foundry server instance in the **Servers** view, and select **Clone Server** from the context menu.
1. On the **Organizations and Spaces** window, select the space you want to target. 
1. The name field will be filled with the name of the space you selected. If desired, edit the server name before clicking finish **Finish**.

## <a id='add-URL'></a>Add a Cloud Foundry Instance URL ##

By default, the Cloud Foundry Eclipse plugin is configured to connect with Pivotal CF Hosted instance. You can configure the plugin to work with other Cloud Foundry instances to which you have access.  To do so: 

1. Perform steps 1 and 2 of [Create a Cloud Foundry Server](#cloud-foundry-server).
1. On the **Cloud Foundry Account** window, enter the email account and password you use to log on to the target instance, and then click **Manage Cloud URLs**

  <img src="/images/sts/cloud-foundry-account.png" />
 
1. On the **Manage Cloud URLs** window, click **Add**.

      <img src="/images/sts/manage-cloud-urls.png" />

1. On the **Add a Cloud URL** window, enter the name and URL of the target cloud instance and click **Finish**. 

      <img src="/images/sts/add-cloud-url.png" />

1. The new cloud instance should appear in the list on the **Manage Cloud URLs** window. Click **OK** to proceed. 
1. On the **Cloud Foundry Account** window, click **Validate Account**. 
1. Complete steps 4 through 6 of [Create a Cloud Foundry Server](#cloud-foundry-server).

     



