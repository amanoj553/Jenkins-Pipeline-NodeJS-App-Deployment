# Configured Poll SCM for Jenkins Pipeline Job

**Required configurations:**

## From GitHub side:

1.  Login to GitHub

2.  Generate personal Access token

    1.  After login into GitHub on the right side click on Avathara
        symbol and click on settings

> <img src="images/27dfc2e81387c14613a1ec2a99840a662094edf5.png"
> style="width:4.3125in;height:5in" />

2.  Then in left side panel scroll down and select Developer settings

> <img src="images/4669f91812a818dfdd5634eada77f89bb3413ba6.png"
> style="width:5in;height:2.125in" />

3.  Then in left side panel click on personal Access tokens

> <img src="images/ac30b22aa65d4e0109d08eeaf3559c4f01d97b90.png"
> style="width:5in;height:1.39583in" />

4.  In pop up page select generate new token and fill the following
    details

> <img src="images/d168ab0e0d83814cdd1bd7df19a52201b86664a9.png"
> style="width:5in;height:1.19792in" />

5.  Fill in the **Note** filed for which purpose we generate token, add
    **Expiration** date and select **Scopes** which are required for our
    token.

> Then click on Generate token which is available below once you fill in
> all the required details.
>
> <img src="images/821030773f18573bb36257aebaba8293ea6b224e.png"
> style="width:5in;height:2.19792in" />

6.  Copy the generated token and place it somewhere for further usage
    (token disappears once save the token).

> <img src="images/23fa4249fba9deff144c063b43585d07745f7cdc.png"
> style="width:5in;height:1.33333in" />

7.  If you’ve lost or forgotten this token, you can regenerate it, but
    be aware that any scripts or applications using this token will need
    to be updated.

## From Jenkins' side:

1.  First Login to Jenkins

2.  Add GitHub credentials in Jenkins

In Jenkins Dashboard on left side panel click on ==\> Manage Jenkins

<img src="images/566ffa36c54eef46dacee40a339337c4f114c2ab.png"
style="width:3.35417in;height:5in" />

Then scroll down page under Security section ==\> click on manage
credentials

<img src="images/ccf6f2afd0333a4cb79e4a4a81588ab8f0dd5e76.png"
style="width:5in;height:1.66667in" />

Drop down the menu and select Jenkins shown Under Stores scoped to
Jenkins section below.

<img src="images/3ac26ad8b86a8a3fb282db56c7d191a2d378a144.png"
style="width:5in;height:0.95833in" />

Click on Global credentials (unrestricted)

<img src="images/0580bd8b848920abad2941d1aa26b94b011ed10e.png"
style="width:5in;height:0.9375in" />

Then on left hand side menu click on Add Credentials

<img src="images/e955ec108ffedc9dfa922e0d15f911ee66b87ebb.png"
style="width:5in;height:1.32292in" />

Add below credentials to each section:

**Kind section:** Username with password

**Scope section**: Global (Jenkins, nodes, items, all child items etc.)

**Username:** Add GitHub Username

**Password:** Instead of Add GitHub Password add Personal Access token
which was generated earlier.

**Description section:** add any name for reference.

Then click on the ok button to save GitHub credentials on Jenkins
server.

<img src="images/94b5e10870c4296c6981c6cfe5c44b5b14801788.png"
style="width:5in;height:2.04167in" />

3.  After creating credentials follow below steps for creating Jenkins
    Pipeline job

In Jenkins Dashboard on left side panel click on ==\> New Item.
<img src="images/daca9e90bdaa42342768e8a22ce57bf22055c6b2.png"
style="width:5in;height:1.94792in" />

Enter job name with respect to Application \> Choose Pipeline \> Click
OK.

<img src="images/93f3df5d32f5ab8c964f4eb7d661aa9e78716293.png"
style="width:5in;height:2.38542in" />

After clicking OK. Goto Build Triggers section ==\> select PollSCM ==\>
In Schedule section give the time period depends on repo commit changes
build periodically.

<img src="images/0e5b34c7e5a54809b72d0f2c9e6b5924b2c6b3bd.png"
style="width:5in;height:2.07292in" />

Goto the Pipeline Section and add below pipeline script and click on
apply and save buttons to save Jenkins Pipeline job.

<img src="images/ef757cfbe17bd314f6a43844a0b67d5801d687c3.png"
style="width:5in;height:2.33333in" />

**Note**: if we are cloning Private repo we require GitHub credentials
so, we need to add in Pipeline source stage along with credentials. Not
Required credentials for Public Repo cloning in Pipeline Source stage.

Now the Pipeline Job has been configured successfully and it will run
according to schedule time when the commit changes happen in repository
with Particular branch.



[<- Back to Jenkins Mediator and scheduled Jobs](../Jenkins_Jobs/SDN_Mediator_and_schedule_Jenkins_job.md) - - - [Up to Main](../main.md) - - - [Ahead to Sample Jenkinsfiles ->](../Jenkins_Jobs/Jenkinsfile.md)
