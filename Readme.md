English|[中文](Readme_cn.md)

# Facial Recognition<a name="EN-US_TOPIC_0232642722"></a>

Developers can deploy the application on the Atlas 200 DK to implement face registrations, predict the face information in a video by using cameras, and compare the predicted face with the registered face to output the most possible user.

The applications in the current version branch adapt to  [DDK&RunTime](https://ascend.huawei.com/resources) **1.32.0.0 and later**.

## Prerequisites<a name="en-us_topic_0228461922_section137245294533"></a>

Before deploying this sample, ensure that:

-   Mind Studio  has been installed.
-   The Atlas 200 DK developer board has been connected to  Mind Studio, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Deployment<a name="en-us_topic_0228461922_section412811285117"></a>

You can use either of the following methods:

1.  Quick deployment: visit  [https://github.com/Atlas200dk/faster-deploy](https://github.com/Atlas200dk/faster-deploy).

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   The quick deployment script can be used to deploy multiple samples rapidly. Select  **facialrecognition**.  
    >-   The quick deployment script automatically completes code download, model conversion, and environment variable configuration. To learn about the detailed deployment process, go to  [2. Common deployment](#en-us_topic_0228461922_li10170621131715).  

2.  <a name="en-us_topic_0228461922_li10170621131715"></a>Common deployment: visit  [https://github.com/Atlas200dk/sample-README/tree/master/sample-facialrecognition](https://github.com/Atlas200dk/sample-READEME/tree/master/sample-facialrecognition).

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   In this deployment mode, you need to manually download code, convert models, and configure environment variables. After that, you will have a better understanding of the process.  


## Building a Project<a name="en-us_topic_0228461922_section147911829155918"></a>

1.  Open the project.

    Go to the directory that stores the decompressed installation package as the Mind Studio installation user in CLI mode, for example,  **$HOME/MindStudio-ubuntu/bin**. Run the following command to start Mind Studio:

    **./MindStudio.sh**

    After the startup is successful, open the  **sample-facialrecognition**  project, as shown in  [Figure 1](#en-us_topic_0228461922_en-us_topic_0203223340_fig28591855104218).

    **Figure  1**  Opening the sample-facialrecognition project<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig28591855104218"></a>  
    ![](figures/opening-the-sample-facialrecognition-project.png "opening-the-sample-facialrecognition-project")

2.  Configure project information in the  **src/param\_configure.conf**  file.

    For details, see  [Figure 2](#en-us_topic_0228461922_en-us_topic_0203223340_fig1338571124515).

    **Figure  2**  Configuration file path<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig1338571124515"></a>  
    

    ![](figures/facial_open_src.png)

    The default configurations of the configuration file are as follows:

    ```
    remote_host=192.168.1.2
    data_source=Channel-1
    presenter_view_app_name=video
    ```

    -   **remote\_host**: IP address of the Atlas 200 DK developer board
    -   **data\_source**: camera channel. The value can be  **Channel-1**  or  **Channel-2**. For details, see  **Viewing the Channel to Which a Camera Belongs**  in  [Atlas 200 DK User Guide](https://ascend.huawei.com/doc/Atlas200DK/).
    -   **presenter\_view\_app\_name**: indicates the value of  **View Name**  on the  **Presenter Server**  page, which must be unique. The value consists of 3 to 20 characters and supports only uppercase letters, lowercase letters, digits, and underscores \(\_\).

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   All the three parameters must be set. Otherwise, the build fails.  
    >-   Do not use double quotation marks \(""\) during parameter settings.  
    >-   Modify the default configurations as required.  

3.  Run the  **deploy.sh**  script to adjust configuration parameters and download and compile the third-party library. Open the  **Terminal**  window of Mind Studio. By default, the home directory of the code is used. Run the  **deploy.sh**  script in the background to deploy the environment, as shown in  [Figure 3](#en-us_topic_0228461922_en-us_topic_0203223340_fig16909182592016).

    **Figure  3**  Running the deploy.sh script<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig16909182592016"></a>  
    ![](figures/running-the-deploy-sh-script.png "running-the-deploy-sh-script")

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   During the first deployment, if no third-party library is used, the system automatically downloads and builds the third-party library, which may take a long time. The third-party library can be directly used for the subsequent compilation.  
    >-   During deployment, select the IP address of the host that communicates with the developer board. Generally, the IP address is the IP address configured for the virtual NIC. If the IP address is in the same network segment as the IP address of the developer board, it is automatically selected for deployment. If they are not in the same network segment, you need to manually type the IP address of the host that communicates with the developer board to complete the deployment.  

4.  Start the build. Open Mind Studio and choose  **Build \> Build \> Build-Configuration**  from the main menu. The  **build**  and  **run**  folders are generated in the directory, as shown in  [Figure 4](#en-us_topic_0228461922_en-us_topic_0203223340_fig1629455494718).

    **Figure  4**  Build and file generating<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig1629455494718"></a>  
    ![](figures/build-and-file-generating.png "build-and-file-generating")

    >![](public_sys-resources/icon-notice.gif) **NOTICE:**   
    >When you build a project for the first time,  **Build \> Build**  is unavailable. You need to choose  **Build \> Edit Build Configuration**  to set parameters before the build.  

5.  Start Presenter Server.

    Open the  **Terminal**  window of Mind Studio. By default, under the code storage path, run the following command to start the Presenter Server program of the facial recognition application on the server, as shown in  [Figure 5](#en-us_topic_0228461922_en-us_topic_0203223340_fig156364995016):

    **bash run\_present\_server.sh**

    **Figure  5**  Starting Presenter Server<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig156364995016"></a>  
    

    ![](figures/facial_run_1.png)

    -   When the message  **Please choose one to show the presenter in browser\(default: 127.0.0.1\):**  is displayed, type the IP address \(usually IP address for accessing Mind Studio\) used for accessing the Presenter Server service in the browser.
    -   When the message  **Please input a absolute path to storage facial recognition data:**  is displayed, type the path for storing face registration data and parsing data on Mind Studio. The  Mind Studio  user must have the read and write permissions. If the path does not exist, the script will automatically create it.

    Select the IP address used by the browser to access the Presenter Server service in  **Current environment valid ip list**  and type the path for storing facial recognition data, as shown in  [Figure 6](#en-us_topic_0228461922_en-us_topic_0203223340_fig157571218181018).

    **Figure  6**  Project deployment<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig157571218181018"></a>  
    

    ![](figures/facial_run_2.png)

    [Figure 7](#en-us_topic_0228461922_en-us_topic_0203223340_fig123741843161320)  shows that the presenter\_server service has been started successfully.

    **Figure  7**  Starting the Presenter Server process<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig123741843161320"></a>  
    

    ![](figures/facial_runok.png)

    Use the URL shown in the preceding figure to log in to Presenter Server \(only the Chrome browser is supported\). The IP address is that typed in  [Figure 6](#en-us_topic_0228461922_en-us_topic_0203223340_fig157571218181018)  and the default port number is  **7009**. The following figure indicates that Presenter Server has been started successfully.

    **Figure  8**  Home page<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig98461795813"></a>  
    ![](figures/home-page.png "home-page")

    The following figure shows the IP address used by Presenter Server and  Mind Studio  to communicate with the Atlas 200 DK.

    **Figure  9**  IP address example<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig1627210116351"></a>  
    ![](figures/ip-address-example.png "ip-address-example")

    Where:

    -   The IP address of the Atlas 200 DK developer board is 192.168.1.2 \(connected in USB mode\).
    -   The IP address used by the Presenter Server to communicate with the Atlas 200 DK is in the same network segment as the IP address of the Atlas 200 DK on the UI Host server. For example: 192.168.1.223.
    -   The following describes how to access the IP address \(such as  **10.10.0.1**\) of Presenter Server using a browser. Because Presenter Server and  Mind Studio  are deployed on the same server, you can access  Mind Studio  through the browser using the same IP address. 


## Run<a name="en-us_topic_0228461922_section1676879104"></a>

1.  Run the facial recognition application.

    On the toolbar of Mind Studio, click  **Run**  and choose  **Run \> Run 'sample-facialrecognition'**. As shown in  [Figure 10](#en-us_topic_0228461922_fig182957429910), the executable application is running on the developer board.

    **Figure  10**  Application running<a name="en-us_topic_0228461922_fig182957429910"></a>  
    

    ![](figures/facial_run3.png)

2.  Use the URL displayed upon the start of the Presenter Server service to log in to Presenter Server.

    [Figure 11](#en-us_topic_0228461922_fig1189774382115)  shows the Presenter Server page.

    **Figure  11**  Presenter Server page<a name="en-us_topic_0228461922_fig1189774382115"></a>  
    ![](figures/presenter-server-page.png "presenter-server-page")

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   Presenter Server of the facial recognition application supports a maximum of two channels at the same time \(each  _presenter\_view\_app\_name_  corresponds to a channel\).  
    >-   Due to hardware limitations, each channel supports a maximum frame rate of 20 fps. A lower frame rate is automatically used when the network bandwidth is low.  

3.  Register a face.
    1.  Click the  **Face Library**  tab and enter a user name in the  **Username**  text box.

        **Figure  12**  Face registration page<a name="en-us_topic_0228461922_fig12445181112163"></a>  
        ![](figures/face-registration-page.png "face-registration-page")

    2.  Click  **Browse**  to upload a face image. Crop the face image based on the ratio of  **Example Photo**.

    1.  Click  **Submit**. If the upload fails, you can change the cropping ratio.

4.  Perform facial recognition and comparison.

    On the  **App List**  tab page, click  _video_  for example in the  **App Name**  column. If a face is displayed in the camera and matches the registered face, the name and similarity information of the person are displayed.


## Follow-up Operations<a name="en-us_topic_0228461922_section1092612277429"></a>

-   **Stopping the Facial Recognition Application**

    The facial recognition application is running continually after being executed. To stop it, perform the following operation:

    Click the stop button shown in  [Figure 13](#en-us_topic_0228461922_en-us_topic_0203223340_fig12461162791610)  to stop the facial recognition application.

    **Figure  13**  Stop of the facial recognition application<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig12461162791610"></a>  
    

    ![](figures/facial_stopping.png)

    [Figure 14](#en-us_topic_0228461922_en-us_topic_0203223340_fig5786125319165)  shows that the application has been stopped.

    **Figure  14**  Stop of the facial recognition application<a name="en-us_topic_0228461922_en-us_topic_0203223340_fig5786125319165"></a>  
    

    ![](figures/facial_stopped.png)

-   **Stopping the Presenter Server Service**

    The Presenter Server service is always in running state after being started. To stop the Presenter Server service of the facial recognition application, perform the following operations:

    Run the following command to check the process of the Presenter Server service corresponding to the facial recognition application as the  Mind Studio  installation user:

    **ps -ef | grep presenter | grep facial\_recognition**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-facialrecognition$ ps -ef | grep presenter | grep facial_recognition
    ascend 22294 20313 22 14:45 pts/24?? 00:00:01 python3 presenterserver/presenter_server.py --app facial_recognition
    ```

    In the preceding information,  _22294_  indicates the process ID of the Presenter Server service corresponding to the facial recognition application.

    To stop the service, run the following command:

    **kill -9** _22294_


