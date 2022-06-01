# Jenkins Overview

Jenkins is an open source continuous integration/continuous delivery and deployment (CI/CD) automation software DevOps tool written in the Java programming language. It is used to implement CI/CD workflows, called pipelines.

## Why Jenkins?
Jenkins is a software that allows continuous integration. Jenkins will be installed on a server where the central build will take place. The following flowchart demonstrates a very simple workflow of how Jenkins works.


Along with Jenkins, sometimes, one might also see the association of Hudson. Hudson is a very popular open-source Java-based continuous integration tool developed by Sun Microsystems which was later acquired by Oracle. After the acquisition of Sun by Oracle, a fork was created from the Hudson source code, which brought about the introduction of Jenkins.

## What is Continuous Integration?
Continuous Integration is a development practice that requires developers to integrate code into a shared repository at regular intervals. This concept was meant to remove the problem of finding later occurrence of issues in the build lifecycle. Continuous integration requires the developers to have frequent builds. The common practice is that whenever a code commit occurs, a build should be triggered.

## Jenkins Architecture

Here's how Jenkins elements are put together and interact:

- Developers commit changes to the source code, found in the repository.
- The Jenkins CI server checks the repository at regular intervals and pulls any newly available code.
- The Build Server builds the code into an executable file. In case the build fails, feedback is sent to the developers.
- Jenkins deploys the build application to the test server. If the test fails, the developers are alerted.
- If the code is error-free, the tested application is deployed on the production server.
- The files can contain different code and be very large, requiring multiple builds. However, a single Jenkins server cannot handle multiple files and builds simultaneously; for that, a distributed Jenkins architecture is necessary.

## What are the Jenkins Features?
Jenkins offers many attractive features for developers:

- Easy Installation
Jenkins is a platform-agnostic, self-contained Java-based program, ready to run with packages for Windows, Mac OS, and Unix-like operating systems.
- Easy Configuration
Jenkins is easily set up and configured using its web interface, featuring error checks and a built-in help function.
- Available Plugins
There are hundreds of plugins available in the Update Center, integrating with every tool in the CI and CD toolchain.
- Extensible
Jenkins can be extended by means of its plugin architecture, providing nearly endless possibilities for what it can do.
- Easy Distribution
Jenkins can easily distribute work across multiple machines for faster builds, tests, and deployments across multiple platforms.
- Free Open Source
Jenkins is an open-source resource backed by heavy community support.
As a part of our learning about what is Jenkins, let us next learn about the Jenkins architecture.

## Advantages of Using Jenkins
Jenkins is a powerful tool truly built and friendly for developers. Here are some of the most significant advantages of using Jenkins:

1. Free to Use
Jenkins is fully open-source and free to use. Since its development in 2011, it is the most preferred CI/CD tool used by developers in both early-stage startups and big organizations.

2. Rich Plugin Ecosystem
There are over a thousand different plugins that can be used to enhance the functionality of a Jenkins environment and suit the specific needs of an organization.

3. Easy Integration 
Jenkins can be easily integrated with a number of popular cloud platforms such as Google Cloud, Digital Ocean, Amazon EC2 and more.

## Disadvantages of Using Jenkins
Jenkins also has its own share of disadvantages. Here are some of the most common ones:

1. Developer Centric
Jenkins is more developer-centric and feature-driven. A person may need to have some sort of developer experience to use Jenkins.

2. Setting Change Issues
There are some issues (such as Jenkins not starting up) that you may face when you change the settings in Jenkins. These issues can come up when you install some plugins as well. Fortunately, Jenkins has a large user base so you can search online for a solution whenever you are faced with these issues.



[Up to main](../main.md) - - - [Ahead to Jenkins Installation->](../Installation/Jenkins_Installation.md)
