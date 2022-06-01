**<u>Email Notification in Jenkins</u>**

<img src="images/f23a2b08df90a15cf0b989d6723f64d5b0b31b74.png"
style="width:5in;height:2.54167in" />

Jenkins provides you with an email notification service through which
you can report the build status and testing results to the team.

# **Why do we need email notifications in Jenkins?**

## **Problem Statement:**

-   Suppose the release of the application is scheduled at midnight. Now
    there is a problem with the application on the test server or the
    production servers. Also, there might be a case where the
    application is released and it goes down after a few hours. If the
    application, say for example Netflix is down even for a few minutes,
    this can result in the loss of millions of dollars. Also due to such
    errors, the project deadline might get extended.

# **Solution:**

<img src="images/3933733a18491aa2efc1301959a860a476fc1e23.png"
style="width:5in;height:2.625in" />

-   This problem was solved by an automation tool called
    [Jenkins](https://jenkins.io/). Jenkins has a service of Email
    Notifications to handle such situations.

-   If the build is not successful then the team of developers is
    notified about the status of the build. This can be done with the
    help of an Email plugin in Jenkins. **Plugins** are the primary
    means of enhancing the functionality of a **Jenkins** environment to
    suit organization- or user-specific needs.

-   Using the email plugin, you configure the email details of the
    concerned person who should be notified in case of build failure.

-   Once the developer is notified about the error, he then fixes it and
    again commits the code to GitHub. After this Jenkins again pulls the
    code from GitHub and prepares a fresh build.

-   Similarly, Jenkins can solve the problem of the application going
    down after the release, by notifying the concerned team, via email.

Now let us see how to send Email Notifications in Jenkins.

# **How To Send Email Notification In Jenkins?**

There are basically two ways to configure email notifications in
Jenkins.

1.  **Using Email Extension Plugin** — This
    [plugin](https://plugins.jenkins.io/) lets you configure every
    aspect of email notifications. You can customize things such as when
    to send the email, who receives it, and what the email says.

2.  **Using Default Email Notifier** — This comes with Jenkins by
    default. It has a default message consisting of a build number and
    status.

# **Email Extension Plugin**

## **Step 1: Log in to the Jenkins Homepage**

Go to Jenkins home page using the URL localhost:8080. The port number by
default is 8080. In my case, it is 9191. Sign in using your username and
password.

## **Step 2: Install Email Extension Plugin**

After that on the Jenkins homepage click on **Manage Jenkins-\> Manage
Plugins**. In the available tab search for Email Extension Plugin. If it
is found there, install it. If it is not found there, check for it in
the installed tab.

<img src="images/97d36bc5ca3685f3e25aa3209228a78ea5488f1d.png"
style="width:5in;height:0.98958in" />

## **Step 3: Configure System**

Now go to **Manage Jenkins-\> Configure System**. Here scroll down to
the email notification section. If you are using Gmail then type
smtp.gmail.com for the SMTP server. Click on Advanced and select Use
SMTP authentication. Enter your Gmail username and password. Select the
Use **SSL** option and enter the port number as **465**. Click on Apply
and then Save.

<img src="images/ed465978514851fb72875322a33de4afcd4c9058.png"
style="width:5in;height:2.53125in" />

## **Step 4: Create Jenkins Pipeline Job**

Now go to Jenkins homepage and create a new job. Name the job with
whatever name that you want and select pipeline. Click on OK.

Now in the pipeline section type the following code.

pipeline {  
agent anystages {  
stage('Ok') {  
steps {  
echo "Ok"  
}  
}  
}  
post {  
always {  
emailext body: 'A Test EMail', recipientProviders: \[\[$class:
'DevelopersRecipientProvider'\], \[$class:
'RequesterRecipientProvider'\]\], subject: 'Test'  
}  
}  
}

This pipeline runs in any Jenkins agent. It has a stage to sample. In
the post step, you can run any script you want. We have the mail sender
in it. Save it and run by clicking “Build Now” on the job menu. The
build will appear in the stage view.

<img src="images/ce604b63ff3bcddbe6aeab60715e6be69dcd6604.png"
style="width:5in;height:2.48958in" />

## **Step 5: View Console Output**

Click on Build Number “#1” and click on “Console Output” on the build
menu. The output will be like this:

<img src="images/0d83b5d584f60d4c5e154af104dcfa3fca31f00a.png"
style="width:5in;height:3.55208in" />

## **Step 6: Check Email.**

Open the mail id which we configured previously and check the post build
notification.

# **Default Email Notifier**

## **Step 1: Log in to the Jenkins Homepage**

Go to Jenkins homepage.

## **Step 2: Configure System**

Click on **Manage Jenkins-\>Configure System**. Here scroll down to the
Email Notification section. Now enter the details as the following image

<img src="images/b595ad1a9ff6ce617247b74983ad9c75466cdcd3.png"
style="width:5in;height:2.89583in" />

Once the mail configurations are set, you can test whether it is working
fine or not by checking the **Test configuration by sending a test
email**.

## **Step 3: Add post-build action to your project**

To allow your projects to send an email, you need to add **Post Build
Action** and select “**Email Notification** from the drop-down list.
This will provide you the below interface, where you can add a list of
email addresses that the email is required to be sent to.

<img src="images/9be9a752db52fe64757e96a3761f9795333b7eb6.png"
style="width:5in;height:1.11458in" />

## **Step 4: Build the project and check your email**

Now try running the project where you have added the email. If the build
fails you will get an email regarding the build failure.

<img src="images/704ac30053cfb90e08e1485f30c9bcf39d6860f1.png"
style="width:5in;height:1.75in" />

So, this is how you set up Email notifications in Jenkins.



[<- Back to Manage Jenkins users](../Manage_Jenkins_Users/Create_and_Manage_Users_In_Jenkins.md) - - - [Up to Main](../main.md) - - - [Ahead to Jenkins Jobs list ->](../Jenkins_Jobs/List_Of_Jobs.md)
