<h1>Setting Up Azure SIEM Home Lab</h1>

 

<h2>Description</h2>
I will be giving a tutorial of how to set up Azure Sentinel (SIEM) and connect it to a live virtual machine that will have an active honey pot. The goal is to observe live RDP Brute Force attacks from all over. We will also use PowerShell to look up attackers geolocation info and plot it in Azure Sentinel Map.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Powershell<b>

<h2>Environments Used </h2>

- <b>Microsoft Azure Cloud (Free Trial)</b>
- <b>Azure VM</b>
- <b>Azure Sentinel (SIEM)</b>
- <b>Log Analytics Workspace</b>

<h2>Walk-through: (Note: This requires you to have made an Azure Free Trial account or Pay as you Go account)</h2>

<p align="center">
Step by Step process for this lab: <br/>
<br/>
<br/>

- To start, click on the 3 lines in the top left hand corner of the portal and then scroll down till you see "Virtual machines", then click on it: <br/>
![Screenshot 2022-10-03 230213](https://user-images.githubusercontent.com/114842751/193718634-28fa4bc5-5d43-49ce-aed8-7ea8b4fc2728.png)
<br/>
<br/>

- You will then be brought to the Azure VM page where you will click on the "+ Create" and then select, "Azure virtual machine": <br/>
![Screenshot 2022-10-03 231613](https://user-images.githubusercontent.com/114842751/193720199-4d646c1d-fc0a-4536-a397-76db82e1f178.png)
<br/>
<br/>

- Now you will set up your VM, so first you're going to want to creat a new Resource group and name it, to do this, you will want to click "Create New", then name the Resource Group what ever name you wish then click "OK": <br/>
![Screenshot 2022-10-03 231731](https://user-images.githubusercontent.com/114842751/193720530-4dec3e67-5853-4b9b-963c-45a2310056b1.png)
<br/>
<br/>

- This next step I am going to display in the screenshots below, just fill in the following with the exception of "Username and Password", create your own for this lab: <br/>
![Screenshot 2022-10-03 232735](https://user-images.githubusercontent.com/114842751/193721495-966e112b-6118-4bc9-b111-fd99706294c2.png)
![Screenshot 2022-10-03 232806](https://user-images.githubusercontent.com/114842751/193721500-0558c325-2d8c-4519-98e4-d9fc0a1dad49.png)
<br/>
<br/>

- At the bottom click "Next: Disk >", then click "Next: Networking >", Here we will be creating a firewall. So where it says "NIC Network Security Group" click "Advanced" and then "Create new" under "Configure NSG":
![Screenshot 2022-10-03 233341](https://user-images.githubusercontent.com/114842751/193722136-e7c81b01-e3f3-464e-b162-ab8415c8f0cc.png)
<br/>
<br/>

- Then we will remove the Default firewall because in this lab we want invaders to come into our honeypot, so on the right with the 3 dots, click that and then click "Remove", then click "Add an inbound rule": <br/>
![Screenshot 2022-10-03 233656](https://user-images.githubusercontent.com/114842751/193722489-96000ae0-4789-406b-ad18-4e33095dfd52.png)
<br/>
<br/>

- For this step, fill in the following and then at the bottom click "Add": <br/>
![Screenshot 2022-10-03 233936](https://user-images.githubusercontent.com/114842751/193722803-401e6008-072d-44bf-b9a9-3483b9a333a0.png)
<br/>
<br/>

- Then at the bottom left click "Ok" then again at the bottom left, click "Review + create" once it has loaded and finished configuring, click "Create": <br/>
![Screenshot 2022-10-03 234215](https://user-images.githubusercontent.com/114842751/193723151-474c4135-96f8-43ec-badc-866a60fdefd9.png)
<br/>
<br/>

- The deployment will take awhile so the next step is to creat a Log Analytics workspace. So go to the search bar and type it in and proceed. <br/>
<br/>
<br/>

- This will be used to basically ingest all events from the VM and create multiple logs from the events occuring. <br/>
<br/>
<br/>

- While you are in Log Analytics, create a new Log and fill in the following then click "Review + create" and then "Create": <br/>
![Screenshot 2022-10-03 235651](https://user-images.githubusercontent.com/114842751/193724822-14b31a4f-2b32-4a08-b7c1-1ec72b2f88d6.png)
<br/>
<br/>

- The next steps are as follows: <br/>

go to "Microsoft Defender for Cloud"
> Find and click on "Environment Settings" in lefthand toolbar. 
> Find and click on the dropdown arrow immediately next to your Azure subscription to reveal the NAME of your workspace (bear in mind everything has to be deployed in order for this step to work).
> Click on the workspace name to open its settings.
> In settings, disable "SQL servers on machines" .
> In settings, enable "Servers".
> click the save button in the top left next to the search bar.
> click on "Data Collection" in the lefthand toolbar.
> Select "All Events" and save by clicking on the "Save" button.
<br/>
<br/>

- After doing the following steps provided above we will move back to Log Analytics to connect it to the VM we created. <br/>
<br/>
<br/>

- Now click on the following in order to start the connection of the Log and Vm: <br/>
![Screenshot 2022-10-04 001303](https://user-images.githubusercontent.com/114842751/193726571-764d14dd-2056-41bb-b7ef-a4424aa41f77.png)
<br/>
<br/>

- Then click on the name of the VM you created and then in the top left of the next page click "Connect": <br/>
![Screenshot 2022-10-04 001456](https://user-images.githubusercontent.com/114842751/193726765-73df8867-754b-49ff-af65-e16287114967.png)
![Screenshot 2022-10-04 001510](https://user-images.githubusercontent.com/114842751/193726774-4f45723c-796d-4432-bc5a-b0ea09e7367a.png)
<br/>
<br/>

- While it is Connecting Open a new page with your Azure Portal to start setting up Azure Sentinel SIEM (now called Microsoft Sentinel): <br/>
<br/>
<br/>

- Click "Create Microsoft Sentinel": <br/>
![Screenshot 2022-10-04 001939](https://user-images.githubusercontent.com/114842751/193727206-d91a79aa-2c73-466d-aca8-e105a1be8f2c.png)
<br/>
<br/>

- Then click on the VM within Sentinel and at the bottom left click "Add" 
![Screenshot 2022-10-04 002148](https://user-images.githubusercontent.com/114842751/193727421-339a041c-2502-427e-b433-2378f6d503d2.png)
<br/>
<br/>

- While it is adding Sentinel, go back over to Virtual Machine to login from Remote Desktop. <br/>
<br/>
<br/>

- Click on the VM, and copy the Public IP Address: <br/>
![Screenshot 2022-10-04 002558](https://user-images.githubusercontent.com/114842751/193727903-b00958b2-74c8-4049-bb05-0253cd323ef9.png)
<br/>
<br/>

- In Windows on your actual PC pull up, Remote Desktop Connection and paste the Public IP you got for the VM and then Click "Connect": <br/>
![Screenshot 2022-10-04 003042](https://user-images.githubusercontent.com/114842751/193728416-def3dd78-7a10-44dc-8dbb-3c8c4fe597ea.png)
<br/>
<br/>

- When propted to give your login credentials, Click "More choices" and select "Use a different account": <br/>
![Screenshot 2022-10-04 003345](https://user-images.githubusercontent.com/114842751/193728685-33c7cc50-78ac-43e8-b530-e4c84cb2ab37.png)
<br/>
<br/>

- Accept the Certificate Warning and It will load the VM, once in Select "No" for everything (This is a lab so it doesn't matter). <br/>
<br/>
- Once in, set up Microsoft Edge because we will need it for future events. <br/>
<br/>
<br/>

- While in the VM, click the windows button and search "Event Viewer", then open Event Viewer: <br/>
![Screenshot 2022-10-04 004325](https://user-images.githubusercontent.com/114842751/193729700-6539fd72-38e4-4f8d-8fd2-6168cae4928f.png)
<br/>
<br/>

- Next, click on "Windows Logs", then "Security". (We will be focused on code 4625 Login Failure): <br/>
![Screenshot 2022-10-04 005136](https://user-images.githubusercontent.com/114842751/193730507-eb07e7dd-44e5-4b60-a2ff-9f9ede428bf3.png)
<br/>
<br/>

- We need to turn off the firewall so that way the VM is discoverable to the outside. (Good way to test is use CMD on your personal pc and ping the VM IP and you should get "Request timed out") <br/>
<br/>

- So next step is turn off the firewall in your VM so, in the start menu of your VM, type in the search bar "wf.msc" and click on it. Then click "Windows Defender Firewall Porperties". Then turn off the following: Domain Profile, Private, Profile, Public Profile. Then click, "Apply" then "Ok": <br/>
![Screenshot 2022-10-04 010035](https://user-images.githubusercontent.com/114842751/193731471-0dc0defc-b1de-4909-bc03-d3374806b6bb.png)
<br/>
<br/>

- (Now if you ping the VM you should get the requests and that shows that the firewalls are down) <br/>
<br/>
<br/>

- Next you are going to want to Copy the PowerShell Script called "Custom_Security_Log_Exporter.ps1" from the following GitHub: https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1 <br/>
<br/>
<br/>

- Next on the VM your going to want to open PowerShell ISE, then select "New", then paste the copied code from the GitHub provided above: <br/>
![Screenshot 2022-10-04 025322](https://user-images.githubusercontent.com/114842751/193744735-b698b5fc-c29c-46f7-afb7-a959de8f8ef9.png)
<br/>
<br/>

- Then save the PowerShell script to your VM Desktop and you will want to rename it: <br/>
![Screenshot 2022-10-04 025752](https://user-images.githubusercontent.com/114842751/193745289-090aaba8-b488-4d73-a5e7-9854f1a1c82e.png)
<br/>
<br/>

- So now looking at the script you copied into PowerShell you'll notice $API Key. This key is mine so you will need to create your own. In order to do that, you will need to make an account on "ipgeolocation.io" (it's free). Once you do this you will automatically sign in and notice the API Key. Copy it and past it over the API Key in the PowerShell script: <br/>
![Screenshot 2022-10-04 030311](https://user-images.githubusercontent.com/114842751/193746015-cdfa3282-5f39-47eb-bb8f-adee39a32640.png)
![Screenshot 2022-10-04 030326](https://user-images.githubusercontent.com/114842751/193746030-2d0e9c22-0365-4547-8e9a-370288a9a141.png)
- *The reason you need this is to get the longitude/latitude of the attackers when we start to get into the Log aspect of this lab*
<br/>
<br/>

- Then run the PowerShell (You will notice that the script is a loop that goes through the security event log we pulled up earlier and is logging all the failed login attempts "code 4625"): <br/>
![Screenshot 2022-10-04 030858](https://user-images.githubusercontent.com/114842751/193746777-aef79daa-77b6-4111-8b8e-cca9e4187c7b.png)
<br/>
<br/>

- Another thing you will notice is the location of the saved geolocations for the failed login attempts in the script in PowerShell, "$LOGFILE_PATH = "C:\ProgramData\$($LOGFILE_NAME)". This file is hidden so you'll need to run the "Run" app and copy and pasted "C:\ProgramData\". This will pull up the txt file that we will need later. <br/>
<br/>
<br/>

- We now will create the path for our Logs to be able to read the geolocation and make custom logs using the data from the honeypot VM. <br/>
<br/>
<br/>

- So, going back to the Azure Portal we are going to want to go back to Log Analytics workspace, click on the law_honeypot (whatever you named the log) and then go to "Custom Logs": <br/>
![Screenshot 2022-10-04 032933](https://user-images.githubusercontent.com/114842751/193749765-5f966836-19c2-4df3-a87a-2a6e5292c56e.png)
<br/>
<br/>

- Then click "Add custom log". For this next step, you are going to want to go back to your VM and pull up the txt file with all the failed logs. Copy the contents from the txt file. Go back to your actual pc, make a text file and paste the logs from the VM. Save it to your desktop on your personal pc so it's easier to find. Then back to Azure Logs where you started a Custom log, click the Browse tab and select the file you save to your Desktop. The results after clicking "Next" should look like this: <br/>
![Screenshot 2022-10-04 033718](https://user-images.githubusercontent.com/114842751/193750907-47b4a26f-ba85-41cf-9f77-0b46964ec011.png)
<br/>
<br/>

Click "Next" and type in the following: <br/>
![Screenshot 2022-10-04 034040](https://user-images.githubusercontent.com/114842751/193751325-4e0f9cf2-d2ab-4959-ba3e-4dbc5f49decc.png)
*Note: Make sure the path is correct otherwise Azure cant pull the data logs from the VM and display them correctly*
<br/>
<br/>

- Click "Next", then fill in the following with whatever you wish: <br/>
![Screenshot 2022-10-04 034304](https://user-images.githubusercontent.com/114842751/193751712-a0b0574c-d954-445b-aed9-0333ab322e72.png)
- *Azure automatically appends the _CL at the end*
<br/>
<br/>

- Click "Next", then "Create". (This may take awhile) <br/>
<br/>
<br/>

- Go to "Logs" within the named Log you created and in the Query run the following command: <br/>
![Screenshot 2022-10-04 034933](https://user-images.githubusercontent.com/114842751/193752825-2dd155bb-cde0-4e90-8e01-5b4d183725eb.png)
- *Note: this may take awhile to sync with the VM and Azure portal, just give it time and try again till it shows results*
<br/>
<br/>

- Results should look like this: <br/>
![Screenshot 2022-10-04 040307](https://user-images.githubusercontent.com/114842751/193755506-6ecabdf1-9d11-4d6e-8a85-e0a833e1dbb0.png)
<br/>
<br/>

- Now we need to create columns for the fields that have raw data. So, expand one of the raw datas and right click. An option to "Extract fields from" should show, click on it. Then you will be brought to the Logs Custom Fields page where you will see a bunch of information. Where you see "latitude highlight the following and then a prompt to name the "Field Title" should appear as well as a "Field Type" fill in the following and then press "Extract" <br/>
![Screenshot 2022-10-04 041231](https://user-images.githubusercontent.com/114842751/193757226-b758ccce-35cc-4f5c-8315-98b30fe5e7df.png)
- *These next few parts are tedious so I will try to make it as simple as possible*
<br/>
<br/>

The same steps apply from the last example so I will provide the step by step with screenshots: <br/>
![Screenshot 2022-10-04 041524](https://user-images.githubusercontent.com/114842751/193757874-9485aa27-2080-428d-97e9-1b56ced59a13.png)
![Screenshot 2022-10-04 041637](https://user-images.githubusercontent.com/114842751/193757884-d1a90619-cd0b-44ff-91ed-a0262be2706f.png)
![Screenshot 2022-10-04 041726](https://user-images.githubusercontent.com/114842751/193758030-1c7fde76-26c6-477f-b8b1-d0ccf8931baa.png)
![Screenshot 2022-10-04 041943](https://user-images.githubusercontent.com/114842751/193758450-69084d23-cf65-4c41-a03e-629cd9b1e4f5.png)
![Screenshot 2022-10-04 042116](https://user-images.githubusercontent.com/114842751/193758729-82d148cf-d9fe-4b38-a037-37c2915d8f3d.png)
![Screenshot 2022-10-04 042341](https://user-images.githubusercontent.com/114842751/193759191-36fd2808-dd8c-4cb8-8b1c-e6503ada37bd.png)
![Screenshot 2022-10-04 042614](https://user-images.githubusercontent.com/114842751/193759663-d237e6b7-e476-41ef-b56e-e1424ea15e0d.png)
![Screenshot 2022-10-04 042817](https://user-images.githubusercontent.com/114842751/193760054-dd19dcdc-19ad-408f-ab01-7bd361fb71dc.png)
- *Sometimes you run into issues with spacing, in this case refer to the next screenshot:*
- *1: click the edit pencil refered in the screenshot. 2: Highlight the possible mistake and then press "Extract"*
![Screenshot 2022-10-04 043145](https://user-images.githubusercontent.com/114842751/193761064-45d82450-2249-4751-9489-6687249c5ed1.png)
![Screenshot 2022-10-04 043456](https://user-images.githubusercontent.com/114842751/193761398-5d22e3fb-2b95-4419-ba6a-e0f67e382049.png)
![Screenshot 2022-10-04 043652](https://user-images.githubusercontent.com/114842751/193761789-37d0fc9d-9751-48d8-bbb9-ca77a738eda2.png)
<br/>
<br/>

Just like that we are done with the Custom Log! <br/>
<br/>
<br/>

- Now run the Query again and you will notice that the custom columns you made are empty. Dont worry, they will fill in when more of the same failed login attempts happen. For now in Settings go back to "Custom logs": <br/>
![Screenshot 2022-10-04 044047](https://user-images.githubusercontent.com/114842751/193762434-cf18cda9-4f38-4570-9de2-716240da6ee8.png)
<br/>
<br/>

- Click on "Custom Fields"(This will show all the fields we just made when we customized the log): <br/>
![Screenshot 2022-10-04 044228](https://user-images.githubusercontent.com/114842751/193762769-b9edbaec-40f4-427a-8825-2c34b9feb140.png)
<br/>
<br/>

- Go back to Logs, and rerun the Query and now when you look through the custom columns you created and you will see all the information that you set and extracted: <br/>
![Screenshot 2022-10-04 044730](https://user-images.githubusercontent.com/114842751/193763779-57557427-cd8c-478c-800d-a45792998187.png)
<br/>
<br/>

- Now to set up the Map in Sentinel. So go back to Microsoft Sentinel and click on the honeypot you created: <br/>
![Screenshot 2022-10-04 045013](https://user-images.githubusercontent.com/114842751/193764388-2ba5dcdc-abbd-42de-84aa-668500e14814.png)
<br/>
<br/>

- Click on "Overview" and it will show how many failed RDP attempts have happened so far. Now click on "Workbooks":
![Screenshot 2022-10-04 045253](https://user-images.githubusercontent.com/114842751/193764893-5bcf2cc6-05b7-4e88-8b92-17e2d188b981.png)
<br/>
<br/>

- Click "Add workbook" <br/>
![Screenshot 2022-10-04 045350](https://user-images.githubusercontent.com/114842751/193765096-5896cf41-3ed1-48f3-92f9-7ef295761c1a.png)
<br/>
<br/>

- Click Edit, then click "+ Add", then "Add query": <br/>
![Screenshot 2022-10-04 045632](https://user-images.githubusercontent.com/114842751/193765693-f8da233a-0691-4c55-a1e5-0fd3489a8a51.png)
<br/>
<br/>

- In the Log Query you are going to type of copy and paste the following code: "FAILED_RDP_WITH_GEO_CL | summarize event_count=count() by SourceHost_CF, Latitude_CF, Longitude_CF, Country_CF, Label_CF, DestinationHost_CF". This will allow all logged RDP failures to appear in the query after it has been ran: <br/>
![Screenshot 2022-10-04 050916](https://user-images.githubusercontent.com/114842751/193768006-ddabf188-f256-4856-b4bf-54289357b468.png)
<br/>
<br/>

- Select "Visualization" and then select "Map": <br/>
![Screenshot 2022-10-04 051426](https://user-images.githubusercontent.com/114842751/193769043-57a551e5-f5a1-4742-bbf7-68c8208c104a.png)
<br/>
<br/>

- Then fill in the following then click "Apply": <br/>
![Screenshot 2022-10-04 051555](https://user-images.githubusercontent.com/114842751/193769406-07ee0cb2-0e18-481d-bc23-7c1582f52758.png)
![Screenshot 2022-10-04 051618](https://user-images.githubusercontent.com/114842751/193769409-2ec60ba4-e049-403a-9701-7f900349ac0d.png)
<br/>
<br/>

- Save the workbook and fill in the following: <br/>
![Screenshot 2022-10-04 052348](https://user-images.githubusercontent.com/114842751/193771012-1e9dc95d-00d5-4d11-9925-7bad458abc7b.png)
<br/>
<br/>

Congratulations! You have just completed the Lab!




