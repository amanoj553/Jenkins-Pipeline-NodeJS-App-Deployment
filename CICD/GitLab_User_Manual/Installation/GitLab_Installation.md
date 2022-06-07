# 2. GitLab Installation

**<u>GitLab installation steps</u>**

## **<u>For ubuntu</u>**

sudo apt upgrade -y  
sudo apt install -y ca-certificates curl openssh-server

**For download GitLab packages:**

curl
<https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh>
\| sudo bash

**For installing GitLab package:**

sudo apt-get install gitlab-ce  
**Updating external URL with port number:**

sudo vim /etc/gitlab/gitlab.rb

**Add bellow step in the file:**

external_url '<http://10.40.0.36:8081>'

Then save the file: **esc:wq!**

**Reconfigure the GitLab configuration:**

sudo gitlab-ctl reconfigure

**Starting the GitLab service:**

sudo gitlab-ctl start  
sudo gitlab-ctl status

**After Installing GitLab we create root user (admin):**

gitlab-rails console -e production

user = User.where(id: 1).first

user.password = 'welcome01'

user.password_confirmation = 'welcome01'

Here

user: **root** and Password: **welcome01**

## **<u>For Redhat</u>**

**For download GitLab packages:**

sudo wget -e use_proxy=yes -e https_proxy=10.1.17.85:8080
<https://packages.gitlab.com/gitlab/gitlab-ce/packages/el/8/gitlab-ce-14.6.0-ce.0.el8.x86_64.rpm/download.rpm>

**For installing GitLab package:**

sudo yum localinstall download.rpm

**Updating external URL with port number:**

sudo vi /etc/gitlab/gitlab.rb

Add bellow step in the file:

external_url '<http://10.40.0.36:8081>'

Then save the file: **esc:wq!**

**Reconfigure the GitLab configuration:**

sudo gitlab-ctl reconfigure

**Starting the GitLab service:**

sudo gitlab-ctl start

sudo gitlab-ctl status

**After Installing GitLab we create root user (admin):**

gitlab-rails console -e production

user = User.where(id: 1).first

user.password = 'welcome01'

user.password_confirmation = 'welcome01'

Here

user: **root** and Password: **welcome01**

**Reference links:**

<https://fnote.medium.com/jenkins-moving-from-one-server-to-another-9a5dea1fa3f2>

<https://computingforgeeks.com/how-to-install-and-configure-gitlab-on-centos-rhel/>




[<- Back to GitLab-versioning-with-VisualStudiocode](../GitLab_Overview/GitLab-versioning-with-VisualStudiocode.md) - - - [Up to Main](../main.md) - - - [Ahead to Manage GiLab Users->](../Manage_GitLab_Users/Manage_Users.md)
