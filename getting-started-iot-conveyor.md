---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="\_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Getting started with {{site.data.keyword.iot_short_notm}} and a simulated conveyor belt
Perform the following tasks to create a simple node.js web app that simulates a basic conveyor belt with an IoT device that sends monitoring data to {{site.data.keyword.iot_short_notm}} on {{site.data.keyword.Bluemix_notm}}.

## Prerequisites
{: #prereqs}

You need the following accounts and tools:
* [{{site.data.keyword.Bluemix_notm}} account](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}
* Optional: A mobile phone that can send accelerometer data by using a web application

To get stated with {{site.data.keyword.iot_short_notm}} using a different IoT device, see [Getting started with {{site.data.keyword.iot_short_notm}}](https://bluemix.net/docs/services/IoT/index.html).
{: tip}

## Step 1 - Deploy {{site.data.keyword.iot_short_notm}}
{: #deploy_watson_iot_platform_service}

Use the Cloud Foundry CLI to deploy services to {{site.data.keyword.Bluemix_notm}}.

1. Set your API endpoint by running the api command. Replace the `<API-endpoint>` value with the API endpoint for your region.
   ```
cf api <API-endpoint>
   ```
  {: pre}

  **API Endpoint**
  - *US South*: https://api.ng.bluemix.net
  - *United Kingdom*: https://api.eu-gb.bluemix.net
  - *Sydney*: https://api.au-syd.bluemix.net

2. Log into your {{site.data.keyword.Bluemix_notm}} account.

  ```
cf login
  ```
  {: pre}

3. Deploy the {{site.data.keyword.iot_short_notm}} to {{site.data.keyword.Bluemix_notm}} calling it `iotp-for-conveyor`.

   ```
cf create-service iotf-service iotf-service-free iotp-for-conveyor
  ```
  {: pre}


## Step 2 - Deploy the sample web application
{: #deploy_app}

1. Clone the Node.js *iot phone* sample app GitHub repository.
  ```
git clone https://github.com/theiliad/IBM-IoTP-ConveyorBelt
  ```
  {: pre}

2. On the command line, change the directory to the directory in which the sample app is located.
  ```
cd IBM-IoTP-ConveyorBelt
  ```
  {: pre}  

3. From the *IBM-IoTP-ConveyorBelt* directory, push your app to {{site.data.keyword.Bluemix_notm}} and give it a new name; that is, replace *YOUR_APP_NAME* in the following command. Use the `--no-start` option because you will start the app in the next stage after it is bound to {{site.data.keyword.iot_short_notm}}.
   ```
cf push YOUR_APP_NAME --no-start
  ```
  {: pre}


**Note:** Deploying your application can take a few minutes.


## Step 3 - Bind the app to {{site.data.keyword.iot_short_notm}}
{: #bind_app_to_service}
1. From within the *IBM-IoTP-ConveyorBelt* directory, bind your app to your instance of the {{site.data.keyword.iot_short_notm}} by using the names that you provided for each.
  ```
cf bind-service YOUR_APP_NAME iotp-for-conveyor
  ```
  {: pre}

2. Start your application for the binding to take effect.
  ```
cf start YOUR_APP_NAME
  ```
  {: pre}

3.  When deployment completes, a message displays to indicate that your app is running. View your app at the URL listed in the output of the push command or view both the app deployment status and the URL by running the following command:
  ```
cf apps
  ```
  {: pre}

You can troubleshoot errors in the deployment process by using the `cf logs YOUR_APP_NAME --recent` command.
{: tip}


## Step 4 - Run the web app on your desktop or phone
{: #run_app_desktop}

  1. Open the URL to see your app by using the following format:
```
  https://YOUR_APP_NAME.mybluemix.net
```
  For example, `https://conveyorbelt.mybluemix.net/`.

  2. Enter a device ID and token for your device.
  3. Open the {{site.data.keyword.iot_short_notm}} to verify that the device is registered.
    * Login to your {{site.data.keyword.Bluemix_notm}} dashboard: https://bluemix.net
    * From [your list of services](https://bluemix.net/dashboard/services), select {{site.data.keyword.iot_short_notm}} called *iotp-for-conveyor*.
    * Open {{site.data.keyword.iot_short_notm}} by using the *Launch* button. The dashboard opens in a new browser tab with a URL such as  `https://*iot-org-id*.internetofthings.ibmcloud.com`.
    * On the Devices tab, verify that your new device is displayed.
  4. Send sensor data to platform. By stopping, starting or changing the speed of the conveyor belt, new sensor data is sent to {{site.data.keyword.iot_short_notm}}.
  5. Optional: If you are running the app on a mobile device, shaking it can send accelerometer data for the conveyor belt to {{site.data.keyword.iot_short_notm}}.


## Step 5 - See raw data in the {{site.data.keyword.iot_short_notm}}
{: #see_live_data}

1. Open {{site.data.keyword.iot_short_notm}}.
2. Select Boards.
3. Select the "Device Centric Analytics" board.
4. Select your device on the "Devices I Care About" card.
3. Change the state of the conveyor belt or shake your phone and see live text data in the "Device Properties" card.

## Step 6 - Visualize live data in the {{site.data.keyword.iot_short_notm}}
{: #add_card}

Create a dashboard card to see live acceleration data.

1. On the same "Device Centric Analytics" board, click **Add New Card**, and then select **Line Chart**.
2. For Card source data, click **Cards**. A list of card names is displayed.
3. Select **Devices I Care About**, then click **Next**.
4. Click **Connect new data set**, and enter the following values:
  - Event: sensorData
  - Property: d.ay
  - Name: Accel. Y
  - Type: Float
  - Unit: gs
5. Click **Next**.
6. On the Card preview page, select **L** in the Settings, and then click **Next**.
7. On the Card information page, change the name of the title to  **Acceleration** and then click **Submit**.
8. Shake your phone to see the live data in your new card.

## What's next
- [Connect other IoT devices to {{site.data.keyword.iot_short_notm}}](../../services/IoT/iotplatform_task.html){:new_window}
- [Learn more about {{site.data.keyword.iot_short_notm}}](../../services/IoT/iotplatform_overview.html){:new_window}
- [Learn more about {{site.data.keyword.iot_short_notm}} APIs](../../services/IoT/reference/api.html){:new_window}
