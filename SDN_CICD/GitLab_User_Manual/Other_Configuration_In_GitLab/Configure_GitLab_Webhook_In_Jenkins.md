# **6. Configure GitLab Webhook in Jenkins**



**What is a webhook?**

A Webhook is a mechanism to automatically trigger the build of a Jenkins
Project upon a commit pushed in a Git repository or any other event you
choose.

In order for builds to be triggered automatically by PUSH and PULL
REQUEST events, a Jenkins Web Hook needs to be added to each Git
repository. You need admin permissions on that repository.

First you need to create a new GitLab project or choose an existing one.
Then, go to Project-\> Settings-\> Webhooks

Then there's configurations from Jenkins side and from GitLab side.

## \# **Jenkins side configurations:**

-   Install GitLab Webhook plugin in Jenkins

-   In Jenkins job \> build trigger: Check the GitLab Webhook

<img src="images/7e5ec422ef2defccaed4f797f33ec6d2d68a91b4.png"
style="width:6.5in;height:3.16875in" />

-   Click on advanced and generate token code

<img src="images/22cf76e45109717ccd7670dfb504f3f4d690176b.png"
style="width:6.5in;height:3.22292in" />

Copy the secret token and paste it in some safe place for further use.
This key is not available again. If you lose the key again, we need to
generate the key and configure it in GitLab.

Then click on the apply and save button to save configuration.

## \# **GitLab side configurations:**

-   Go to repository settings \> Webhooks

-   Add a New Webhook

-   Add URL of the Jenkins project like this
    [http://172.29.145.204:8080/project/my_Project/](http://192.168.179.135:8080/project/my_maven_Project/)

-   Add the generated token code from Jenkins build trigger section

-   Save and test

<img src="images/86f2358fc1bbaff7b48a0aef3988ed1b8b3dab1a.png"
style="width:6.32212in;height:2.73958in" />

**There's a trick that must to be done to be created successfully**

-   Go to GitLab Admin Area \> Settings \> Network \> Outbound requests
    \> check on Allow requests to the local network from web hooks and
    services && Allow requests to the local network from system hooks \>
    Save Changes

<img src="images/3954ad7b8b115c4097356c944fb2673a74f1275e.png"
style="width:6.60417in;height:2.88932in" />

Finally, you can enter the Jenkins IP Address manually in (Local IP
addresses and domain names that hooks and services may access).

We are all done to integrate Jenkins and GitLab. Now every time a
developer commits a code to GitLab, our build will be triggered.

<img src="images/4c44cf5fae5f0ab0d9b6bcfd0be2d7ced9e71b8c.png"
style="width:6.42643in;height:4.45833in" />

This is how it will be looks like, you will notice (Started by GitLab
Push by Administrator)

So, When I pushed new updates to my project on GitLab, the Webhook that
i configured has been triggered the Jenkins job/project automatically.

**Referral links:**

<https://www.linkedin.com/pulse/how-configure-gitlab-webhook-jenkins-mohamed-elemam?trk=read_related_article-card_title>

<https://docs.gitlab.com/ee/integration/jenkins.html>



[<- Back to Manage GitLab Groups and Projects](../Manage_GitLab_Groups_And_Projects/Groups_And_Projects.md) - - - [Up to Main](../main.md) - - - [Ahead to SSH-Keys in GitLab ->](../Other_Configuration_In_GitLab/Configure_SSH_Keys_In_GitLab.md)




