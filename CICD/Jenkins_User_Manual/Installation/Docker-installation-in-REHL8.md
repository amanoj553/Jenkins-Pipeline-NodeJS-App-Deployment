# Docker installation in REHL8

**1.  Adding the repository**

sudo dnf config-manager
--add-repo=https://download.docker.com/linux/centos/docker-ce.repo

**2.  verify that the repository has been enabled**

sudo dnf repolist -v

verify the output as it is below.

Repo-id : docker-ce-stable

Repo-name : Docker CE Stable - x86_64

Repo-revision: 1549905809

Repo-updated : Mon 11 Feb 2019 06:23:29 PM CET

Repo-pkgs : 30

Repo-size : 618 M

Repo-baseurl : https://download.docker.com/linux/centos/7/x86_64/stable

Repo-expire : 172,800 second(s) (last: Mon 18 Feb 2019 10:23:54 AM CET)

Repo-filename: /etc/yum.repos.d/docker-ce.repo

**3.  Use below command to install the latest docker**

sudo dnf install docker-ce

**4.  Install the latest available containerd.io**

sudo dnf install containerd.io

**5.  Start and enable the docker daemon**

sudo systemctl enable --now docker

**6.  confirm that the daemon is active and it is enabled at boot, by
running below command**


systemctl is-active docker

active

systemctl is-enabled docker

enable

**Reference link:**

https://linuxconfig.org/how-to-install-docker-in-rhel-8




[<- Back to Jenkins Installation](../Installation/Jenkins_Installation.md) - - - [Up to Main](../main.md) - - - [Ahead to Manage Jenkins Users ->](../Manage_Jenkins_Users/Create_and_Manage_Users_In_Jenkins.md)
