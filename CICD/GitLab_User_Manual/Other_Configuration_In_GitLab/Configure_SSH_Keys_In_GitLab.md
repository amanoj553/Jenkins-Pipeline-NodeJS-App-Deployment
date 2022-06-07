# **7. SSH keys to communicate with GitLab**

Git is a distributed version control system, which means you can work
locally, then share or *push* your changes to a server. In this case,
the server you push to is GitLab.

GitLab uses the SSH protocol to securely communicate with Git. When you
use SSH keys to authenticate to the GitLab remote server, you don’t need
to supply your username and password each time. Before generating ssh
keygen, you need to have Git installed in your system.

Before you create a key pair, see if a key pair already exists.

-   Go to your home directory.

<!-- -->

-   Go to the .ssh/ subdirectory. If the .ssh/ subdirectory doesn’t
    exist, you are either not in the home directory, or you haven’t used
    ssh before. In the latter case, you need to [generate an SSH key
    pair](https://docs.gitlab.com/ee/user/ssh.html#generate-an-ssh-key-pair).

## **Step 1:**

**Generate an SSH key pair**

If you do not have an existing SSH key pair, generate a new one:

-   Open a terminal.

<!-- -->

-   Run **ssh-keygen** followed by the key type and an optional comment.
    This comment is included in the .pub file that’s created. You may
    want to use an email address for the comment.

C:\\−ssh-keygen

It will prompt for 'Enter file in which to save the key
(//.ssh/id_rsa):', just type file name and press enter. Next a prompt to
enter password shows 'Enter passphrase (empty for no passphrase):'.
Enter some password and press enter. You will see the generated SSH key
as shown in the below image.

<img src="images/fcd78eb8b75240b30e276fad82cc58bbefed192c.png"
style="width:6.5in;height:3.20912in" />

## **Step 2:**

Now Login to the GitLab Account and on the top right side click on
**Avatar symbol** and select **Edit profile** option.

<img src="images/6cfd746f057c3f411704383d8082be074ad8d0be.png"
style="width:6.28125in;height:1.79277in" />

## **Step 3:**

To Create SSH Key, click on the SSH Keys tab on the left side of the
menu.

<img src="images/d6a9cf52bab6aa247ad82db51fec3350c22c38f9.png"
style="width:6.40816in;height:3.27083in" />

## **Step 4:**

Now Go to the server which communicate with GitLab. Goto the .ssh file
path under this folder we have id_rsa.pub file available.

$ cd .ssh

<img src="images/3e0b34932d5c5498ebfa7c87e565bb1484fc0be3.png"
style="width:6.55224in;height:4.57292in" />

## **Step 5:**

Next open the id_rsa.pub file, copy the SSH key and paste it in the
highlighted *Key* box as shown in the below image.

<img src="images/240641e10e9e2fd0e6bd1f821e0f273e53630d94.png"
style="width:6.5in;height:0.94792in" />

<img src="images/7376f03ef3d461c0c44404989a548b5547dd6049.png"
style="width:6.5151in;height:2.80963in" />

Here **Expiration date** is optional, if we want to give a particular
time period then that key valid up to mentioned time.

## **Step 6**:

Click on the *Add Key* button, to add SSH key to your GitLab. You will
see the fingerprint (it is a short version of SSH key), title and
created date as shown in the image below.

<img src="images/bf26cc15070aa241aaf1c1a17c12f550031ed638.png"
style="width:6.55208in;height:2.52528in" />

Now, SSH keys are generated successfully. We can able communicate with
server and GitLab without any credentials.

**Referral links:**

<https://docs.gitlab.com/ee/user/ssh.html>

<https://www.tutorialspoint.com/gitlab/gitlab_ssh_key_setup.htm>



[<- Back to Webhook configuration](../Other_Configuration_In_GitLab/Configure_GitLab_Webhook_In_Jenkins.md) - - - [Back to Main](../main.md)



