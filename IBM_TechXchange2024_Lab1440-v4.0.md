![A picture containing text, font, graphics, logo Description
automatically generated](./images/media/image1.jpg)

**Amplify your Integration Middleware with DevOps: The IBM DevOps Deploy
Way**

Session 1440

Lab Exercise Guide

Rafael de Oliveira Osorio

Learning Content Development, Automation Software

rosorio@br.ibm.com

Randall Langehennig

Solution Architect, Product Manager

rlange@ibm.com

**Notices and disclaimers**

© 2024 International Business Machines Corporation. No part of this
document may be reproduced or transmitted in any form without
written permission from IBM.

**U.S. Government Users Restricted Rights — use, duplication or
disclosure restricted by GSA ADP Schedule Contract with IBM.**

This document is current as of the initial date of publication and may
be changed by IBM at any time. Not all offerings are available in every
country in which IBM operates.

Information in these presentations (including information relating to
products that have not yet been announced by IBM) has been reviewed for
accuracy as of the date of initial publication and could include
unintentional technical or typographical errors. IBM shall have no
responsibility to update this information.

**This document is distributed “as is” without any warranty, either
express or implied. In no event, shall IBM be liable for any damage
arising from the use of this information, including but not limited to,
loss of data, business interruption, loss of profit or loss of
opportunity.** IBM products and services are warranted per the terms and
conditions of the agreements under which they are provided. The
performance data and client examples cited are presented for
illustrative purposes only. Actual performance results may vary
depending on specific configurations and operating conditions.

IBM products are manufactured from new parts or new and used parts.  
In some cases, a product may not be new and may have been previously
installed. Regardless, our warranty terms apply.”

**Any statements regarding IBM's future direction, intent or product
plans are subject to change or withdrawal without notice.**

Performance data contained herein was generally obtained in a
controlled, isolated environments. Customer examples are presented as
illustrations of how those customers have used IBM products and the
results they may have achieved. Actual performance, cost, savings or
other results in other operating environments may vary. 

References in this document to IBM products, programs, or services does
not imply that IBM intends to make such products, programs or services
available in all countries in which IBM operates or does business. 

Workshops, sessions and associated materials may have been prepared by
independent session speakers, and do not necessarily reflect the views
of IBM. All materials and discussions are provided for informational
purposes only, and are neither intended to, nor shall constitute legal
or other guidance or advice to any individual participant or their
specific situation.

It is the customer’s responsibility to ensure its own compliance
with legal requirements and to obtain advice of competent legal counsel
as to the identification and interpretation of any relevant laws and
regulatory requirements that may affect the customer’s business and any
actions the customer may need to take to comply with such laws. IBM does
not provide legal advice or represent or warrant that its services or
products will ensure that the customer follows any law.

**Notices and disclaimers (Continued)**

Questions on the capabilities of non-IBM products should be addressed to
the suppliers of those products. IBM does not warrant the quality of any
third-party products, or the ability of any such third-party products to
interoperate with IBM’s products. **IBM expressly disclaims all
warranties, expressed or implied, including but not limited to, the
implied warranties of merchantability and fitness for a purpose.**

The provision of the information contained herein is not intended to,
and does not, grant any right or license under any IBM patents,
copyrights, trademarks or other intellectual property right.

IBM, the IBM logo, and ibm.com are trademarks of International Business
Machines Corporation, registered in many jurisdictions worldwide. Other
product and service names might be trademarks of IBM or other companies.
A current list of IBM trademarks is available on the Web at “Copyright
and trademark information” at:
[www.ibm.com/legal/copytrade.shtml](http://www.ibm.com/legal/copytrade.shtml).

**Table of Contents**

[1 Introduction 5](#introduction)

[1.1 Lab Environment Architecture 5](#lab-environment-architecture)

[1.2 What is App Connect Enterprise (ACE)
6](#what-is-app-connect-enterprise-ace)

[1.3 What is IBM DevOps Deploy 6](#what-is-ibm-devops-deploy)

[1.4 What is IBM DevOps Test Hub 7](#what-is-ibm-devops-test-hub)

[2 Getting Started 9](#getting-started)

[2.1 How to Connect to the Lab 9](#how-to-connect-to-the-lab)

[3 Lab Exercises 11](#lab-exercises)

[3.1 Developing an IBM ACE broker archive using the IBM App Connect
Enterprise Toolkit
11](#developing-an-ibm-ace-broker-archive-using-the-ibm-app-connect-enterprise-toolkit)

[3.1.1 Overview 11](#overview)

[3.1.2 Workbook steps 11](#workbook-steps)

[3.2 Setup a Jenkins CI Pipeline to Automate Build
17](#setup-a-jenkins-ci-pipeline-to-automate-build)

[3.2.1 Overview 17](#overview-1)

[3.2.2 Workbook Steps 18](#workbook-steps-1)

[3.3 Review the Emerald eStore Application in IBM DevOps Deploy
30](#review-the-emerald-estore-application-in-ibm-devops-deploy)

[3.3.1 Overview 30](#overview-2)

[3.3.2 Workbook steps 31](#workbook-steps-2)

[3.4 Work with the emerald-ACE-BAR Component in Deploy
32](#work-with-the-emerald-ace-bar-component-in-deploy)

[3.4.1 Overview 32](#overview-3)

[3.4.2 Workbook steps 32](#workbook-steps-3)

[3.5 Deploy the ACE Broker Archive using IBM DevOps Deploy to DEV
44](#deploy-the-ace-broker-archive-using-ibm-devops-deploy-to-dev)

[3.5.1 Overview 44](#overview-4)

[3.5.2 Workbook steps 44](#workbook-steps-4)

[3.6 Promote the Emerald Components to the QA Environment
51](#promote-the-emerald-components-to-the-qa-environment)

[3.6.1 Overview 51](#overview-5)

[3.6.2 Workbook steps 51](#workbook-steps-5)

[3.7 Publishing a Product to API Connect using IBM DevOps Deploy
61](#publishing-a-product-to-api-connect-using-ibm-devops-deploy)

[3.7.1 Overview 61](#overview-6)

[3.7.2 Workbook steps 62](#workbook-steps-6)

[4 Wrapping Things Up 74](#wrapping-things-up)

[4.1 Lab Re-Cap 74](#lab-re-cap)

# Introduction

The purpose of the IBM DevOps Hands On workshop is to provide a
high-level overview on how to achieve end-to-end automation in your
DevOps pipelines to ensure good quality code is progressing from your
lower environments all the way to your production environment. The focus
will be to highlight App Connect Enterprise (ACE) and API Connect
(APIC).

In this lab, you will be working with these two primary IBM DevOps
solutions:

  - IBM DevOps Deploy (formerly known as IBM UrbanCode Deploy)

  - IBM DevOps Test Hub

Working with a container-based application called Emerald eStore, you
will gain an understanding of IBM DevOps Deploy and how to configure and
deploy the Emerald eStore application which includes an ACE broker
archive and an API Connect Product you will publish to a catalog. You
will also learn how to configure automated test execution using IBM
DevOps Test Hub in your automated processes.

This lab will provide an example of how you can leverage gates in IBM
DevOps Deploy for governance, call automated tests (could include
integration, functional, and performance tests) following an automated
deployment to track quality, and initiate releases to your target
environments.

## Lab Environment Architecture

The high-level architecture for the environment includes three different
servers as shown below:

![A screenshot of a computer Description automatically
generated](./images/media/image2.png)

The main system we will utilize for our labs is the RedHat (rhel8) host
found in the middle of the screen. You will connect to this host to
follow the steps in the labs. One server image hosts the IBM DevOps
Deploy Server and Agent. Finally, the last server image hosts the IBM
DevOps Test Hub installation.

## What is App Connect Enterprise (ACE)

IBM App Connect Enterprise combines the existing industry-trusted
technologies of IBM Integration Bus with cloud-native technologies to
deliver a platform that supports the full breadth of integration needs
across a modern digital enterprise.

You can use IBM App Connect Enterprise to connect applications together,
regardless of the message formats or protocols that they support. This
connectivity means that your diverse applications can interact and
exchange data with other applications in a flexible, dynamic, and
extensible infrastructure. IBM App Connect routes, transforms, and
enriches messages from one location to any other location.

By using the IBM App Connect Enterprise Toolkit, you can develop
integration solutions and deploy them to IBM Cloud Pak for Integration,
the dedicated runtime of IBM App Connect Enterprise software, and to IBM
App Connect Enterprise as a Service. The labs that follow will make use
of this toolkit to complete our tasks.

## What is IBM DevOps Deploy

IBM DevOps Deploy is an application-release solution that infuses
automation into the continuous delivery and continuous deployment
(CI/CD) process and provides robust visibility, traceability and
auditing capabilities.

IBM DevOps Deploy provides the following capabilities:

  - **Integrations that replace custom scripting**

> Integrations with technologies such as Jenkins, Kubernetes, Microsoft,
> ServiceNow and IBM® WebSphere® make processes more robust and easier
> to design.

  - **Scalable distributed automation**

> Meet enterprise requirements with an architecture designed to scale —
> providing high availability, horizontal scalability and tight
> security.

  - **Visual deployment modeling**
    
    Model cloud environments in a simple graphical editor to deploy your
    applications to public, private and hybrid clouds.

  - **Inventory control**

> Track what resides where with visibility into your applications,
> environments and configurations.

  - **Quality gates and approvals**

> Ensure that only application-component versions that meet quality
> criteria are promoted across test environments en route to production.

  - **Coordination of multicontainer deployments**

> Employ industry-leading release automation capabilities for the
> container world.

  - **Rapid migration to the cloud**

> UrbanCode Deploy is available as a container and certified to work
> with Red Hat OpenShift.

## What is IBM DevOps Test Hub

The IBM DevOps Test Hub application (formerly known as IBM Rational Test
Automation Server) brings together test data, test environments, and
test runs and reports into a single, web-based browser for testers and
non-testers.

The solution provides the following capabilities:

  - **Web-based continuous testing platform**

> IBM DevOps Test Hub is a web-based continuous testing platform built
> on modern, cloud native technologies that enables test teams to run a
> breadth of tests that includes API, functional, and performance tests.

  - **Role-based access and security**

> Security is a key concern for IBM clients and therefore, DevOps Test
> Hub brings a comprehensive, role-based access control scheme to the
> server with project owners assigning key permissions (by using roles)
> for specific members. For example, managing test data or working with
> secrets such as passwords.

  - **Running of tests from the server by using Docker containers**
    
    The DevOps Test Hub solution enables direct running of tests from
    the browser by using transient Docker containers.

  - Connected agents for existing performance agents.
    
    Agent owners can connect existing performance agents to the server
    and add them to a project for running schedules and Accelerated
    Functional Testing (AFT) Suites on the current infrastructure.

  - **Project overview statistics**
    
    The Overview page for IBM DevOps Test Hub offers you a quick, simple
    view on the state of testing for your projects.

  - **Test data authoring**
    
    Beyond the concept of a project held in a Git repository for a
    simple location of tests and related assets, you can do full
    concurrent editing of test data sets directly from DevOps Test Hub.
    This true multi-user capability enables team members to collaborate
    more easily as well as try out data changes without impacting the
    rest of the team. When satisfied with the results, team members can
    push their changes.

  - **Integration with DevOps tools**
    
    You can integration DevOps Test Hub with various popular DevOps
    tools like Jenkins, DevOps Deploy, or Microsoft Azure DevOps to get
    more value from your DevOps pipelines. You can configure an IBM
    DevOps Deploy process that automatically triggers test cases and
    have those test insights set a status to indicate that the tests
    passed or failed.
    
    DevOps Test Hub also integrates with Jira for defect tracking and
    GitHub for software source management and version control.

# Getting Started

## How to Connect to the Lab

Follow these instructions to connect to the lab environment.

1.  On your laptop, start your Firefox browser.

2.  Click on the link to your environment that has been assigned to you.
    For example:
    
    https://te-ilo.learninglabs.ibm.com/events/techxchange/1676\_A\#
    
    You will see a screen that looks like this:
    
    ![](./images/media/image3.png)

3.  Enter your email address and click the Login button (as shown
    above).
    
    You should see the screen below:
    
    ![A screenshot of a computer Description automatically
    generated](./images/media/image4.png)

4.  Click on the “Launch Lab” button. You will see the following screen:

> ![A screenshot of a computer Description automatically
> generated](./images/media/image5.png)

5.  Click on the RedHat or ‘rhel8’ screen as shown above. This will
    launch the console we will be using for the labs.
    
    ![A screenshot of a phone Description automatically
    generated](./images/media/image6.png)

6.  Click on the screen and you will see a login for the ‘sysadmin’
    user. Provide a password of “**Passw0rd**” and press Enter.

7.  You are good to proceed to the first lab\!

# Lab Exercises

## Developing an IBM ACE broker archive using the IBM App Connect Enterprise Toolkit

### Overview

In this lab we will explore our IBM App Connect Enterprise (ACE)
development capabilities. We will first explore the use of the IDE
Tookit to create and test a broker archive (BAR).

This toolkit is called the “IBM App Connect Enterprise Toolkit” as shown
below:

![A blue and white background with text Description automatically
generated](./images/media/image7.png)

Afterwards, we will look at an example pipeline that can be used to
automate the build, unit test, and ultimately the deploy of the broker
archive to your target environments.

### Workbook steps

<table>
<thead>
<tr class="header">
<th><strong>Step</strong></th>
<th><strong>Details</strong></th>
<th><strong>Additional Information</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>Click on the Red Hat image found in the middle of the virtual machines to open this image.</td>
<td><img src="./images/media/image5.png" style="width:3.53819in;height:1.73264in" /></td>
</tr>
<tr class="even">
<td>2</td>
<td><p>Login as the user <em><strong>sysadmin</strong></em> with password of <em><strong>Passw0rd</strong></em></p>
<p>The 0 is a zero.</p></td>
<td><img src="./images/media/image6.png" style="width:1.76352in;height:1.75694in" /></td>
</tr>
<tr class="odd">
<td>3</td>
<td>Open a Terminal Window by clicking the terminal shortcut on the desktop</td>
<td><img src="./images/media/image8.png" style="width:1.6836in;height:3.10417in" /></td>
</tr>
<tr class="even">
<td>4</td>
<td><p>Before we get started, we need to start our ACE environment by running a script.</p>
<p>In your terminal window, run these commands:</p>
<p>$ cd scripts</p>
<p>$ ./start-ace.sh</p>
<p><strong>NOTE:</strong> let the script run for a couple of minutes so you see that it starts INODEDEV, INODEQA, and INODEPROD before moving to next step.</p></td>
<td><img src="./images/media/image9.png" style="width:3.53819in;height:1.13403in" /></td>
</tr>
<tr class="odd">
<td>5</td>
<td><p>We will now start the IBM App Connect Enterprise (ACE) Toolkit eclipse-based IDE. It is a great tool for developers as they develop APIs.</p>
<p>To start the ACE Toolkit, we need to first source the ACE mqsiprofile by running this command:</p>
<p>$ . /opt/IBM/ace-12.0.10.0/server/bin/mqsiprofile</p></td>
<td><p>. /opt/IBM/ace-12.0.10.0/server/bin/mqsiprofile</p>
<p><strong>NOTE:</strong> there is a space after the . shown above.</p>
<p><img src="./images/media/image10.png" style="width:3.53819in;height:0.77847in" /></p></td>
</tr>
<tr class="even">
<td>5</td>
<td><p>We can now start the IBM App Connect Enterprise Toolkit eclipse-based IDE.</p>
<p>Run the commands below to start the toolkit:</p>
<p>$ cd /opt/IBM/ace-12.0.10.0</p>
<p>$ ./ace toolkit</p></td>
<td><p># cd /opt/IBM/ace-12.0.10.0</p>
<p># ./ace toolkit</p>
<p>You should see output as follows:</p>
<p><img src="./images/media/image11.png" style="width:3.53819in;height:1.47847in" /></p></td>
</tr>
<tr class="odd">
<td>6</td>
<td><p>A launcher dialog will appear.</p>
<p>Take the default workspace that is shown and click the “<strong>Launch</strong>” button.</p></td>
<td><img src="./images/media/image12.png" style="width:3.29236in;height:1.52631in" /></td>
</tr>
<tr class="even">
<td>7</td>
<td>The IDE will appear as shown to the right and your workspace is already populated with an example ACE project we will use.</td>
<td><img src="./images/media/image13.png" style="width:3.53819in;height:1.55139in" /></td>
</tr>
<tr class="odd">
<td>8</td>
<td><p>As a developer, you can edit your ACE code in the IDE, compile your code, and deploy to a DEV environment.</p>
<p>Let’s make a small change to our program to see how this works in the IDE.</p></td>
<td></td>
</tr>
<tr class="even">
<td>9</td>
<td>In the <strong>GetHello_JavaCompute.java</strong> program, scroll down to the line that starts with “MbElement outJsonMsg” as highlighted to the right.</td>
<td><img src="./images/media/image14.png" style="width:3.53819in;height:1.88542in" /></td>
</tr>
<tr class="odd">
<td>10</td>
<td>Change the text that says “Hello from <strong>Green</strong> Integration powered by…” to “Hello from <strong>Blue</strong> Integration powered by…” as shown to the right</td>
<td><img src="./images/media/image15.png" style="width:3.53819in;height:0.4in" /></td>
</tr>
<tr class="even">
<td>11</td>
<td><p>Save your changes by clicking on the File menu and then clicking “Save”</p>
<p>or</p>
<p>by clicking the Save icon as shown to the right.</p></td>
<td><img src="./images/media/image16.png" style="width:1.1875in;height:0.92532in" /></td>
</tr>
<tr class="odd">
<td>12</td>
<td><p>You can build and deploy your BAR file in a single step using the IDE.</p>
<p>Expand the INODEDEV integration node that is shown towards the bottom of the page.</p>
<p>You should see the child node, “Emerald-ACE-DEV”, which is an integration server as shown to the right.</p></td>
<td><img src="./images/media/image17.png" style="width:3.53819in;height:2.12222in" /></td>
</tr>
<tr class="even">
<td>13</td>
<td>To initiate the build and deploy, in the left-hand pane, drag “<strong>JGRACEIVT</strong>” from the top pane to the “<strong>Emerald-ACE-DEV</strong>” integration server as shown in the screen shot above.</td>
<td><img src="./images/media/image18.png" style="width:3.07019in;height:2.99306in" /></td>
</tr>
<tr class="odd">
<td>14</td>
<td><p>A “Progress Information” dialog will appear to show you the progress of your build and deployment.</p>
<p>The task should complete successfully as shown to the right.</p>
<p>In the messages that appear, you should see that your BAR file has been successfully deployed to the integration server, Emerald-ACE-DEV.</p></td>
<td><img src="./images/media/image19.png" style="width:2.86332in;height:2.9375in" /></td>
</tr>
<tr class="even">
<td>15</td>
<td>Click the ‘<strong>Close</strong>’ button to close the ‘Progress Information’ window.</td>
<td></td>
</tr>
<tr class="odd">
<td>16</td>
<td><p>Click the ‘Deployment Log’ perspective at the bottom of the screen to see a log of your deployments.</p>
<p>Expand the parent tree node to see all the messages as shown to the right.</p></td>
<td><img src="./images/media/image20.png" style="width:3.53819in;height:2.92569in" /></td>
</tr>
<tr class="even">
<td>17</td>
<td><p>We will now validate that our changes are visible in this new version of the BAR.</p>
<p>You can minimize the ACE IDE by clicking on the application workspace icon at the bottom of the screen.</p>
<p>Open a Firefox dialog using the Desktop shortcut as shown to the right.</p></td>
<td><img src="./images/media/image21.png" style="width:0.87955in;height:3.48611in" /></td>
</tr>
<tr class="odd">
<td>18</td>
<td>Click on the “IBM ACE – INODEDEV” bookmark found in the bookmark bar as shown to the right.</td>
<td><img src="./images/media/image22.png" style="width:2.35094in;height:2.35417in" /></td>
</tr>
<tr class="even">
<td>19</td>
<td><p>First, click on ‘Emerald-ACE-DEV’ and you will see the ‘JGRACEIVT’ api.</p>
<p>Second, click on ‘JGRACEIVT’ and you will see the Documentation tab of the API as shown to the right.</p>
<p>Notice the ‘Endpoint’ value. Copy this to your buffer.</p></td>
<td><img src="./images/media/image23.png" style="width:3.53819in;height:2.20556in" /></td>
</tr>
<tr class="odd">
<td>20</td>
<td><p>In your browser, open a new tab and paste the endpoint value into the browser and append /hello as shown below to the URL:</p>
<p><a href="http://ace-server:7080/jgraceivt/v1/hello">http://ace-server:7080/jgraceivt/v1/hello</a></p>
<p>Press Enter.</p></td>
<td><img src="./images/media/image24.png" style="width:3.53819in;height:0.95556in" /></td>
</tr>
<tr class="even">
<td>21</td>
<td><p>You should see ‘Blue’ in the message as shown above.</p>
<p>You have completed this section! In the next section, we will explore a way to create an automated build process in a CI/CD pipeline as well as automatically run some unit tests against your ACE BAR.</p></td>
<td><p><strong>NOTE:</strong> You would not want your developers performing automating deployments to QA or PROD from their local desktop IDE.</p>
<p>You would want a proper DevOps pipeline to ensure you have the right controls and governance in place.</p></td>
</tr>
<tr class="odd">
<td><strong>End of Section – 3.1</strong></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Setup a Jenkins CI Pipeline to Automate Build

### Overview

In the past, many developers using their IDE would build a new BAR and
copy it to a shared folder that others would pick up for deployment. The
issue with this is you do not have traceability back to the build, you
are not placing the artifact in a definitive asset repository that is
immutable, and you don’t have any real record of the build or
deployment.

In this lab section, you will explore an example Continuous Integration
(CI) Pipeline using Jenkins. This pipeline requires that developer’s
check-in their code changes to a git repository. You could configure the
pipeline to automatically trigger a build on code-commit if you like or
on-demand.

You will see in this lab that we have incorporated a stage to run unit
tests and to push the deployable artifact (a BAR file) to IBM DevOps
Deploy’s version repository called ‘codestation’, which is like a JFrog
Artifactory or Sonatype Nexus. Using this pipeline, we will have full
traceability and trail of audit with proper governance.

### Workbook Steps

### 

<table>
<thead>
<tr class="header">
<th><strong>Step</strong></th>
<th><strong>Details</strong></th>
<th><strong>Additional Information</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td><p>Before we open our Jenkins pipeline, we need to start our Jenkins build agent.</p>
<p>Open a <strong>new terminal</strong> <strong>window</strong> by clicking on Activities at the upper left-hand corner of the screen and then click on the Terminal icon as shown to the right.</p>
<p><strong>NOTE:</strong> we are opening a new terminal to ensure JAVA_HOME is set to a Java 11 installation on the host.</p></td>
<td><img src="./images/media/image25.png" style="width:0.56106in;height:4.33333in" /> <img src="./images/media/image26.png" style="width:3.06921in;height:0.76319in" /></td>
</tr>
<tr class="even">
<td>2</td>
<td><p>In the terminal window, change directories to /home/sysadmin/scripts</p>
<p>$ cd /home/sysadmin/scripts</p></td>
<td><img src="./images/media/image27.png" style="width:3.45833in;height:1.35542in" /></td>
</tr>
<tr class="odd">
<td>3</td>
<td><p>Run the following command to start the Jenkins agent:</p>
<p>$ sudo ./start-jenkins-agent.sh</p></td>
<td><img src="./images/media/image28.png" style="width:3.25366in;height:2.08362in" /></td>
</tr>
<tr class="even">
<td>4</td>
<td><p>We also need to start the IBM DevOps Deploy Agent used for deployment.</p>
<p>Run the following command to start the Deploy agent:</p>
<p>$ sudo ./start-ucd-agent.sh</p></td>
<td><img src="./images/media/image29.png" style="width:3.25347in;height:0.6045in" /></td>
</tr>
<tr class="odd">
<td>5</td>
<td><p>We can now explore our Jenkins CI pipeline.</p>
<p>In your Firefox browser window, create a new tab and click on the “<strong>Dashboard [Jenkins]</strong>” bookmark as shown to the right</p></td>
<td><img src="./images/media/image30.png" style="width:3.54583in;height:1.72159in" /></td>
</tr>
<tr class="even">
<td>6</td>
<td>Login to the console with a user of “<strong>admin</strong>” and a password of “<strong>password</strong>”</td>
<td></td>
</tr>
<tr class="odd">
<td>7</td>
<td>Click on the “<strong>emerald-ace</strong>” pipeline as shown to the right</td>
<td><img src="./images/media/image31.png" style="width:3.75847in;height:2.39236in" /></td>
</tr>
<tr class="even">
<td><strong>INFO</strong></td>
<td>This is an example pipeline that is pointed to a GitHub repository that I have created for this lab. Take time to explore the pipeline as much as you like.</td>
<td></td>
</tr>
<tr class="odd">
<td>8</td>
<td><p>You will see the ‘emerald-ace’ pipeline and you can see each stage on the right-hand side which includes:</p>
<ul>
<li><p>Cloning the repository</p></li>
<li><p>Build</p></li>
<li><p>UnitTest</p></li>
<li><p>Push Artifact of Build to IBM DevOps Deploy</p></li>
</ul></td>
<td><img src="./images/media/image32.png" style="width:3.64306in;height:2.96292in" /></td>
</tr>
<tr class="even">
<td>9</td>
<td><p>Move mouse over the “GitHub” found in the left-hand pane.</p>
<p>Right click on this link and select “Open Link in a New Tab” as shown to the right.</p></td>
<td><img src="./images/media/image33.png" style="width:2.98333in;height:2.36099in" /></td>
</tr>
<tr class="odd">
<td>10</td>
<td><p>This is the same code that you were working with in the first lab.</p>
<p>The focus of this lab is to explain how you can setup a CI pipeline that includes automated unit testing and deployment as part of the process.</p></td>
<td><img src="./images/media/image34.png" style="width:3.40972in;height:2.3553in" /></td>
</tr>
<tr class="even">
<td>11</td>
<td><p>Return to the Jenkins tab in your browser.</p>
<p>Notice the build history at the bottom left showing you the most recent builds.</p>
<p>Notice the build tags that identify each build (3.0.28, 3.0.27, etc).</p></td>
<td><img src="./images/media/image35.png" style="width:3.52083in;height:2.64988in" /></td>
</tr>
<tr class="odd">
<td>12</td>
<td>Click the “Configure” link in the left-hand pane to explore the build pipeline.</td>
<td><img src="./images/media/image36.png" style="width:3.35139in;height:1.50989in" /></td>
</tr>
<tr class="even">
<td>13</td>
<td><p>Scroll down to the Pipeline script area as shown to the right.</p>
<p><strong>NOTE:</strong> You can make the script pane larger by dragging the text area further down using your mouse.</p></td>
<td><img src="./images/media/image37.png" style="width:3.77083in;height:2.13853in" /></td>
</tr>
<tr class="odd">
<td>14</td>
<td>In the pipeline view, you will see each stage of the build process. Our first stage is to ‘Clone the Repository’ which will pull down your source code from git to a workspace that is used by the Jenkins Agent to perform the build.</td>
<td><img src="./images/media/image38.png" style="width:3.775in;height:0.85037in" /></td>
</tr>
<tr class="even">
<td>15</td>
<td>Next, you see the ‘Build’ stage of the process. This is where the agent will use the ‘<strong>ibmint</strong>’ command to build your broker archive (BAR) image.</td>
<td><img src="./images/media/image39.png" style="width:3.70833in;height:0.89932in" /></td>
</tr>
<tr class="odd">
<td>16</td>
<td>As you scroll down, you will find a ‘UnitTest’ stage of the pipeline to run unit tests against your newly built BAR file. This helps to ensure your changes did not break any functionality.</td>
<td><img src="./images/media/image40.png" style="width:3.67083in;height:1.40959in" /></td>
</tr>
<tr class="even">
<td>17</td>
<td>For now, scroll back to the top of the browser and click on ‘emerald-ace’ in the crumb trail as shown to the right.</td>
<td><img src="./images/media/image41.png" style="width:3.5111in;height:2.56736in" /></td>
</tr>
<tr class="odd">
<td>18</td>
<td><p>Let’s start a build and watch it run.</p>
<p>Click the ‘<strong>Build Now</strong>’ button in the left-hand pane.</p></td>
<td><img src="./images/media/image42.png" style="width:2.92469in;height:1.56847in" /></td>
</tr>
<tr class="even">
<td>19</td>
<td>The build will initiate, and you will see a new build labeled ‘3.0.29’ in the bottom left-hand ‘Build History’ pane as shown to the right.</td>
<td><img src="./images/media/image43.png" style="width:3.53889in;height:2.34487in" /></td>
</tr>
<tr class="odd">
<td>20</td>
<td><p>When the build completes, click on the green checkmark next to the 3.0.29 build label in the Build History as shown above.</p>
<p>This will allow you to see the Console Output for the build shown to the right.</p></td>
<td><img src="./images/media/image44.png" style="width:3.66389in;height:2.44187in" /></td>
</tr>
<tr class="even">
<td>21</td>
<td>Scroll down and you will see the successful build of the BAR.</td>
<td><img src="./images/media/image45.png" style="width:3.7958in;height:3.28472in" /></td>
</tr>
<tr class="odd">
<td>22</td>
<td>Scroll down a little further and you will see the Unit Tests were run and that they were successful.</td>
<td><img src="./images/media/image46.png" style="width:3.71215in;height:2.82in" /></td>
</tr>
<tr class="even">
<td>23</td>
<td><p>If you scroll down, you will notice one more stage called ‘<strong>Push Artifact of Build to IBM DevOps Deploy</strong>’. This stage is not configured yet.</p>
<p>Let’s modify this build project to perform this step so we can deploy our BAR file to our target environments.</p></td>
<td>We will work on this stage together to enable it to push the BAR to the DevOps Deploy Server for automated deployment.</td>
</tr>
<tr class="odd">
<td>24</td>
<td><p>In your browser window, create a new tab.</p>
<p>Then click on the ‘<strong>UrbanCode Deploy: Login</strong>’ bookmark in the toolbar as shown to the right.</p></td>
<td><img src="./images/media/image47.png" style="width:3.57389in;height:0.74306in" /></td>
</tr>
<tr class="even">
<td>25</td>
<td>Login as the user ‘<strong>admin’</strong> and with a password of ‘<strong>admin’</strong></td>
<td><img src="./images/media/image48.png" style="width:3.62917in;height:1.82934in" /></td>
</tr>
<tr class="odd">
<td>26</td>
<td>Click on Components at the top of the page as shown to the right</td>
<td><img src="./images/media/image49.png" style="width:2.95492in;height:2.29134in" /></td>
</tr>
<tr class="even">
<td>27</td>
<td>Click on ‘emerald-ACE-BAR’ as shown above to view this component</td>
<td></td>
</tr>
<tr class="odd">
<td>28</td>
<td><p>Notice the component versions listed.</p>
<p>This is where are Jenkins build process will push the built artifact as a new component version using the build tag.</p></td>
<td><img src="./images/media/image50.png" style="width:2.21186in;height:1.88861in" /></td>
</tr>
<tr class="even">
<td>29</td>
<td><p>In order for the Jenkins build to push the new component version, we need to create an Authentication Token that it can use.</p>
<p>Click on the <strong>Settings</strong> tab at the top right-hand side of the page.</p></td>
<td><img src="./images/media/image51.png" style="width:3.86528in;height:1.97403in" /></td>
</tr>
<tr class="odd">
<td>30</td>
<td>Click on <strong>Tokens</strong> found in the Security section of the Settings page.</td>
<td><img src="./images/media/image52.png" style="width:3.39306in;height:1.857in" /></td>
</tr>
<tr class="even">
<td>31</td>
<td>Click on the ‘<strong>Create Token</strong>’ button</td>
<td><img src="./images/media/image53.png" style="width:3.55972in;height:0.49376in" /></td>
</tr>
<tr class="odd">
<td>32</td>
<td><p>The Create Token dialog will appear. Use the following follows:</p>
<p>Description: Jenkins Token</p>
<p>User: admin</p>
<p>Expiration Date: 12/13/2024</p>
<p>Expiration Time: 08:00 AM</p></td>
<td><img src="./images/media/image54.png" style="width:1.73563in;height:2.26in" /></td>
</tr>
<tr class="even">
<td>33</td>
<td>Click Save</td>
<td></td>
</tr>
<tr class="odd">
<td>34</td>
<td>In the Newly Created Token dialog that appears, copy the Token value to your buffer.</td>
<td><img src="./images/media/image55.png" style="width:1.75in;height:1.0077in" /></td>
</tr>
<tr class="even">
<td>35</td>
<td>Open a Text Editor by clicking on Activities at the top left-hand side of the page (step 1) and then click on the dots (step 2) to see all the applications.</td>
<td><img src="./images/media/image56.png" style="width:3.79167in;height:2.88266in" /></td>
</tr>
<tr class="odd">
<td>36</td>
<td>Click on the <strong>Text Editor</strong> icon (step 3) as shown above to start the editor.</td>
<td></td>
</tr>
<tr class="even">
<td>37</td>
<td>In the terminal window, enter ‘Deploy Token:’ and then paste your auth token.</td>
<td><img src="./images/media/image57.png" style="width:3.53194in;height:0.63873in" /></td>
</tr>
<tr class="odd">
<td>38</td>
<td>Close the ‘Newly Created Token’ dialog in the Deploy web console by clicking the ‘Close’ button.</td>
<td><img src="./images/media/image58.png" style="width:1.5625in;height:0.90618in" /></td>
</tr>
<tr class="even">
<td>39</td>
<td><p>Return to your Jenkins tab in your browser.</p>
<p>Return to the ‘emerald-ace’ project as shown to the right. You can click on ‘emerald-ace’ in the crumb trail at upper-right of screen to return to this page.</p></td>
<td><img src="./images/media/image59.png" style="width:3.65972in;height:3.07916in" /></td>
</tr>
<tr class="odd">
<td>40</td>
<td>Click on ‘Configure’ for the ‘emerald-ace’ pipeline as shown above</td>
<td></td>
</tr>
<tr class="even">
<td>41</td>
<td>Scroll down to the Pipeline script and expand the script pane to give you more space to work with.</td>
<td><img src="./images/media/image60.png" style="width:3.65972in;height:1.82986in" /></td>
</tr>
<tr class="odd">
<td>42</td>
<td>In the script area, scroll down to the ‘<strong>Push Artifact of Build to IBM DevOps Deploy’</strong> stage.</td>
<td></td>
</tr>
<tr class="even">
<td>43</td>
<td><p>Notice line 50 of the script:</p>
<p>export UCD_AUTH_TOKEN=”replace-me”</p></td>
<td><img src="./images/media/image61.png" style="width:3.65972in;height:0.79428in" /></td>
</tr>
<tr class="odd">
<td>44</td>
<td><p>Paste your new auth token value to replace the ‘replace-me’ text as shown in the example to the right.</p>
<p><strong>NOTE:</strong> normally this would be configured as a secure property.</p></td>
<td><img src="./images/media/image62.png" style="width:3.05556in;height:0.65528in" /></td>
</tr>
<tr class="even">
<td>45</td>
<td><p>Scroll down and remove the # at the beginning of lines 70-72 to uncomment them.</p>
<p>This will allow the pipeline to create a new component version using the IBM DevOps Deploy udclient command.</p></td>
<td><img src="./images/media/image63.png" style="width:3.775in;height:0.45924in" /></td>
</tr>
<tr class="odd">
<td>46</td>
<td>Scroll down to line 78 and remove the # to uncomment this line so it will add a component status of ‘Unit Tests Passed’</td>
<td><img src="./images/media/image64.png" style="width:3.58681in;height:0.64083in" /></td>
</tr>
<tr class="even">
<td>47</td>
<td><p>Click ‘<strong>Save</strong>’ to save your updates to the pipeline script.</p>
<p><strong>NOTE:</strong> you do not need to uncomment lines 83-87. Leave them as they were.</p></td>
<td><img src="./images/media/image65.png" style="width:3.84722in;height:1.97167in" /></td>
</tr>
<tr class="odd">
<td>48</td>
<td>In the crumb trail at the top left, click on ‘emerald-ace’</td>
<td><img src="./images/media/image66.png" style="width:2.23611in;height:1.14821in" /></td>
</tr>
<tr class="even">
<td>49</td>
<td>Initiate a new build by clicking the ‘<strong>Build Now</strong>’ button</td>
<td><img src="./images/media/image67.png" style="width:1.09028in;height:0.93867in" /></td>
</tr>
<tr class="odd">
<td>50</td>
<td><p>You will see a new build initiate.</p>
<p>The build should complete successfully.</p></td>
<td><img src="./images/media/image68.png" style="width:3.69429in;height:3.08333in" /></td>
</tr>
<tr class="even">
<td>51</td>
<td><p>Examine the build output and you should see that it was successful in creating a new component version to push the new deployable artifact.</p>
<p><strong>NOTE:</strong> DevOps Deploy can integrate with other definitive asset repositories like JFrog Artifactory or Sonatype Nexus.</p></td>
<td><img src="./images/media/image69.png" style="width:3.55278in;height:1.97611in" /></td>
</tr>
<tr class="odd">
<td>52</td>
<td>In your browser, click on the ‘DevOps Deploy’ tab.</td>
<td></td>
</tr>
<tr class="even">
<td>53</td>
<td><p>Click on Components at the top of the page.</p>
<p>NOTE: you may need to re-authenticate using username of ‘admin’ and password of ‘admin’</p></td>
<td><img src="./images/media/image70.png" style="width:3.55278in;height:1.76441in" /></td>
</tr>
<tr class="odd">
<td>54</td>
<td>Click on the ‘emerald-ACE-BAR’ component.</td>
<td></td>
</tr>
<tr class="even">
<td>55</td>
<td>You should see a new component version, 3.0.30, in the list of Component Versions as shown to the right.</td>
<td><img src="./images/media/image71.png" style="width:2.68602in;height:1.90972in" /></td>
</tr>
<tr class="odd">
<td>56</td>
<td><p>Click on 3.0.30 to view the new version.</p>
<p>Notice the immutable artifact in the Artifacts list, <strong>jgr-cp4i-aceivt.bar</strong>. A component version can have one or more files.</p></td>
<td><img src="./images/media/image72.png" style="width:2.60495in;height:2.75in" /></td>
</tr>
<tr class="even">
<td>57</td>
<td><p>Notice the link back to the Jenkins pipeline (see screenshot above) so you have traceability back to the build and the git commit.</p>
<p>If you right click on the link, you can open this link in a new tab. It will take you to the build ‘Console Output’ as shown to the right.</p></td>
<td><img src="./images/media/image73.png" style="width:3.90278in;height:2.13558in" /></td>
</tr>
<tr class="odd">
<td>58</td>
<td><p>You have completed this lab.</p>
<p>In the next lab, we will look at the deployment of the application in IBM DevOps Deploy.</p></td>
<td></td>
</tr>
<tr class="even">
<td><strong>End of Section – 3.2</strong></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Review the Emerald eStore Application in IBM DevOps Deploy

### Overview

In this lab section, you will explore the ‘Emerald eStore’ application
in IBM DevOps Deploy. The solution leverages an application model that
is comprised of three parts:

1.  Environments

2.  Components that make up your application. You can have more than
    one.

3.  Processes to perform deployments.

### Workbook steps

<table>
<thead>
<tr class="header">
<th><strong>Step</strong></th>
<th><strong>Details</strong></th>
<th><strong>Additional Information</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>In your Firefox browse, return to the “Deploy” tab.</td>
<td><img src="./images/media/image74.png" style="width:3.6875in;height:1.36298in" /></td>
</tr>
<tr class="even">
<td>2</td>
<td>Click on the “Applications” tab at the top of the page as highlighted above.</td>
<td><strong>NOTE:</strong> you may be asked to re-authenticate to the Deploy Console using your admin/admin credentials</td>
</tr>
<tr class="odd">
<td>3</td>
<td><p>You will see the “<strong>Emerald eStore</strong>” application in the Applications list.</p>
<p>Click on “Emerald eStore” to view the application</p></td>
<td><img src="./images/media/image75.png" style="width:3.49722in;height:1.42614in" /></td>
</tr>
<tr class="even">
<td>4</td>
<td>The first part of the application model which we can see are the target environments which are DEV, QA, and PROD which are already configured for you.</td>
<td><img src="./images/media/image76.png" style="width:3.715in;height:1.75694in" /></td>
</tr>
<tr class="odd">
<td>5</td>
<td><p>Expand the DEV environment by clicking the arrow next to the DEV environment. You will see the second part of the model which are the components.</p>
<p>In this case, we have a component named “emerald” and our ACE component named “emerald-ACE-BAR”.</p>
<p>Notice that IBM DevOps Deploy tracks inventory of what is currently deployed in the DEV environment (e.g. 9.1.6-201 for “emerald” which is usually a build tag for traceability)</p></td>
<td><img src="./images/media/image77.png" style="width:3.69126in;height:1.41597in" /></td>
</tr>
<tr class="even">
<td><strong>INFO</strong></td>
<td><p>To see all the components, you can also click on the “Components” sub-tab.</p>
<p>Not all components will necessarily track inventory. For instance, the “emerald-RTAS” component will run operational processes to initiate test execution using Rational Test Automation Server.</p></td>
<td></td>
</tr>
<tr class="odd">
<td>6</td>
<td><p>The last part of the application model are processes. For now, click on the “Processes” sub-tab for our application to see our application process which will perform the deployment of the Emerald eStore application and more.</p>
<p>We will be updating a process as part of the next lab section.</p></td>
<td><img src="./images/media/image78.png" style="width:3.53194in;height:2.06643in" /></td>
</tr>
<tr class="even">
<td><strong>End of Section – 3.3</strong></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Work with the emerald-ACE-BAR Component in Deploy

### Overview

In this lab section, you will review the emerald-BAR component which
will be used to deploy your broker archive that was built earlier in the
lab. You will update the component process and then test the deployment
to a DEV environment.

### Workbook steps

<table>
<thead>
<tr class="header">
<th><strong>Step</strong></th>
<th><strong>Details</strong></th>
<th><strong>Additional Information</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>Continuing to work in the IBM DevOps Deploy application, click on the <strong>Components</strong> tab at the top of the page</td>
<td><img src="./images/media/image79.png" style="width:3.42778in;height:1.33019in" /></td>
</tr>
<tr class="even">
<td>2</td>
<td>Click on the “emerald-ACE-BAR” component as highlighted above</td>
<td></td>
</tr>
<tr class="odd">
<td>3</td>
<td>Click on the “History” sub-tab as highlighted to the right.</td>
<td><img src="./images/media/image80.png" style="width:3.27778in;height:1.90437in" /></td>
</tr>
<tr class="even">
<td>4</td>
<td>This view will show you which versions of a component are deployed in each target environment.</td>
<td><img src="./images/media/image81.png" style="width:3.54583in;height:1.33944in" /></td>
</tr>
<tr class="odd">
<td>5</td>
<td>Click on the “Usage” sub-tab just to the right of the History sub-tab.</td>
<td></td>
</tr>
<tr class="even">
<td>6</td>
<td>The Usage tab will allow you to see which component version is currently deployed to a target environment, what used to be deployed in the environment prior, and at what days over time was it deployed there.</td>
<td><img src="./images/media/image82.png" style="width:3.56667in;height:1.46719in" /></td>
</tr>
<tr class="odd">
<td>7</td>
<td>Click on the “Processes” sub-tab (see below)</td>
<td></td>
</tr>
<tr class="even">
<td>8</td>
<td>Click on the “Deploy-BAR” process as shown to the right</td>
<td><img src="./images/media/image83.png" style="width:3.57049in;height:1.12361in" /></td>
</tr>
<tr class="odd">
<td>9</td>
<td><p>The visual process designer will appear and display the component process.</p>
<p>This left-hand pane of the designer is where you will find all the steps that you can drag and drop onto the process design. You can add to these steps by installing automation plugins.</p>
<p>Notice the flow of the process. The first step downloads the artifact for deployment from IBM DevOps Deploy’s codestation repository.</p></td>
<td><img src="./images/media/image84.png" style="width:3.61111in;height:2.49218in" /></td>
</tr>
<tr class="even">
<td>10</td>
<td><p>In the ‘Type to filter’ text area found at the upper left, type ‘ACE’ as shown.</p>
<p>The left-hand step-palette will display all of the IBM ACE plugin steps including the ‘Deploy’ step. This is the step we will use to deploy the broker archive (BAR) to an integration server running on an integration node.</p></td>
<td><img src="./images/media/image85.png" style="width:3.48502in;height:2.41in" /></td>
</tr>
<tr class="odd">
<td>11</td>
<td>Click the pencil icon for the existing ‘Deploy’ step in the component process to examine the step details.</td>
<td><img src="./images/media/image86.png" style="width:1.1953in;height:0.61806in" /></td>
</tr>
<tr class="even">
<td>12</td>
<td><p>Examine the inputs for the step.</p>
<p>With IBM DevOps Deploy, you can pass in a hard-code string value for some of the inputs, however, it is most common to leverage properties.</p>
<p>A property in IBM DevOps Deploy looks like <strong>${p:my-property}</strong>. If a value could vary from one environment to the next, you can set the property at an environment scope. You can then reference the property with <strong>${p:environment/my-property}</strong> in your step.</p></td>
<td><img src="./images/media/image87.png" style="width:2.04861in;height:2.68182in" /></td>
</tr>
<tr class="odd">
<td>13</td>
<td>Scroll down and observe some additional properties for the ACE Deploy step including ip-address, ace-port, and integration-server-name.</td>
<td><img src="./images/media/image88.png" style="width:2.04528in;height:2.65972in" /></td>
</tr>
<tr class="even">
<td>14</td>
<td><p>Check the box to ‘<strong>Clear Old Deployments’</strong></p>
<p>Notice the help pop-up dialog for each step you can hover your mouse over.</p>
<p>The help tells us that when ‘Clear Old Deployments’ is enabled (or checked), this will run a complete deployment (as opposed to incremental).</p></td>
<td><img src="./images/media/image89.png" style="width:2.08696in;height:2.01389in" /></td>
</tr>
<tr class="odd">
<td>15</td>
<td>Scroll down and click OK</td>
<td><img src="./images/media/image90.png" style="width:1.60109in;height:2.09028in" /></td>
</tr>
<tr class="even">
<td>17</td>
<td>Notice that the next step in the process will ‘Run ACE RTAS Tests’. This will execute some automated tests in IBM DevOps Test Hub to verify the deployed BAR is working as expected.</td>
<td><img src="./images/media/image91.png" style="width:2.375in;height:2.375in" /></td>
</tr>
<tr class="odd">
<td>18</td>
<td><p>IBM DevOps Deploy has a governance feature that you can leverage called ‘<strong>gates’</strong>. The gates help to ensure that a component version meets entry criteria for a target environment. For example, “Unit Tests Passed” or Functional Tests Passed”.</p>
<p>Here is an example of gates configured for an application:</p>
<p><img src="./images/media/image92.png" style="width:2.54962in;height:2.0625in" /></p>
<p>For our process, we need to update the process so that if the functional test pass, we automatically set a status called ‘<strong>Functional</strong> <strong>Tests</strong> <strong>Passed’</strong>. This is needed so we can promote this to the QA environment.</p>
<p>In the search ‘<strong>Type to filter’</strong> text field, type ‘<strong>Add Status</strong>’ as shown to the right</p></td>
<td><img src="./images/media/image93.png" style="width:3.2125in;height:2.10249in" /></td>
</tr>
<tr class="even">
<td>19</td>
<td><p>Drag the ‘<strong>Add Status to Version</strong>’ step from the step palette and drop it on the process design.</p>
<p>The best way to do this is to drag the step and hover over the line that connects the ‘<strong>Run ACE RTAS Tests’</strong> step to ‘<strong>Set Status: Success</strong>’ step. The line will turn a blue color. (See the screen shot to the right). While the line is blue, release your mouse to drop the step onto the design.</p></td>
<td><img src="./images/media/image94.png" style="width:3.5625in;height:2.28034in" /></td>
</tr>
<tr class="odd">
<td>20</td>
<td><p>Your process design should now look like this.</p>
<p>Click the pencil icon for the new step you added to the process design</p></td>
<td><img src="./images/media/image95.png" style="width:2.76389in;height:2.71456in" /></td>
</tr>
<tr class="even">
<td>21</td>
<td><p>In the Edit Properties dialog that appears, provide the following initial values:</p>
<p><strong>Name</strong>: Add Status to Version - Pass</p>
<p><strong>Status</strong>: Functional Tests Passed</p>
<p><strong>NOTE</strong>: the status is case sensitive and it must match an existing Status that exists. Be sure the value you type is ‘<strong>Functional</strong> <strong>Tests</strong> <strong>Passed’</strong> as shown to the right.</p></td>
<td><img src="./images/media/image96.png" style="width:2.957in;height:1.75556in" /></td>
</tr>
<tr class="odd">
<td>22</td>
<td>Scroll down and click OK</td>
<td><img src="./images/media/image97.png" style="width:2.36111in;height:2.55565in" /></td>
</tr>
<tr class="even">
<td>23</td>
<td>Click the <strong>Save</strong> button to save the component process</td>
<td><img src="./images/media/image98.png" style="width:2.74306in;height:2.03866in" /></td>
</tr>
<tr class="odd">
<td>24</td>
<td><p>You should notice that the version of the process is now ‘Version 10 of 10’ as highlighted to the right.</p>
<p>DevOps Deploy has built-in versioning capabilities in the tool you can leverage. This process can be exported in a JSON format and checked into a git repository.</p></td>
<td><img src="./images/media/image99.png" style="width:3.92452in;height:2.60499in" /></td>
</tr>
<tr class="even">
<td>25</td>
<td><p>Before we complete this section of the lab, we need to generate a new API Token in IBM DevOps Test Hub that will be used by our processes to test what we deploy to the target environments. The API Token is needed to authenticate with the IBM DevOps Test Hub application.</p>
<p>In your browser, create a new tab and then click the ‘<strong>DevOps Test Hub</strong>’ bookmark found the toolbar.</p></td>
<td><img src="./images/media/image100.png" style="width:4.39547in;height:1.88962in" /></td>
</tr>
<tr class="odd">
<td>26</td>
<td>Login to IBM DevOps Test Hub as the user <em><strong>techxchange</strong></em> with password of <em><strong>password</strong></em></td>
<td></td>
</tr>
<tr class="even">
<td>27</td>
<td>Right click on the user profile at the top-right of the screen as shown to the right (step 1).</td>
<td><img src="./images/media/image101.png" style="width:4.37917in;height:1.63166in" /></td>
</tr>
<tr class="odd">
<td>28</td>
<td>Click the ‘<strong>Create Token</strong>’ menu item as highlighted above (step 2).</td>
<td></td>
</tr>
<tr class="even">
<td>29</td>
<td><p>A new API Token will appear.</p>
<p>Click the ‘<strong>Copy</strong>’ button to copy the token to your buffer.</p></td>
<td><img src="./images/media/image102.png" style="width:2.95139in;height:1.70965in" /></td>
</tr>
<tr class="odd">
<td>30</td>
<td>Open your ‘Text Editor’ window and paste the API Token for future reference as shown in the example to the right.</td>
<td><img src="./images/media/image103.png" style="width:4.1764in;height:0.71304in" /></td>
</tr>
<tr class="even">
<td>31</td>
<td><p>Return to your DevOps Deploy tab in your browser.</p>
<p>Click on Components at the top of the screen (step 1).</p></td>
<td><img src="./images/media/image104.png" style="width:4.06395in;height:2.95109in" /></td>
</tr>
<tr class="odd">
<td>32</td>
<td>Click on the ‘emerald-TestHub component (step 2) as shown above.</td>
<td></td>
</tr>
<tr class="even">
<td>33</td>
<td>Click on the Processes sub-tab</td>
<td><img src="./images/media/image105.png" style="width:2.625in;height:1.11031in" /></td>
</tr>
<tr class="odd">
<td>34</td>
<td>Click on the ‘Run Automated Test for ACE API’ process.</td>
<td><img src="./images/media/image106.png" style="width:2.95139in;height:1.61537in" /></td>
</tr>
<tr class="even">
<td>35</td>
<td><p>The visual process design will appear for the process.</p>
<p>Click the pencil icon for the ‘<strong>Run IBM Rational Test Automation Server test</strong>’ step as shown to the right.</p></td>
<td><img src="./images/media/image107.png" style="width:3.18068in;height:2.27292in" /></td>
</tr>
<tr class="odd">
<td>36</td>
<td>Paste the new API Key from your Text Editor window into the ‘<strong>Offline Token</strong>’ field as shown to the right.</td>
<td><img src="./images/media/image108.png" style="width:3.53472in;height:2.45928in" /></td>
</tr>
<tr class="even">
<td>37</td>
<td>Scroll down and click OK.</td>
<td><img src="./images/media/image109.png" style="width:2.48611in;height:1.7001in" /></td>
</tr>
<tr class="odd">
<td>38</td>
<td>In the Visual Process Designer, click ‘<strong>Save</strong>’ to save the changes to the process.</td>
<td><img src="./images/media/image110.png" style="width:3.44444in;height:2.31161in" /></td>
</tr>
<tr class="even">
<td>39</td>
<td><p>We need to repeat these steps for one more process.</p>
<p>Click on ‘Processes’ next to ‘emerald-TestHub’ in the crumb trail as shown to the right</p></td>
<td><img src="./images/media/image111.png" style="width:3.84698in;height:2.47242in" /></td>
</tr>
<tr class="odd">
<td>40</td>
<td>Click on the ‘<strong>Run Automated Test for Web Console</strong>’ process</td>
<td><img src="./images/media/image112.png" style="width:4.09834in;height:2.27685in" /></td>
</tr>
<tr class="even">
<td>41</td>
<td><p>The Visual Process Designer will appear for the process.</p>
<p>Click the pencil icon on the step ‘<strong>Run IBM Rational Test Automation Server test</strong>’ as shown to the right.</p></td>
<td><img src="./images/media/image113.png" style="width:3.25826in;height:2.15278in" /></td>
</tr>
<tr class="odd">
<td>42</td>
<td>Paste the API Key from your Text Editor into the ‘<strong>Offline Token</strong>’ field as shown to the right.</td>
<td><img src="./images/media/image114.png" style="width:2.84763in;height:1.95139in" /></td>
</tr>
<tr class="even">
<td>43</td>
<td>Scroll down and click the OK button</td>
<td><img src="./images/media/image115.png" style="width:2.28233in;height:1.56944in" /></td>
</tr>
<tr class="odd">
<td>44</td>
<td>In the Visual Process Designer view, click the ‘<strong>Save</strong>’ button to save your changes to the process.</td>
<td><img src="./images/media/image116.png" style="width:2.90625in;height:2.08967in" /></td>
</tr>
<tr class="even">
<td>45</td>
<td><p>You have completed this lab section!</p>
<p>In the next section, we will deploy our new BAR file to the DEV environment and an automated test will be executed in IBM DevOps Test Hub.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>End of Section - 3.4</strong></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Deploy the ACE Broker Archive using IBM DevOps Deploy to DEV

### Overview

In this lab section, we will deploy the built ACE broker archive file to
the DEV environment and invoke an automated API test using Rational Test
Automation Server (RTAS).

### Workbook steps

<table>
<thead>
<tr class="header">
<th><strong>Step</strong></th>
<th><strong>Details</strong></th>
<th><strong>Additional Information</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>Return to your IBM DevOps Deploy web console in your browser.</td>
<td></td>
</tr>
<tr class="even">
<td>2</td>
<td>Click on <strong>Applications</strong> at the top of the page</td>
<td><img src="./images/media/image117.png" style="width:3.2875in;height:0.89583in" /></td>
</tr>
<tr class="odd">
<td>3</td>
<td>Click on the ‘Emerald eStore’ application in the list</td>
<td></td>
</tr>
<tr class="even">
<td>4</td>
<td><p>Before we initiate the deployment, we will review the environment properties that are set for the DEV environment.</p>
<p>Click on the “DEV” text for the DEV environment as shown to the right.</p></td>
<td><img src="./images/media/image118.png" style="width:2.09236in;height:2.28731in" /></td>
</tr>
<tr class="odd">
<td>5</td>
<td>In the ‘Environment: DEV’ page, click on the ‘<strong>Configuration</strong>’ sub-tab</td>
<td><img src="./images/media/image119.png" style="width:2.13309in;height:1.03472in" /></td>
</tr>
<tr class="even">
<td>6</td>
<td>Click on ‘<strong>Environment Properties</strong>’ in the left-hand pane</td>
<td><img src="./images/media/image120.png" style="width:1.97222in;height:1.25489in" /></td>
</tr>
<tr class="odd">
<td>7</td>
<td><p>Here you will see the property values that are used in our automated deployment processes.</p>
<p>Notice the ACE specific properties that you saw referenced in the component process we reviewed in the previous lab.</p></td>
<td><img src="./images/media/image121.png" style="width:2.54525in;height:2.78472in" /></td>
</tr>
<tr class="even">
<td><strong>INFO</strong></td>
<td><p>If the way you deploy one BAR file is the same way you will deploy the other 10 BAR files you typically deploy, you can setup a reusable <strong>component template</strong> to handle these deploys. This provides two benefits:</p>
<ul>
<li><p>You can quickly on-board other ACE components based on the template</p></li>
<li><p>You have one place to make updates to the ACE deployment process (helping with maintenance)</p></li>
</ul>
<p>The use of properties, rather than hard-coded string values, is vital to the creation of reusable templates. Properties can be set at the environment, component, application, and resource scope in IBM DevOps Deploy.</p></td>
<td></td>
</tr>
<tr class="odd">
<td>8</td>
<td><p>Let’s initiate our deployment.</p>
<p>Click on “Emerald eStore” in the crumb trail at the top of the page.</p></td>
<td><img src="./images/media/image122.png" style="width:2.64792in;height:1.46186in" /></td>
</tr>
<tr class="even">
<td>9</td>
<td>Click the “<strong>Request Process</strong>” button for your DEV environment as shown to the right</td>
<td><img src="./images/media/image123.png" style="width:3.34028in;height:1.16141in" /></td>
</tr>
<tr class="odd">
<td>10</td>
<td>For the ‘Run Application Process’ page that appears, select the Process labeled ‘<strong>Deploy</strong> <strong>Emerald</strong>’ from the pulldown menu.</td>
<td><img src="./images/media/image124.png" style="width:2.79861in;height:2.42263in" /></td>
</tr>
<tr class="even">
<td>11</td>
<td><p>Click the ‘Choose Versions’ button to choose component versions.</p>
<p>A ‘Select Component Versions’ dialog will appear to the right.</p></td>
<td><img src="./images/media/image125.png" style="width:3.2875in;height:1.55972in" /></td>
</tr>
<tr class="odd">
<td>12</td>
<td>In the Select Component Versions dialog that appears to the right, click the ‘<strong>Select For All</strong>’ pulldown and choose ‘<strong>Latest Available</strong>’ as shown to the right</td>
<td><img src="./images/media/image126.png" style="width:2.51274in;height:2.75in" /></td>
</tr>
<tr class="even">
<td>13</td>
<td>You should see that the values in the ‘Versions to Deploy’ column look different from what is in the ‘Current Environment Inventory’ column.</td>
<td><img src="./images/media/image127.png" style="width:2.48889in;height:2.00678in" /></td>
</tr>
<tr class="odd">
<td>14</td>
<td>Back in the ‘Run Application Process’ page, notice that it shows that there are ‘2 Selected’ component versions for deployment.</td>
<td><img src="./images/media/image128.png" style="width:2.83784in;height:2.42361in" /></td>
</tr>
<tr class="even">
<td>15</td>
<td>Click the ‘<strong>Submit’</strong> button to initiate the deployment (as shown above)</td>
<td>NOTE: you can schedule the deployment for a specific day and time as well if you like.</td>
</tr>
<tr class="odd">
<td><strong>INFO</strong></td>
<td><strong>NOTE:</strong> We are running the deployment through the web console, however, keep in mind that this deployment could be initiated automatically following a build process. You can make REST or CLI calls to start deployments automatically from your Jenkins or GitLab pipeline.</td>
<td></td>
</tr>
<tr class="even">
<td>16</td>
<td><p>The deployment will start, and you will have a nice trail of audit for each deployment as you see to the right.</p>
<p>You can click ‘Expand All’ or manually expand the deployment for the BAR file.</p></td>
<td><img src="./images/media/image129.png" style="width:3.32222in;height:1.76989in" /></td>
</tr>
<tr class="odd">
<td>17</td>
<td><p>Click the layer cake (dots) pulldown menu to the right of the ‘<strong>Deploy’</strong> step as shown to the right.</p>
<p>Then click the ‘<strong>View Output Log’</strong> menu item for the pulldown menu</p></td>
<td><img src="./images/media/image130.png" style="width:3.2875in;height:1.22569in" /></td>
</tr>
<tr class="even">
<td>18</td>
<td><p>You can view the Output Log for any of the steps that were executed.</p>
<p>Here we see that the deployment of the BAR file was successful.</p></td>
<td><img src="./images/media/image131.png" style="width:2.67361in;height:2.18057in" /></td>
</tr>
<tr class="odd">
<td>19</td>
<td>Click the ‘Close’ button to close the Output Log dialog</td>
<td></td>
</tr>
<tr class="even">
<td>20</td>
<td>Notice that following the deployment that we are incorporating automated test execution to validate the ACE APIs using IBM DevOps Test Hub to run an automated API test suite.</td>
<td><img src="./images/media/image132.png" style="width:3.2875in;height:1.15764in" /></td>
</tr>
<tr class="odd">
<td><strong>INFO</strong></td>
<td><p>IBM DevOps Test Hub can run many different types of tests including:</p>
<ul>
<li><p>API Tests</p></li>
<li><p>Performance Tests</p></li>
<li><p>Functional Tests</p></li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<td>21</td>
<td><p>In your browser, return to the IBM DevOps Test Hub tab.</p>
<p>If you need to create a new tab, click the ‘<strong>DevOps Test Hub</strong>’ bookmark found the toolbar as shown to the right.</p></td>
<td><img src="./images/media/image133.png" style="width:3.2875in;height:1.48611in" /></td>
</tr>
<tr class="odd">
<td>22</td>
<td>Login to IBM DevOps Test Hub as the user <em><strong>techxchange</strong></em> with password of <em><strong>password</strong></em></td>
<td></td>
</tr>
<tr class="even">
<td>23</td>
<td><p>You will see your Active Projects in the view.</p>
<p>Click on the <strong>ACE</strong> project as highlighted to the right.</p></td>
<td><img src="./images/media/image134.png" style="width:3.2875in;height:1.22153in" /></td>
</tr>
<tr class="odd">
<td>24</td>
<td>In the ACE Overview page that appears, you can see the latest execution results.</td>
<td><img src="./images/media/image135.png" style="width:3.2875in;height:1.27361in" /></td>
</tr>
<tr class="even">
<td>25</td>
<td>In the left-hand menu, click on Analyze to expand the menu. Click on “Results” in the pulldown menu. This should show you all the Results from your tests as shown to the right.</td>
<td><img src="./images/media/image136.png" style="width:3.2875in;height:1.08542in" /></td>
</tr>
<tr class="odd">
<td>26</td>
<td>You can drill into the test logs for a given test run. Click on our latest test (click on the “ACETests” text) that was run against the DEV environment.</td>
<td><img src="./images/media/image137.png" style="width:3.2875in;height:1.09861in" /></td>
</tr>
<tr class="even">
<td>27</td>
<td><p>A dialog will appear to the right.</p>
<p>Click on the ‘Test Log’ link</p></td>
<td><img src="./images/media/image138.png" style="width:3.2875in;height:1.33958in" /></td>
</tr>
<tr class="odd">
<td>28</td>
<td>The Test Log will appear. Expand the ‘<strong>Create Scenario</strong>’ node in the left pane to see each test that was executed.</td>
<td><img src="./images/media/image139.png" style="width:3.2875in;height:1.01875in" /></td>
</tr>
<tr class="even">
<td>29</td>
<td>Expand the ‘<strong>Run Test – Hello ESQL</strong>’ test and examine the Send Message, Receive Message, and more to see the results of the test.</td>
<td><img src="./images/media/image140.png" style="width:3.2875in;height:1.63819in" /></td>
</tr>
<tr class="odd">
<td>30</td>
<td><p>Return to the IBM DevOps Deploy tab in your browser.</p>
<p>The deployment of both the ACE BAR and the Emerald web application should succeed as shown to the right.</p></td>
<td><img src="./images/media/image141.png" style="width:3.2875in;height:1.42361in" /></td>
</tr>
<tr class="even">
<td>31</td>
<td>Click on ‘Emerald eStore’ in the crumb trail as shown to the right</td>
<td><img src="./images/media/image142.png" style="width:1.97917in;height:0.88799in" /></td>
</tr>
<tr class="odd">
<td>32</td>
<td>Expand the DEV environment to see that the inventory has been updated to reflect the component versions that you deployed.</td>
<td><img src="./images/media/image143.png" style="width:3.2875in;height:1.60417in" /></td>
</tr>
<tr class="even">
<td>33</td>
<td>Click on the ‘emerald-ACE-BAR’ component</td>
<td></td>
</tr>
<tr class="odd">
<td>34</td>
<td><p>Notice that version 3.0.30 that we just deployed and ran automated tests against now has a ‘<strong>Functional Tests Passed</strong>’ status added to it.</p>
<p>In IBM DevOps Deploy, you can use these status values to ensure <strong>Gate criteria</strong> are met before a deployment occurs to the next environment.</p>
<p>This helps to ensure good quality code is progressing through your pipeline using IBM DevOps Deploy.</p></td>
<td><img src="./images/media/image144.png" style="width:2.43463in;height:2.25in" /></td>
</tr>
<tr class="even">
<td>35</td>
<td><p>Let’s go check what was deployed.</p>
<p>In your browser, create a new tab.</p>
<p>Click the “IBM ACE – INODEDEV” bookmark to open this page.</p></td>
<td><img src="./images/media/image145.png" style="width:3.2875in;height:1.38681in" /></td>
</tr>
<tr class="odd">
<td>36</td>
<td>Click on “Emerald-ACE-DEV” or select “Open” from the layer cake pulldown menu item to see that the JGRACEIVT API has been deployed to this Integration Server.</td>
<td><img src="./images/media/image146.png" style="width:1.23393in;height:1.82639in" /></td>
</tr>
<tr class="even">
<td>37</td>
<td><p>If you open the JGRACEIVT API, you can see the REST APIs that are available for it as shown to the right.</p>
<p><strong>NOTE:</strong> Our DevOps Test Hub automated test exercised these APIs to ensure they were working properly.</p></td>
<td><img src="./images/media/image147.png" style="width:3.2875in;height:1.29236in" /></td>
</tr>
<tr class="odd">
<td>38</td>
<td><p>In your browser window, view the Emerald web application running in the DEV environment by opening a new tab and navigating to:</p>
<p><a href="http://192.168.252.201:3001/">http://192.168.252.201:3001/</a></p>
<p>You should see the application as shown to the right.</p></td>
<td><img src="./images/media/image148.png" style="width:3.2875in;height:1.47847in" /></td>
</tr>
<tr class="even">
<td>39</td>
<td><p>You have successfully deployed the ACE BAR to the DEV environment along with the Emerald web application!</p>
<p>We will promote our updates to the QA environment in the next lab.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>End of Section – 3.5</strong></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Promote the Emerald Components to the QA Environment

### Overview

In this lab section, we will deploy the built ACE broker archive file to
the QA environment and invoke an automated API test using Rational Test
Automation Server (RTAS). We will review the results.

### Workbook steps

<table>
<thead>
<tr class="header">
<th><strong>Step</strong></th>
<th><strong>Details</strong></th>
<th><strong>Additional Information</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>In your browser, return to the IBM DevOps Deploy tab.</td>
<td></td>
</tr>
<tr class="even">
<td>2</td>
<td>Click on the ‘<strong>Applications’</strong> tab at the top of the page and click on the ‘<strong>Emerald eStore</strong>’ application as shown to the right.</td>
<td><img src="./images/media/image149.png" style="width:4.1625in;height:1.17778in" /></td>
</tr>
<tr class="odd">
<td>3</td>
<td>Expand the DEV environment to show what is currently deployed to the DEV environment.</td>
<td><img src="./images/media/image150.png" style="width:4.1625in;height:2.04514in" /></td>
</tr>
<tr class="even">
<td>4</td>
<td><p>One of the nice features of IBM DevOps Deploy is that you can create a Snapshot of an environment.</p>
<p>This allows you to easily promote what you have tested together (the component versions for the ACE and WEB components) to the next environment.</p>
<p>Click on the ‘<strong>camera</strong>’ icon for the DEV environment as shown to the right to create a Snapshot.</p></td>
<td><img src="./images/media/image151.png" style="width:4.1625in;height:1.64028in" /></td>
</tr>
<tr class="odd">
<td>5</td>
<td><p>Enter the following values in the ‘Create Snapshot’ dialog that appears:</p>
<p>Name: 2024-Nov-01</p>
<p>You may optionally add a description similar to what is shown in the screen capture to the right.</p></td>
<td><img src="./images/media/image152.png" style="width:2.38849in;height:1.67382in" /></td>
</tr>
<tr class="even">
<td>6</td>
<td><p>Click the ‘<strong>Save</strong>’ button</p>
<p>The snapshot page will appear.</p></td>
<td></td>
</tr>
<tr class="odd">
<td>7</td>
<td>Click on the ‘Component Versions’ sub-tab as shown to the right.</td>
<td><img src="./images/media/image153.png" style="width:3.58993in;height:1.52425in" /></td>
</tr>
<tr class="even">
<td>8</td>
<td><p>Notice that the current inventory of the DEV environment was added as Component Versions for the snapshot.</p>
<p><strong>NOTE:</strong> you can press the ‘Lock Versions’ button to ensure this snapshot cannot be modified.</p></td>
<td><img src="./images/media/image154.png" style="width:4.1625in;height:1.44306in" /></td>
</tr>
<tr class="odd">
<td>9</td>
<td>In the crumb trail at the top, click on ‘Emerald eStore’</td>
<td><img src="./images/media/image155.png" style="width:3.32374in;height:0.86005in" /></td>
</tr>
<tr class="even">
<td>10</td>
<td><p>Let’s examine our QA environment to see that we have setup an approval process before a deployment can take place.</p>
<p>Click on the text ‘QA’ for the QA environment.</p></td>
<td><img src="./images/media/image156.png" style="width:1.84722in;height:2.43646in" /></td>
</tr>
<tr class="odd">
<td>11</td>
<td>Click on the ‘Configuration’ sub-tab as shown to the right.</td>
<td><img src="./images/media/image157.png" style="width:2.28472in;height:0.88965in" /></td>
</tr>
<tr class="even">
<td>12</td>
<td>On the Basic Settings page that appears, scroll down to the ‘Deployment Approvals’ section and notice that the ‘Require Manual Approvals’ is enabled (or checked) as shown to the right.</td>
<td><img src="./images/media/image158.png" style="width:2.7247in;height:3.9375in" /></td>
</tr>
<tr class="odd">
<td>13</td>
<td>Click on the ‘<strong>Manual Approval Process</strong>’ sub-tab that appears</td>
<td><img src="./images/media/image159.png" style="width:3.11111in;height:0.93375in" /></td>
</tr>
<tr class="even">
<td>14</td>
<td>In the process design that appears, slide the ‘Autolayout’ slider to the on position.</td>
<td><img src="./images/media/image160.png" style="width:2.34722in;height:1.28757in" /></td>
</tr>
<tr class="odd">
<td>15</td>
<td><p>Drag and drop the ‘Environment Approval Task’ step in the left-hand palette to the process design.</p>
<p><strong>NOTE:</strong> Using the Autolayout feature, the process design will automatically connect the Start and Finish steps for you.</p></td>
<td><img src="./images/media/image161.png" style="width:2.95139in;height:2.31374in" /></td>
</tr>
<tr class="even">
<td>16</td>
<td>Click the pencil icon for the ‘Environment Approval’ step to edit it</td>
<td></td>
</tr>
<tr class="odd">
<td>17</td>
<td><p>The properties of the step will be displayed.</p>
<p>Take the defaults as shown and scroll down and click OK.</p></td>
<td><img src="./images/media/image162.png" style="width:2.19028in;height:2.2239in" /></td>
</tr>
<tr class="even">
<td>18</td>
<td>Click ‘Save’ to save your approval process.</td>
<td><img src="./images/media/image163.png" style="width:2.83333in;height:2.15076in" /></td>
</tr>
<tr class="odd">
<td>19</td>
<td>Click on ‘Emerald eStore’ in the crumb-trail at the top to return to the application.</td>
<td><img src="./images/media/image164.png" style="width:3.06944in;height:0.5254in" /></td>
</tr>
<tr class="even">
<td>20</td>
<td><p>In IBM DevOps Deploy, you can compare inventory of one environment to another.</p>
<p>Click the layer-cake icon next to the DEV environment and then click ‘<strong>Compare</strong>’ from the pull-down menu as shown to the right.</p></td>
<td><img src="./images/media/image165.png" style="width:4.1625in;height:1.47083in" /></td>
</tr>
<tr class="odd">
<td>22</td>
<td>In the ‘Compare Environments’ dialog that appears, choose the QA environment from the pull-down menu.</td>
<td><img src="./images/media/image166.png" style="width:1.93056in;height:1.35049in" /></td>
</tr>
<tr class="even">
<td>23</td>
<td>Click ‘Compare’</td>
<td></td>
</tr>
<tr class="odd">
<td>24</td>
<td>An Environment Comparison page will be displayed so you can see the inventory differences between the DEV and QA environments.</td>
<td><img src="./images/media/image167.png" style="width:4.1625in;height:1.47083in" /></td>
</tr>
<tr class="even">
<td>25</td>
<td><p>Let’s deploy the snapshot to the QA environment.</p>
<p>Click on ‘Emerald eStore’ in the crumb-trail as you have before to return the main page for the application.</p></td>
<td><img src="./images/media/image168.png" style="width:2.09722in;height:0.70257in" /></td>
</tr>
<tr class="odd">
<td>26</td>
<td>Click the ‘Request Process’ button next to the QA environment</td>
<td><img src="./images/media/image169.png" style="width:4.1625in;height:1.33611in" /></td>
</tr>
<tr class="even">
<td>27</td>
<td>In the ‘Run Application Process’ page that appears, select ‘Deploy Emerald’ from the Process pulldown menu.</td>
<td><img src="./images/media/image170.png" style="width:3.46043in;height:2.28098in" /></td>
</tr>
<tr class="odd">
<td>28</td>
<td>In the ‘Select a Snapshot’ pulldown, select ‘2024-Nov-01’ as shown to the right.</td>
<td><img src="./images/media/image171.png" style="width:3.51413in;height:2.22257in" /></td>
</tr>
<tr class="even">
<td>29</td>
<td>Scroll down and click the ‘<strong>Submit</strong>’ button to initiate the deployment.</td>
<td><img src="./images/media/image172.png" style="width:4.1625in;height:3.13611in" /></td>
</tr>
<tr class="odd">
<td>30</td>
<td><p>Notice that the deployment is waiting for an approval before it can begin.</p>
<p><strong>Before we respond to this approval request</strong>, we are going to disable all future approval requirements just for this lab.</p>
<p><strong>Click on</strong> ‘<strong>Emerald eStore</strong>’ in the crumb-trail as you have before</p></td>
<td><img src="./images/media/image173.png" style="width:4.1625in;height:1.60764in" /></td>
</tr>
<tr class="even">
<td>31</td>
<td>Click on the QA environment text</td>
<td><img src="./images/media/image174.png" style="width:1.57232in;height:1.97917in" /></td>
</tr>
<tr class="odd">
<td>32</td>
<td>Click on the ‘Configuration’ sub-tab and scroll down to <strong>uncheck</strong> the ‘<strong>Require Manual Approvals</strong>’ checkbox as shown to the right.</td>
<td><img src="./images/media/image175.png" style="width:1.8128in;height:2.17361in" /></td>
</tr>
<tr class="even">
<td>33</td>
<td>Scroll down and click ‘<strong>Save</strong>’</td>
<td><img src="./images/media/image176.png" style="width:4.1625in;height:1.59514in" /></td>
</tr>
<tr class="odd">
<td>34</td>
<td>Let’s return to our deployment. Click on the ‘Work Items’ tab at the top of the page.</td>
<td><img src="./images/media/image177.png" style="width:4.1625in;height:0.96528in" /></td>
</tr>
<tr class="even">
<td>35</td>
<td><p>Click the layer cake icon next to the QA approval request and select ‘View Request’ as shown to the right.</p>
<p>This will take us back to our deployment request.</p></td>
<td><img src="./images/media/image178.png" style="width:4.1625in;height:1.075in" /></td>
</tr>
<tr class="odd">
<td>36</td>
<td>After reviewing the deployment, click the layer-cake icon to the right and select ‘<strong>Respond</strong>’ from the pulldown menu.</td>
<td><img src="./images/media/image179.png" style="width:4.1625in;height:1.5625in" /></td>
</tr>
<tr class="even">
<td>37</td>
<td><p>In the Respond dialog that appears, select ‘Approve’ from the response choice menu item and add an optional comment.</p>
<p>Click <strong>Submit</strong></p></td>
<td><img src="./images/media/image180.png" style="width:3.86111in;height:1.87967in" /></td>
</tr>
<tr class="odd">
<td>38</td>
<td>The deployment process will begin to the QA environment and you can view the progress of the deployment.</td>
<td><img src="./images/media/image181.png" style="width:4.1625in;height:1.63819in" /></td>
</tr>
<tr class="even">
<td>39</td>
<td><p>The deployment of the ACE BAR should succeed to QA just as it did earlier for the DEV environment.</p>
<p>The automated IBM DevOps Test Hub functional test will run against the API in the QA environment.</p></td>
<td><img src="./images/media/image182.png" style="width:4.1625in;height:1.81181in" /></td>
</tr>
<tr class="odd">
<td>40</td>
<td><p>Likewise, the deployment of the emerald WEB component should succeed as well.</p>
<p><strong>NOTE:</strong> we are running functional tests against the web component as well using IBM DevOps Test Hub.</p></td>
<td><img src="./images/media/image183.png" style="width:4.1625in;height:1.47847in" /></td>
</tr>
<tr class="even">
<td>41</td>
<td><p>Optionally, review the test results in IBM DevOps Test Hub by switching to that tab in your browser.</p>
<p>For the ACE project, click on ‘Analyze’ in the left-hand pane and then click on ‘Results’.</p></td>
<td><img src="./images/media/image184.png" style="width:4.1625in;height:1.47083in" /></td>
</tr>
<tr class="odd">
<td>42</td>
<td><p>Optionally, review the test results in IBM DevOps Test Hub for the ‘Emerald’ project.</p>
<p>For the Emerald project, click on ‘Analyze’ in the left-hand pane and then click on ‘Results’.</p>
<p>In the right hand Results view, click on the ‘Tests’ sub-tab as shown to the right.</p></td>
<td><img src="./images/media/image185.png" style="width:4.1625in;height:1.38889in" /></td>
</tr>
<tr class="even">
<td>43</td>
<td>In your IBM DevOps Deploy tab, return to the ‘Emerald eStore’ application view.</td>
<td></td>
</tr>
<tr class="odd">
<td>44</td>
<td>Notice that inventory is updated for the QA environment to show that the snapshot has been deployed</td>
<td><img src="./images/media/image186.png" style="width:4.1625in;height:1.46667in" /></td>
</tr>
<tr class="even">
<td>45</td>
<td>In your browser, create a new tab and click the ‘IBM ACE – INODEQA’ bookmark</td>
<td><img src="./images/media/image187.png" style="width:4.1625in;height:1.76736in" /></td>
</tr>
<tr class="odd">
<td>46</td>
<td>Open the Emerald-ACE-QA integration server to see that the JGRACEIVT API is deployed as expected.</td>
<td><img src="./images/media/image188.png" style="width:2.32831in;height:3.125in" /></td>
</tr>
<tr class="even">
<td>47</td>
<td><p>In your browser window, view the Emerald web application by opening a new tab and navigating to:</p>
<p><a href="http://192.168.252.201:3002/">http://192.168.252.201:3002/</a></p>
<p>You should see the application as shown to the right.</p></td>
<td><img src="./images/media/image189.png" style="width:4.1625in;height:1.98958in" /></td>
</tr>
<tr class="odd">
<td>48</td>
<td>Congratulations! You have successfully promoted the BAR file as well as the web component.</td>
<td></td>
</tr>
<tr class="even">
<td><strong>End of Section – 3.6</strong></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Publishing a Product to API Connect using IBM DevOps Deploy

### Overview

IBM API Connect is a full lifecycle API management solution that uses
you create, manage, secure, socialize, and monetize APIs. In this final
lab, you will publish a product, which includes APIs you want to
socialize to your end users in a secure manner. The product will be
published to a ‘sandbox’ catalog that is already setup and ready for you
to use in a DEV environment.

**NOTE**: this Lab is leveraging an API Connect instance that is running
in the IBM Cloud. Each student in the lab will be provided a unique
login and password to authenticate with this API Connect instance.

### Workbook steps

<table>
<thead>
<tr class="header">
<th><strong>Step</strong></th>
<th><strong>Details</strong></th>
<th><strong>Additional Information</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td><p>For this lab, each student will be assigned a student number which will provide you with a unique login credential as well as an organization to use for API Connect.</p>
<p>Open or return to a terminal window and run this command:</p>
<p># cd /home/sysadmin/scripts</p>
<p># ls -al</p>
<p>You should see a ‘student-passwords.txt’ file as shown to the right.</p></td>
<td><img src="./images/media/image190.png" style="width:3.59028in;height:1.56524in" /></td>
</tr>
<tr class="even">
<td>2</td>
<td><p>Run this command:</p>
<p># cat student-passwords.txt</p>
<p><strong>NOTE:</strong> your login will be ‘studentxx’ based on your number. For this example, I will be using ‘student20’.</p></td>
<td><img src="./images/media/image191.png" style="width:2.81944in;height:2.04443in" /></td>
</tr>
<tr class="odd">
<td>3</td>
<td><p>For your student id, copy the line which contains your password.</p>
<p>For this example, I am using ‘student20’ so I copy the last line to my buffer.</p></td>
<td><img src="./images/media/image192.png" style="width:1.58333in;height:1.24049in" /></td>
</tr>
<tr class="even">
<td>4</td>
<td>Return to your ‘Text Editor’ window that you had opened earlier. Paste the student password into this file for future reference.</td>
<td><img src="./images/media/image193.png" style="width:2.89583in;height:0.65578in" /></td>
</tr>
<tr class="odd">
<td>5</td>
<td>Return to your Firefox browser and your IBM DevOps Deploy tab.</td>
<td></td>
</tr>
<tr class="even">
<td>6</td>
<td>Click on the ‘Components’ tab at the top of the page as shown to the right.</td>
<td><img src="./images/media/image194.png" style="width:3.38318in;height:1.64329in" /></td>
</tr>
<tr class="odd">
<td>7</td>
<td><p>You will see a ‘emerald-APIC-Product’ component in the list.</p>
<p>Click on the ‘<strong>emerald-APIC-Product</strong>’ component text</p></td>
<td></td>
</tr>
<tr class="even">
<td>8</td>
<td>Notice we have a component version already this component. Let’s examine this by clicking on the ‘4.1.9’ component version.</td>
<td><img src="./images/media/image195.png" style="width:3.02083in;height:1.52854in" /></td>
</tr>
<tr class="odd">
<td>9</td>
<td><p>You will see that the component version consists of two yaml files:</p>
<ul>
<li><p>jgraceivt-product_1.0.1.yaml</p></li>
<li><p>jgraceivt-api_1.0.0.yaml</p></li>
</ul>
<p>The ‘product’ yaml describes your product that you want to publish to a catalog to expose the ‘api’ that it references which is in the ‘api’ yaml file above.</p></td>
<td><img src="./images/media/image196.png" style="width:3.53889in;height:2.98697in" /></td>
</tr>
<tr class="even">
<td>10</td>
<td>Click on ‘emerald-APIC-Product’ in the crumb trail as shown to the right to return to the component.</td>
<td><img src="./images/media/image197.png" style="width:3.125in;height:0.95646in" /></td>
</tr>
<tr class="odd">
<td>11</td>
<td>Click on the ‘Configuration’ sub-tab</td>
<td><img src="./images/media/image198.png" style="width:3.11806in;height:1.64802in" /></td>
</tr>
<tr class="even">
<td>12</td>
<td>Click on ‘Component Properties’ in the left-hand pane</td>
<td><img src="./images/media/image199.png" style="width:2.66667in;height:2.30366in" /></td>
</tr>
<tr class="odd">
<td>13</td>
<td>You will see the component properties that will be used by our deployment process listed in the right-hand pane.</td>
<td><img src="./images/media/image200.png" style="width:3.67213in;height:2.06944in" /></td>
</tr>
<tr class="even">
<td>14</td>
<td>For the <strong>apic.username</strong> and <strong>apic.password</strong> properties, use the three dots (layer cake) menu item and select ‘<strong>Edit’</strong> to change these values to your studentxx number you were assigned and the password found in your Text Editor.</td>
<td><img src="./images/media/image201.png" style="width:3.65768in;height:0.34742in" /></td>
</tr>
<tr class="odd">
<td>15</td>
<td><p>The values for the ‘apic.username’ and ‘apic.password’ should reflect what you were assigned as shown to the right.</p>
<p><strong>NOTE:</strong> you can ‘secure’ passwords in IBM DevOps Deploy where a user cannot see them.</p></td>
<td><img src="./images/media/image202.png" style="width:2.7062in;height:3.06944in" /></td>
</tr>
<tr class="even">
<td>16</td>
<td>In the component properties list, scroll down to the ‘<strong>apic</strong>.<strong>organization’</strong> property.</td>
<td><img src="./images/media/image203.png" style="width:3.22917in;height:1.44121in" /></td>
</tr>
<tr class="odd">
<td>17</td>
<td><p>Edit this value to be ‘<strong>techxchange</strong>-<strong>org</strong>-<strong>xx’</strong> where xx is your student number.</p>
<p>In my case, it is ‘techxchange-org-20’ as shown to the right.</p></td>
<td><img src="./images/media/image204.png" style="width:2.86111in;height:0.43921in" /></td>
</tr>
<tr class="even">
<td>18</td>
<td><p>We will now quickly review the component process for deployment.</p>
<p>Click on the ‘Processes’ sub-tab as shown to the right.</p></td>
<td><img src="./images/media/image205.png" style="width:2.72833in;height:2.18056in" /></td>
</tr>
<tr class="odd">
<td>19</td>
<td>Click on the ‘Publish-Product’ process</td>
<td><img src="./images/media/image206.png" style="width:3.19804in;height:1.36565in" /></td>
</tr>
<tr class="even">
<td>20</td>
<td><p>The visual process designer will appear.</p>
<p>The process starts with a ‘Download Artifacts’ step that will download the yaml files to a host that has the API Connect Toolkit installed.</p>
<p>The second step will replace tokens in the ‘jgraceivt-api_1.0.0.yaml’ file with environment properties set in DevOps Deploy. At time of deployment, these values will be substituted (these values can vary from one environment to the next). Here is our example:</p>
<p><img src="./images/media/image207.png" style="width:1.57569in;height:0.90539in" /></p>
<p>The third and fourth steps of the process use the APIC plugin steps to Login and ‘Publish the API Product Definition’ to your API Connect target environment catalog.</p></td>
<td><img src="./images/media/image208.png" style="width:3.21944in;height:2.89003in" /></td>
</tr>
<tr class="odd">
<td>21</td>
<td>Click the pencil icon for the ‘Publish API Product Definitions’ step.</td>
<td></td>
</tr>
<tr class="even">
<td>22</td>
<td>Notice the use of the component properties that we reviewed and updated.</td>
<td><img src="./images/media/image209.png" style="width:2.49977in;height:2.47917in" /></td>
</tr>
<tr class="odd">
<td>23</td>
<td>Scroll down and click <strong>Cancel</strong> to close the ‘Edit Properties’ dialog without making any changes.</td>
<td><img src="./images/media/image210.png" style="width:1.95736in;height:1.29594in" /></td>
</tr>
<tr class="even">
<td>24</td>
<td><p>In your visual process design view, type ‘API Connect’ in the ‘Type to filter’ search text field as shown to the right.</p>
<p>This will show you the plugin steps that come with the ‘IBM API Connect’ automation plugin that you can leverage in IBM DevOps Deploy.</p>
<p><strong>NOTE</strong>: IBM DevOps Deploy has plugins for MQ, DataPower and other technologies that many of our clients manage to run operational processes (e.g. ‘Create Queue Manager’) or deployment processes.</p></td>
<td><img src="./images/media/image211.png" style="width:3.14839in;height:2.70139in" /></td>
</tr>
<tr class="odd">
<td>25</td>
<td>In the crumb trail at the top, click on ‘<strong>emerald</strong>-<strong>APIC</strong>-<strong>Product’</strong> to return to the component view.</td>
<td><img src="./images/media/image212.png" style="width:3.14792in;height:1.24632in" /></td>
</tr>
<tr class="even">
<td>26</td>
<td><p>At the top of the Components view, you will see a ‘Used By’ field as shown to the right.</p>
<p>Click on ‘<strong>Emerald</strong> <strong>eStore’</strong> to return to the application.</p></td>
<td><img src="./images/media/image213.png" style="width:2.86806in;height:1.49403in" /></td>
</tr>
<tr class="odd">
<td>27</td>
<td><p>From the Application view, we will now deploy our API Connect product to the DEV environment.</p>
<p>Click on the ‘Request Process’ button for the DEV environment as shown to the right.</p></td>
<td><img src="./images/media/image214.png" style="width:3.65278in;height:1.34218in" /></td>
</tr>
<tr class="even">
<td>28</td>
<td>In the Run Application Process page that appears, for the Process pull-down menu, select ‘<strong>Deploy</strong> <strong>Emerald</strong> <strong>APIC’</strong></td>
<td><img src="./images/media/image215.png" style="width:3.13889in;height:2.19722in" /></td>
</tr>
<tr class="odd">
<td>29</td>
<td>Click the ‘Choose Component Versions’ button</td>
<td><img src="./images/media/image216.png" style="width:2.86806in;height:1.0841in" /></td>
</tr>
<tr class="even">
<td>30</td>
<td>From the ‘Select for All’ pulldown that appears, select the ‘<strong>Latest</strong> <strong>Available’</strong></td>
<td><img src="./images/media/image217.png" style="width:2.04314in;height:2.11806in" /></td>
</tr>
<tr class="odd">
<td>31</td>
<td>You should see version 4.1.9 selected to be deployed</td>
<td><img src="./images/media/image218.png" style="width:3.54167in;height:1.29819in" /></td>
</tr>
<tr class="even">
<td>32</td>
<td>Scroll down and click the ‘Submit’ button</td>
<td><img src="./images/media/image219.png" style="width:3.125in;height:1.41509in" /></td>
</tr>
<tr class="odd">
<td>33</td>
<td>The deployment will begin. You can click the ‘Expand All’ link to show each step that is executed with the deployment.</td>
<td><img src="./images/media/image220.png" style="width:3.44861in;height:1.35366in" /></td>
</tr>
<tr class="even">
<td>34</td>
<td>The deployment should succeed as shown above.</td>
<td></td>
</tr>
<tr class="odd">
<td>35</td>
<td>View the output for the ‘Login’ step by clicking on the layer cake (three dot) icon to the right of the step and then select ‘View Output Log’</td>
<td><img src="./images/media/image221.png" style="width:5.12917in;height:1.24949in" /></td>
</tr>
<tr class="even">
<td>36</td>
<td><p>You should see ‘Authentication completed successfully’ as shown to the right.</p>
<p>Click ‘Close’ to close the Output Log dialog window.</p></td>
<td><img src="./images/media/image222.png" style="width:3.58752in;height:2.93056in" /></td>
</tr>
<tr class="odd">
<td>37</td>
<td>Repeat the same steps to view the output for the ‘Publish API Product Definitions’ step.</td>
<td><img src="./images/media/image223.png" style="width:5.00417in;height:1.21904in" /></td>
</tr>
<tr class="even">
<td>38</td>
<td><p>You should see the ‘[state: published]’ message as shown to the right along with a ‘Successfully published definition’ message in the output log.</p>
<p>Click Close to close the Output Log dialog window.</p></td>
<td><img src="./images/media/image224.png" style="width:3.94861in;height:3.23962in" /></td>
</tr>
<tr class="odd">
<td>39</td>
<td>Open a new tab in your browser. Click on the ‘API Connect’ bookmark as shown to the right.</td>
<td><img src="./images/media/image225.png" style="width:2.74306in;height:0.83669in" /></td>
</tr>
<tr class="even">
<td>40</td>
<td><p>The API Connect Login Page will appear.</p>
<p>For the Username field, enter your <strong>studentxx</strong> number.</p>
<p>Copy the studentxx password from your Text Editor window. Paste this value into the Password field.</p></td>
<td><img src="./images/media/image226.png" style="width:3.34028in;height:1.45785in" /></td>
</tr>
<tr class="odd">
<td>41</td>
<td>Click the ‘Log in’ button.</td>
<td></td>
</tr>
<tr class="even">
<td>42</td>
<td>Click on the ‘<strong>Manage</strong> <strong>catalogs’</strong> tile as shown to the right.</td>
<td><img src="./images/media/image227.png" style="width:4.025in;height:1.97858in" /></td>
</tr>
<tr class="odd">
<td>43</td>
<td>Click on the ‘Sandbox’ catalog</td>
<td><img src="./images/media/image228.png" style="width:2.69632in;height:1.63472in" /></td>
</tr>
<tr class="even">
<td>44</td>
<td>You should see the ‘JGRACEIVT Product’ in the list of products following your deployment as shown to the right!</td>
<td><img src="./images/media/image229.png" style="width:3.32951in;height:0.9154in" /></td>
</tr>
<tr class="odd">
<td>45</td>
<td>By clicking on the layer cake (three dot) menu to the right, select ‘Manage APIs’ to view the APIs that are securely exposed to end users.</td>
<td><img src="./images/media/image230.png" style="width:4.83056in;height:2.61835in" /></td>
</tr>
<tr class="even">
<td>46</td>
<td><p>Here you see the APIs included with the product.</p>
<p>Click the ‘Close’ button</p></td>
<td><img src="./images/media/image231.png" style="width:4.69167in;height:1.46388in" /></td>
</tr>
<tr class="odd">
<td>47</td>
<td>Repeat the same process to view the plans by clicking the ‘View Plans’ menu item.</td>
<td><img src="./images/media/image232.png" style="width:4.74722in;height:2.59342in" /></td>
</tr>
<tr class="even">
<td>48</td>
<td>You will see there is a ‘Default Plan’ as well as a ‘Premium Plan’ provided for this API that end users can subscribe to.</td>
<td><img src="./images/media/image233.png" style="width:5.04583in;height:1.71997in" /></td>
</tr>
<tr class="odd">
<td>49</td>
<td>You have completed the lab!</td>
<td></td>
</tr>
<tr class="even">
<td><strong>End of Section – 3.7</strong></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

# Wrapping Things Up

## Lab Re-Cap

Congratulations\!

In this workbook you have gone through the process of integrating IBM
DevOps capabilities with IBM App Connect Enterprise (ACE) and API
Connect to provide an end-to-end DevOps experience. By executing each
lab, you were able to:

  - Explore IBM App Connect Enterprise (ACE) and how one can create,
    build, and deploy APIs from both the ACE Toolkit IDE and through a
    pipeline like Jenkins which integrates with DevOps Deploy to handle
    the deployment.

  - Explore IBM DevOps Deploy and its application model which includes
    target environments, components, and processes. We explored how to
    setup processes to handle the deployment of both IBM App Connect
    Enterprise (ACE) and API Connect assets in the labs.

  - Explore Rational Test Automation Server (RTAS) and how it can run
    automated tests and be triggered automatically as part of a
    deployment process.

  - Explore IBM API Connect and how you can automate the publish of a
    product to a target catalog using DevOps Deploy. IBM API Connect is
    a full lifecycle API management solution that is used to create,
    manage, secure, socialize, and monetize APIs.

For more information on each solution, please refer to the documentation
links below:

> **IBM DevOps Test Hub Overview** -
> <https://www.ibm.com/products/devops-test/hub>
> 
> **IBM DevOps Deploy Documentation** -
> <https://www.ibm.com/docs/en/urbancode-deploy/8.0.0?topic=notes-whats-new>
> 
> **IBM App Connect Enterprise Documentation** -
> <https://www.ibm.com/docs/en/app-connect/12.0?topic=overview-whats-new-in-version-120>
> 
> **IBM API Connect Overview** -
> <https://www.ibm.com/products/api-connect>
