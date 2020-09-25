# QuizApp Overview and Deployment Guide

**Quiz App** is a gamification based PowerApp hosted on Microsoft Teams. It is designed to test an end user’s knowledge on Microsoft Teams, thereby facilitating learning and it also helps in providing insights to the organization on areas to drive further awareness. The quiz, pinned on Microsoft Teams, can be easily accessible from any device at any time.

It is a simple and interactive application and can be tailored for any of your internal Learning scenarios as well. The quiz is uniquely designed, in that, it randomly picks 10 questions from a large pool of questions, thereby ensuring that every user gets a unique experience. Questions are given along with four choices, and the user is provided an instant feedback whether he is right / wrong.

## Core Scenario
### Home: 
This is app landing page that is displayed to the users once they login to the Quiz App.
<p> <img src="images/image001.png" />

### View Instructions: 
On the home page user is asked to view the quiz instructions.
<p> <img src="images/image002.jpg" />
<br>End user can view quiz instructions and then clicking on “Take Quiz” will directly take them to questions screen.

### Take Quiz: 
When end-user clicks on the “Take Quiz” button, he navigates to questions screen. Each question presented on questions screen will be a multiple choice question where user can select the answer by clicking on radio button corresponding to the option. Feedback on correctness of the answer will be displayed on the questions screen to the user once he makes his choice and submits the chosen option.

### End Quiz: 
On submission of the quiz by clicking "Submit Quiz" button, Total Score of the user along with his email and full name will be displayed and same will also be recorded in a share point site.

## Deployment guide
### Prerequisites
To begin, you will need:
* Power Apps Studio
* SharePoint Online
* Office 365 Groups connector
* A copy of QuizApp zip package. Link to [QuizApp package](https://github.com/swatiarora11/QuizApp/blob/master/Deployment/QuizApp.zip)

### Step 1: Create SharePoint Team Site

From Sharepoint Online, create a **Team Site** named as **Quiz**.
<p> <img src="images/image003.png" />
<p> <img src="images/image004.png" />

### Step 2: Create SharePoint Lists

#### List1: QuizData (Question Bank for the quiz)
1. We will use an Excel file containing the questions to create this list. For this, download the Excel Template from the repository here - [Sample Quiz Data](https://github.com/swatiarora11/QuizApp/blob/master/Deployment/TeamsQuestionBank.xlsx). 
1. Navigate to the **Documents** document library folder in the Quiz team site and upload this excel document in the same.<p> <img src="images/image005.jpg" />
1. Open **Site Contents** on the **Quiz Team Site** and select **New >> List**.<p> <img src="images/image006.jpg" />
1. Enter the name of the List as **QuizData** and Select **From Excel** to import the list from the Excel file, saved in the **Documents** folder of the **Quiz Team Site**. Hit **Next** to continue.<p> <img src="images/image007.jpg" />
1. You will see a **Loading Tables** message on pressing **Next** and it will thereafter load the table as shown below.<p> <img src="images/image008.jpg" />
1. At this stage, we need to change the List Header fields as follows –
* Set _Option1_ to _Title_
* Set _SNo._ to _Number_
* Set _Question_ to _Multiple lines of text_.
<br><br>The columns should appear as shown below. Once you’re done with this, click **Create**.<p> <img src="images/image009.jpg" />
<br>Once created the **List** should look as shown below -<p> <img src="images/image010.png" />
7. Next, we need to rename the column name **Title** to **Option1**. To do this follow the screenshot below –<p> <img src="images/image011.jpg" /><p> <img src="images/image012.jpg" />
<br>Net Result should look as shown below -<p> <img src="images/image013.jpg" />
8. Select **Option1** column and Drag & Drop the column before **Option2** for better readability of the list.<p> <img src="images/image014.jpg" />
<br>The list should now look as below –<p> <img src="images/image015.jpg" />

#### List2: UserQuizData

1. Navigate to the **Quiz** SharePoint site via the url - _https://<TenantName>.sharepoint.com/teams/Quiz_ and click on the **New** button to create a new **List**.<p> <img src="images/image016.jpg" />
1. Add list name as **UserQuizData** and click **Create**. Please use this exact name for the list.
1. Add below columns under **UserQuizData** list. Please make sure to follow exact naming convention for the columns as mentioned below.<br>_**Note:** While creating the list, there is no need to add **Title** column, because SharePoint Online will automatically create that column_

Name of Column     	| Type                	| Comment
--------------------| ----------------------| ------------------------------------------------------------
Title				| Single line of text	| Auto generated by SharePoint. We will rename this column to **Email** in next step.
QIndex				| Number				| Serial Number
Question			| Multiple line of text	| Captures the Question attempted by the user.
SubmittedAnswer		| Single Line of text	| Captures the response to the question by the user.
Score				| Number				| Net score based on the answer to the question

4. Rename the **Title** column to **Email**.<p> <img src="images/image017.jpg" /><p> <img src="images/image018.jpg" /><br>Net Result will look as shown below –<p> <img src="images/image019.png" />

#### List3: UserQuizSummary

1. Navigate to the **Quiz** SharePoint site via the url - _https://<TenantName>.sharepoint.com/teams/Quiz_ and click on the **New** button to create a new **List**.<p> <img src="images/image016.jpg" />
1. Add list name as **UserQuizSummary** and click **Create**. Please use this exact name for the list.
1. Add below columns under **UserQuizSummary** list. Please make sure to follow exact naming convention for the columns as mentioned below.<br>_**Note:** While creating the list, there is no need to add **Title** column, because SharePoint Online will automatically create that column_

Name of Column     	| Type                	| Comment
--------------------| ----------------------| ------------------------------------------------------------
Title				| Single line of text	| Auto generated by SharePoint. We will rename this column to **Email** in next step.
Name				| Single line of text	| Captures the full name of the user.
Score				| Number 				| Score of the Quiz taken by User
Status				| Yes/No				| Status of Quiz is taken by the user
Time				| Number				| Time captured to attempt the Quiz in seconds

4. Rename the **Title** column to **Email**.<p> <img src="images/image017_1.jpg" /><p> <img src="images/image018.jpg" /><br>Net Result will look as shown below –<p> <img src="images/image019_1.png" />

#### Step 3: Import Package in Power Apps using zip file
1. Navigate to Power Apps https://make.powerapps.com/
1. Click on Apps in the left side pane and click on **Import canvas app**.<p> <img src="images/image020.jpg" />
1. Import the package zip file.
1. Click on the wrench icon present under **Action** label to change name of the app. Change name of the app to **QuizApp** and click on **Save**.<p> <img src="images/image021.jpg" />
1. Click on **Import** button at bottom.<p> <img src="images/image022.png" />
1. You will see a successful messsage after importing the app.

#### Step 4: Edit Data source
1. Click on **Open app** link when zip package is successfully imported. You will be redirected to PowerApps portal.
1. Using left side menu, navigate to **Open > Power Apps > QuizApp** which you have imported.
1. The app will request your permission to use all the listed data connections.<p> <img src="images/image023.png" />
1. Go to left menu > click **View** and select **Data sources**.
<br>**VIMP -** _Delete the 3 existing lists – **QuizData, UserQuizData and UserQuizSummary** as shown below._ These will be reimported in the next step.<p> <img src="images/image024.jpg" />
1. Search and select **SharePoint** site - _https://<TenantName>.sharepoint.com/teams/Quiz_ and click _Connect_<p> <img src="images/image025.jpg" />
1. Enter the SharePoint URL created in above step.<p> <img src="images/image026.jpg" />
1. Select **QuizData, UserQuizData, UserQuizSummary** check boxes and click **Connect**.<p> <img src="images/image027.jpg" />
1. Make the App personal by also adding your Company Name and Logo to the App. Select the Label2_4 in the app and edit the **Text** field as shown –<p> <img src="images/image028.png" />
<br>You may also insert a small image / logo to be placed next to the organization name –<p> <img src="images/image029.png" />

#### Step 5: Set Quiz Active Time Duration
1. To set the quiz active time, Navigate to **Welcome Screen** in the **Edit App** page and select **On Visible** Property of the **Welcome Screen** from the top left dropdown.<p> <img src="images/image029_1.jpg" />
1. Set **QuizStartTime** to date and time when quiz should be live in IST **mm/dd/yyyy hh:mm AM/PM** format.<p> <img src="images/image029_2.jpg" />
1. Set **QuizEndTime** to date and time when quiz should end in IST **mm/dd/yyyy hh:mm AM/PM** format.<p> <img src="images/image029_3.jpg" />
1. Now **QuizApp** is ready to be published and shared within your organization.

#### Step 6: Share Power Apps
1. Once the required changes are made in above steps, click on **File >> Save** the app. Thereafter **Publish** the app.
1. Once the app is published, Admin needs to share the app to all individuals who will be using the app. You will get a Share option as soon as you publish the app and if you wish to share the app at this time, **jump to point 6**. Else proceed to **Point 3**.
1. Open https://make.preview.powerapps.com/
1. Go to Apps menu in the left menu bar and you will be able to see the app you have imported.
1. Click on 3 dots (Options) for your app and click on **Share**.<p> <img src="images/image030.jpg" />
1. Enter the **group name** containing the users in the popup and click on **Share**. You can also add additional members if needed. This permission is required to grant access to the **QuizApp**.<p> <img src="images/image031.jpg" />

#### Step 7: Export Teams Package
1. Open https://make.preview.powerapps.com/
1. Go to Apps menu in the left menu bar and you will be able to see the app you have imported.
1. Click on 3 dots (Options) for your app and click on **Add to Teams**.<p> <img src="images/image032.jpg" />
1. Click on **Download App** in the popup to download a zip package.

#### Step 8: Adding App to Teams via Teams Admin Center
1. We will now pin the app to the Teams App for all users. This can be done via the Teams Admin Center.<p> <img src="images/image072.jpg" /><p> <img src="images/image073.jpg" />
<br>Net result once upload is complete should be – Admin can easily find the **Quiz App** under the **Manage Apps** tab, as shown below<p> <img src="images/image074.jpg" />
<br>_**NOTE – Ensure that Custom App policy permission has been enabled under Permission Policies.**_<p> <img src="images/image075.png" />
1. Next add this App to the **App Setup Policies**, which in turn will make the app visible to all users in the Teams user interface. To add this for all users, select the Global Policy.<p> <img src="images/image076.jpg" /><p> <img src="images/image077.jpg" />
1. Now set the sequence to make the app visible to each user. We recommend to pin the app in the top 5, so that it is easily visible to end users on each client. Hit **Save** to make this change.<p> <img src="images/image079.jpg" />
<br>That’s it! You will now see the Quiz App pinned on every user’s Teams App experience and you can run the quiz successfully.

## How to Obtain Quiz Results
1. Post the quiz deadline, navigate to the **UserQuizSummary** list created in above steps, in the **Quiz Team Site**.
1. Select **Export to Excel** option. This will download a **query.iqy** file. Open this file and follow the steps to obtain the Excel list with the quiz results.<p> <img src="images/image080.png" /><p> <img src="images/image081.jpg" /><p> <img src="images/image082.png" />
<br>**Important Note –**
* The Time field shows the time in **seconds** format.
* The columns which show 36000 secs indicate that a user has closed / refreshed the app, while taking the quiz, hence may be disqualified. Make sure to remove these user entries by Removing Duplicates.
3. **Finding the Winner -**
<br>One of the approaches to get the winner is by using a **Custom Sort** on the final data (post removing Duplicates).<p> <img src="images/image083.jpg" />
<br>**Sort condition –**
* Score – Largest to Smallest; and
* Time – Smallest to Largest
<p> <img src="images/image084.png" />
<br>Final Winners - Pick top 3 or 5 winners, as per your choice.
<p> <img src="images/image085.png" />


 