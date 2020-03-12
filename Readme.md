EN|[CN](Readme_cn.md)

# Facial Recognition<a name="ZH-CN_TOPIC_0208835545"></a>

Developers can deploy the application on the Atlas 200 DK to register a face, predict the face information in the video by using the camera, and compare the predicted face with the registered face to predict the most possible user.

## Prerequisites<a name="zh-cn_topic_0203223340_section137245294533"></a>

Before using an open source application, ensure that:

-   Mind Studio  has been installed.
-   The Atlas 200 DK developer board has been connected to  Mind Studio, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Deployment
1. Deployment: choose either faster deployment or conventional deployment as shown below: 

   1.1 Faster deployment, refer to https://github.com/Atlas200dk/faster-deploy.git .
    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-   This faster deployment script can quickly deploy multiple cases, select facialrecognition case for this project.
    >-   This faster deployment automatically performs code download, model conversion and environment variable configuration. For details, choose conventional deployment method, as shown in 1.2.
    
   1.2 Conventional deployment, refer to : https://github.com/Atlas200dk/sample-README/tree/master/sample-facialrecognition .
    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-   This deployment method requires manually performing code download, model conversion and environment variable configuration. A better understand of the deployment process can be obtained from this method.


## Compile<a name="zh-cn_topic_0203223340_section147911829155918"></a>

1.  Open the corresponding project.

    Enter the “**MindStudio-ubuntu/bin**” directory after decompressing the installation package in the command line, for example, **$HOME/MindStudio-ubuntu/bin**. Run the following command to start **Mind Studio**:
    
    **./MindStudio.sh**

    After successfully starting Mind Studio, open **sample-facialrecognition** project，as shown in [Figure 1](#zh-cn_topic_0203223340_fig28591855104218).

    **Figure 1**  Open sample-facialrecognition project<a name="zh-cn_topic_0203223340_fig28591855104218"></a>  
    ![](figures/打开sample-facialrecognition工程.png "Open sample-facialrecognition project")

2.  Configure related project information in the **src/param\_configure.conf**.

    As shown in [Figure 2](#zh-cn_topic_0203223340_fig1338571124515).

    **Figure 2**  Configuration file path<a name="zh-cn_topic_0203223340_fig1338571124515"></a>  
    

    ![](figures/facial_open_src.png)

    The configuration file is as follows:

    ```
    remote_host=
    data_source=
    presenter_view_app_name=
    ```

    Following parameter configuration needs to be added manually：

    -   remote\_host：this parameter indicates the IP address of Atlas 200 DK developer board.
    -   data\_source: configure the channel to which the camera belongs, the value can be **Channel-1** or **Channel-2**. For checking the channel to which camera belongs, refer to **"View the Channel to which the camera belongs"**[Atlas 200 DK User Guidance](https://ascend.huawei.com/doc).
    -   presenter\_view\_app\_name: The user-defined View Name on the PresenterServer interface, this View Name needs to be unique  on the Presenter Server. It can only be a combination of uppercase and lowercase letters, numbers, and "\_", with a digit of 3 \~20.

     An example of video file configuration is as follows:

    ```
    remote_host=192.168.1.2
    data_source=Channel-1
    presenter_view_app_name=video
    ```

    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-   All the three parameters must be filled in, otherwise build cannot be passed.
    >-   Note that the "" symbol is no need to be used when filling in parameters.

3.  Run the deployment script to adjust the configuration parameters, download and compile 3rd party libraries. Open the Terminal of **Mind Studio** tool, which is under the main code directory, run the following command to execute environment deployment in the backstage, as shown in [Figure 3](#zh-cn_topic_0182554577_fig19292258105419).
    
    **Figure 3**  Execute deployment script<a name="zh-cn_topic_0182554577_fig19292258105419"></a>  
    
    ![](figures/deploy_facial.png)
    
    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-   Automatic download and compilation will perform if 3rd party libraries are not deployed for the first time of deployment. This process might take some time, please wait patiently. It will not download and compilation repeatedly when recompiling later, deployment is shown as above. 
    >-   Select the HOST IP connected to the developer board when deploying, which is usually the IP of virtual network card. If this IP belongs to the same segment as the developer board IP, it will be selected automatically and deployed. Otherwise, manual entering the IP connected to developer board is required for deployment.


4.  Begin to compile, open **Mind Studio** tool, click **Build \> Build \> Build-Configuration** in the toolbar, shown as [Figure 4](#zh-cn_topic_0203223340_fig1629455494718), **build** and **run** folders will be generated under the directory.

    **Figure 4**  Compilation operation and generated files<a name="zh-cn_topic_0203223340_fig1629455494718"></a>  
    ![](figures/编译操作及生成文件.png "Compilation operation and generated files")

    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >When you compile the project for the first time, **Build \> Build** is gray and not clickable. Your need to click **Build \> Edit Build Configuration**, configure the compilation parameters and then compile.  
    
    >![](figures/build_configuration.png)  

4.  <a name="zh-cn_topic_0203223340_li1364788188"></a>Start Presenter Server.

     Open **Terminal** of **Mind Studio** tool, it is in the path where code saved in [Step 1](#zh-cn_topic_0203223340_li953280133816) by default, run the following command to start the **Presenter Server** main program of the **_facialrecognition_** application, as shown in [Figure 5](#zh-cn_topic_0203223340_fig156364995016).

    **bash run\_present\_server.sh**

    **Figure 5**  Start PresenterServer<a name="zh-cn_topic_0203223340_fig156364995016"></a>  
    

    ![](figures/facial_run_1.png)

    -   When the message "Please choose one to show the presenter in browser (default: 127.0.0.1):" is displayed, enter the IP address used for accessing the Presenter Server service in the browser. Generally, the IP address is the IP address for accessing the Mind Studio service.
    -   When the message  "**Please input a absolute path to storage facial recognition data:**" ,is displayed, enter the path for storing face registration data and parsing data in **Mind Studio**. The **Mind Studio** user must have the read and write permissions. If the path does not exist, the script is automatically created.

    As shown in [Figure 6](#zh-cn_topic_0203223340_fig157571218181018), Select the IP address used by the browser to access the Presenter Server service in "Current environment valid ip list" and enter the path for face detection parsing data.


    **Figure 6**  Project deployment<a name="zh-cn_topic_0203223340_fig157571218181018"></a>  
    

    ![](figures/facial_run_2.png)

    As shown in [Figure 7](#zh-cn_topic_0203223340_fig123741843161320),  it means **presenter\_server** service starts successfully.

    **Figure 7** Starting the **Presenter Server** process<a name="zh-cn_topic_0203223340_fig123741843161320"></a>  
    

    ![](figures/facial_runOK.png)

    Use the URL shown in the preceding figure to log in to Presenter Server (only the Chrome browser is supported). The IP address is that entered in  [Figure 6](#zh-cn_topic_0203223340_fig157571218181018) and the default port number is 7009. The following figure indicates that Presenter Server is started successfully.
    

    **Figure 8**  Home page<a name="zh-cn_topic_0203223340_fig98461795813"></a>  
    ![](figures/主页显示.png "Home page")

    The following figure shows the IP address used by the **Presenter Server** and **Mind Studio** to communicate with the Atlas 200 DK.

    **Figure 9**  Example IP Address<a name="zh-cn_topic_0203223340_fig1627210116351"></a>  
    ![](figures/IP地址示例.png "Example IP Address")

    -   The IP address of the Atlas 200 DK developer board is 192.168.1.2 (connected in USB mode).
    -   The IP address used by the **Presenter Server** to communicate with the Atlas 200 DK is in the same network segment as the IP address of the Atlas 200 DK on the UI Host server. For example: 192.168.1.223.
    -   The following is an example of accessing the IP address of the **Presenter Server** using a browser: 10.10.0.1, because the Presenter Server and **Mind Studio** are deployed on the same server, the IP address is also the IP address for accessing the Mind Studio through the browser.


## Running<a name="zh-cn_topic_0203223340_section1676879104"></a>

1.  Run the Facial Recognition application

    Find **Run** button in the toolbar of **Mind Studio** tool, click **Run \> Run 'sample-facialrecognition'**, as shown in [Figure 10](#zh-cn_topic_0203223340_fig182957429910), the executable program has been executed on the developer board.

    **Figure 10**   Executed program<a name="zh-cn_topic_0203223340_fig182957429910"></a>  
    

    ![](figures/facial_run3.png)

2.   Log in to the **Presenter Server** website using the URL promoted when starting the **Presenter Server** service（only supports Chrome browser）, for details, please refer to [Step 5](#zh-cn_topic_0203223340_li1364788188) .

      Web page for **Presenter Server** is shown as [Figure 11](#zh-cn_topic_0203223340_fig1189774382115).

     **Figure 11**   Web page for **Presenter Server**<a name="zh-cn_topic_0203223340_fig1189774382115"></a>  
     ![](figures/Presenter-Server界面.png "Web page for **Presenter Server**")

     >![](public_sys-resources/icon-note.gif) **NOTE：**   
     >-   **Presenter Server** of Facial Recognition supports up to two Channels for display at the same time, each ** _presenter\_view\_app\_name_** corresponds to one Channel.
     >-   Due to hardware limitations, the maximum frame rate supported by each channel is 20fps, a lower frame rate is automatically used when the network bandwidth is low.
3.  Facial registration
    1.  Click the **Face Library** tab and enter a user name in the **Username** text box.

        **Figure 12**  Facial registration page<a name="zh-cn_topic_0203223340_fig12445181112163"></a>  
        ![](figures/人脸注册界面.png "Facial registration page")

    2.  Click **Browse** to upload a face image. Crop the face image based on the ratio of **Example Photo**.

    1.  Click **Submit**. If the upload fails, you can change the cropping ratio.


4.  Facial recognition and comparison.
  
    On the **App List** tab page, click ** _video_** for example in the **App Name** column. If a face is displayed in the camera and matches the registered face, the name and similarity information of the person are displayed.
   

## Follow-up Operations<a name="zh-cn_topic_0203223340_section1092612277429"></a>

-   **Stopping the Facial Recognition Application**

    **Facial Recognition** is running continually after being executed. To stop it, perform the following operation:

    Click the button shown in [Figure 13](#zh-cn_topic_0203223340_fig12461162791610) to stop **Facial Recognition**.

    **Figure 13**  Stopping **Facial Recognition** application<a name="zh-cn_topic_0203223340_fig12461162791610"></a>  
    

    ![](figures/facial_stopping.png)

    The application has been stopped as shown in [Figure 14](#zh-cn_topic_0203223340_fig5786125319165).

    **Figure 14**  **Facial Recognition** has been stopped<a name="zh-cn_topic_0203223340_fig5786125319165"></a>  
    

    ![](figures/facial_stopped.png)

-   **Stopping the Presenter Server Service**

    The Presenter Server service is always in the running state after being started. To stop the Presenter Server service of the facial recognition application, perform the following operations:

    Run the following command to check the process of the **Presenter Server** service corresponding to the facial recognition application in **Mind Studio** as the **Mind Studio** installation user:

    **ps -ef | grep presenter | grep facial\_recognition**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-facialrecognition$ ps -ef | grep presenter | grep facial_recognition
    ascend 22294 20313 22 14:45 pts/24?? 00:00:01 python3 presenterserver/presenter_server.py --app facial_recognition
    ```

    Where  _22294_  indicates the process ID of the **Presenter Server** service corresponding to the facial recognition application.

    To stop the service, run the following command:

    **kill -9** _22294_



