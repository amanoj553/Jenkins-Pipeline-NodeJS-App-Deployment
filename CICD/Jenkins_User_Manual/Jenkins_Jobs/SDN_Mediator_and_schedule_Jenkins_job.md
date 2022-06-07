# SDN_Mediator_Jenkins_job

Table of contents:

1.  First configure **server group centers** and **servers list** in
    Jenkins **configure system** section

2.  After configuration, we have to create the **free style** project in
    Jenkins Dashboard.

## 1. First configure **server group centers** and **servers list** in
Jenkins **configure system** section.


Note: Before we add group centers and server list we have to make SSH
connection between these servers with Jenkins server.

**Configure server group centers:**

In **Jenkins Dashboard** left hand side click on the **Manage Jenkins**
and Under **system configuration** select **configure system**.

Goto the **server group center** and add **server group list** like
below screenshot.

<img src="images/9cd45e23914318436026563b7baca8f607b2fc39.png"
style="width:6.4375in;height:2.87005in" />

Then click on the save button to save the server group list.

**Configure servers list:**

After creating server group centers then Goto the same configure system
and Goto the servers list sections and add server details according to
group of servers earlier we added.

<img src="images/a589a3571bad08f0826455ed1e3a38a857426bc8.png"
style="width:6.58654in;height:2.85417in" />

## 2. Create the **free style project** in Jenkins Dashboard

In Jenkins Dashboard, left hand side menu click on the **New Item.**

<img src="images/7246e5aea727594cb60463e39214d82c0e472df7.png"
style="width:6.54167in;height:1.98976in" />

Then enter the Item name (Job name), select Freestyle Project and click
on ok button to create Freestyle project in Jenkins.

<img src="images/19264d1f2526b41da734224603dae44deabdedeb.png"
style="width:6.37295in;height:3.23958in" />

Then open the previously created freestyle project and under **Build
section** select **Remote shell** and select which server we have to
execute Jenkins job.

<img src="images/c596400fc4eb51096fdf91710b739e21ce67c7af.png"
style="width:6.5in;height:3.65625in" />

Then add the commands whatever we have to perform on target server and
click on apply, save button to save the job configurations.

After saving the Job configuration under job section left hand side
menu, we have **built now** option available click on this to **build
the Jenkins Job** as per our configuration.

<img src="images/a5090b35133836b775a1cd683459f91e12b80ffd.png"
style="width:6.17225in;height:2.6875in" />

After building the Jenkins job we can check the Job console output by
following way in Job section.

<img src="images/3c1c1312b4cab0372e8c544a02bc004181b9b83b.png"
style="width:6.1583in;height:3.32292in" />

Here we are looking at the Job build status.

<img src="images/89f2c1d03f0326f80477b156b4dc9c88f92d0333.png"
style="width:6.36458in;height:2.58561in" />

# Scheduled_Jenkins_Jobs

**Instead of running a job based on an event, you may want to run it at
specific times**. For example, if an application build needs a
significant amount of system resources, you may only want to run it
overnight so that your build systems are free for your development teams
during the day.

Scheduling Jobs are created for daily, Nightly and weekly builds.

As per our requirement we scheduled Jenkins jobs.

In our Project we configured scheduled jobs for running sanity and
extended sanity test cases on a daily basis.

## **Create the free style project in Jenkins Dashboard**

In Jenkins Dashboard, left hand side menu click on the **New Item.**

<img src="images/7246e5aea727594cb60463e39214d82c0e472df7.png"
style="width:6.5in;height:1.97708in" />

Then enter the Item name (Job name), select Freestyle Project and click
on ok button to create Freestyle project in Jenkins.

<img src="images/19264d1f2526b41da734224603dae44deabdedeb.png"
style="width:6.37295in;height:3.23958in" />

Then open the previously created freestyle project and under **Build
Trigger section** select **Build periodically** and schedule the time
for daily auto running job.

<img src="images/0001ccacb546cccd160dae262f0ba1dcf2943714.png"
style="width:6.55242in;height:3.38542in" />

Goto the **Build section** select **Remote shell** and select which
server we have to execute Jenkins job.

<img src="images/c596400fc4eb51096fdf91710b739e21ce67c7af.png"
style="width:6.5in;height:3.65625in" />

Then add the commands whatever we have to perform on target server and
click on apply, save button to save the job configurations.

After saving the Job configuration under job section left hand side
menu, we have **built now** option available click on this to **build
the Jenkins Job** as per our configuration.

<img src="images/a5090b35133836b775a1cd683459f91e12b80ffd.png"
style="width:6.17225in;height:2.6875in" />

After building the Jenkins job we can check the Job console output by
following way in Job section.

<img src="images/3c1c1312b4cab0372e8c544a02bc004181b9b83b.png"
style="width:6.1583in;height:3.32292in" />

Here we are looking at the Job build status.

<img src="images/89f2c1d03f0326f80477b156b4dc9c88f92d0333.png"
style="width:6.36458in;height:2.58561in" />

Here once we configured scheduling Jenkins job it builds automatically
as per mentioned timings.

<img src="images/dff698710985897630d6970d9acd9263087b481e.png"
style="width:6.40625in;height:5.2985in" />



[<- Back to Pipeline Job For Application Deployment](../Jenkins_Jobs/SDN_Application_Deployment_Through_CI-CD.md) - - - [Up to Main](../main.md) - - - [Ahead to Jenkins PollSCM Jobs ->](../Jenkins_Jobs/Jenkins-pollSCM-PipelineJob.md)
