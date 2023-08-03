# PRISMA CLOUD APPSEC BOOTCAMP


### Lab Introduction

Thank you for joining today’s AppSec camp. The lab will focus on application security throughout the software development lifecycle. Before we begin the lab let's start with a brief overview of the lab scenario to help frame the context.

### Scenario

The Exampli Corp, a mock corporation, is rushing to finish a new mobile banking app for their customers by the end of their fiscal quarter. Up against unrealistic goals the development and infrastructure teams are working around the clock to get their app built, tested, and released to hit their deadlines.

Fortunately, Exampli Corp recently integrated Prisma Cloud into their development lifecycle adopting security from code to cloud. Once in production Exampli Corps operations and security teams continue to leverage Prisma Cloud to monitor and protect runtime resources, reduce the attack surface, and enforce least privilege.

Will the Exampli Corp team take the time to build a secure app? Or will the stress of completing the Bank of Anthos app in time for deadlines lead to mistakes?

### Architecture 

The lab primarily focuses on Exampli Corp’s banking application known as the Bank of Anthos. The Bank of Anthos application is an example application purpose built for Google Kubernetes Engine, you can find the repo in the Resources section.

Prisma Cloud is integrated with mock company Exampli Corp in the following ways : 

1. Cloud Accounts are onboarded with Prisma Cloud allowing visibility into Exampli’s resources as well as their associated behavior and configuration states.

2. Critical applications in Exampli Corp’s cloud footprint are protected by Prisma Cloud defenders.

3. Code Repositories, Image Registries, and CI Tools are on-boarded into Prisma Cloud allowing for detection and remediation of misconfigurations and vulnerabilities earlier on in the development process.

### Resources

Vulnerable Repo:

In this lab we leverage some intentionally vulnerable code repository. To learn more about the project and its contributors visit the link below:

- https://github.com/bridgecrewio/supplygoat

Bank of Anthos Application:

In this lab there is a mock banking application that is used as the application the Exampli Corp is building. To learn more about the project and its contributors visit the link below:


- https://github.com/GoogleCloudPlatform/bank-of-anthos


### Exercise

Let's begin by exploring the power of shifting security left with Infrastructure as code scanning. As infrastructure is being defined as code security must be integrated with the tools developers use. In this exercise, we will take a look at some IaC templates within Exampli Corp’s repository.

### Software Composition Analysis:


1. Login to [Prisma Cloud](https://app3.prismacloud.io/auth/signin).

2. Use the credentials provided by your Instructor to authenticate.

3. Use the navigation pane on the left hand and click the **blue arrow** on the lower left side of the UI to open up the navigation pane and move between the different modules within Prisma Cloud.

![Alt text for image](/appsec_screenshots/software-composition-analysis-3.png "Optional title")

4. Next, use the navigation pane to select the **Code Security** module and then select **Projects**.

![Alt text for image](/appsec_screenshots/software-composition-analysis-4.png "Optional title")

5. Ensure that you select the **c-haisten/bank-of-anthos** repository.

![Alt text for image](/appsec_screenshots/software-composition-analysis-5-v2.png "Optional title")

6. Once you have selected the correct repository, it will show you all the security incidents found in the code of that branch. Let’s check to see if there are any serious vulnerabilities by filtering **Severities -> High.**

![Alt text for image](/appsec_screenshots/software-composition-analysis-6-v2.png "Optional title")

7. Next, we will select a CVE ID to investigate the vulnerability and determine what next steps to take. Prisma Cloud gives us several options for how to interact with the vulnerability.

Administrators can click suppress, or fix. The suppress button allows you to dismiss all incidents that fall under that specific policy violation. The fix button will allow you to remediate the vulnerability via a bump fix. Here we can see that the vulnerability can be fixed easily by bumping from v2.7.4 to 2.7.5.

**Suppress and Fix requires increased RBAC that is not available in this lab**

8. You can also click the “Details” or “Errors” tab on the right side of the page to get some more information on the dangers of the specific vulnerability.

![Alt text for image](/appsec_screenshots/software-composition-analysis-8-v2.png "Optional title")

9. This CVE has a CVSS score of 7. It makes Exampli Corp’s Bank of Anthos app vulnerable to information leaks and privilege escalation. 

On this page Exampli Corp developers can gain context on the CVE and click on the link to NIST providing them with all the details and documentation regarding the vulnerability.

10. In Prisma Cloud licenses are scanned in parallel to vulnerability scanning. This means that Exampli Corp developers can make sure they are remaining compliant when working with open source packages. Adjust your filter to **Category -> Licenses** and
let's see if there are any licensing issues in the Bank of Anthos Repo.

![Alt text for image](/appsec_screenshots/software-composition-analysis-10.png "Optional title")

11. Now, let's scroll down and look at some of the licensing issues identified by Prisma Cloud.

![Alt text for image](/appsec_screenshots/software-composition-analysis-11.png "Optional title")

12. By Clicking on the license type Prisma Cloud provides developers with critical information and identifies each policy violation as a single error.

![Alt text for image](/appsec_screenshots/software-composition-analysis-12.png "Optional title")

Now that we have found some vulnerabilities and licensing violations in our Application code, let's take a look at how Prisma Cloud can give us visibility to the package manager files that comprise applications by taking a look at the supply chain and software composition analysis (SCA).

### Supply Chain Security

1. Use the navigation pane on the left hand and click the **blue arrow** on the lower left side of the UI to open up the navigation pane and move between the different modules within Prisma Cloud.

![Alt text for image](/appsec_screenshots/supply-chain-security-1.png "Optional title")

2. Next, use the navigation pane to select the Code Security module and select Supply Chain.

![Alt text for image](/appsec_screenshots/supply-chain-security-2a.png "Optional title")

![Alt text for image](/appsec_screenshots/supply-chain-security-2b.png "Optional title")

3. Use the Supply Chain Graph to view the relationships between different IaC templates and the types of software packages and services they provision. Be sure to select the bank-of-anthos repository from the drop-down window in the filters at the top.

![Alt text for image](/appsec_screenshots/supply-chain-security-3.png "Optional title")

4. Next, take a deeper look at the **requirements.txt** file. Feel free to test the filters on the left side of the UI and search bar at the top to quickly locate templates.

![Alt text for image](/appsec_screenshots/supply-chain-security-4.png "Optional title")

5. Once you have found the **requirements.txt** file click on the first package that is unpacked, **cryptography: 38.0.1**. Notice on the right side of the UI there is additional information about this resource.

Here we can quickly identify valuable information like the package version, license type and privileges.

6. Your screen should look similar to the screenshot below.

![Alt text for image](/appsec_screenshots/supply-chain-security-6.png "Optional title")

7. Next, click on the **Errors** tab to investigate policy violations and vulnerabilities.

![Alt text for image](/appsec_screenshots/supply-chain-security-7.png "Optional title")

8. How many Vulnerabilities are associated with the **cryptography: 38.0.1** package? Read the **Details** section to discover more about the CVE and confirm the **Fix Version**. Are there other packages with a higher CVSS score?

Now that you have helped to protect the Bank of Anthos banking app Software Supply Chain, let’s take a look at the recent activity of the Exampli Corp developers.

### Protect Critical Applications

#### Visualize Applications and Establish Context 

The first step to protecting applications is to gain and maintain comprehensive visibility of your applications and all their associated resources. If Exampli Corp does not have oversight of their cloud environment it is impossible for them to stop emerging threats, respond to incidents, or reduce vulnerabilities. In a modern multi-cloud and hybrid world, applications are broken into different environments across the clouds like VMs, containers, serverless compute architecture types. Maintaining visibility is essential to protecting applications at runtime.

Prisma Cloud supports a massive amount of compute types, to review the supported systems check out our public documentation. (https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/install/system_requirements)

Let's help Exampli Corp get a clear picture of the application running on the vulnerable GKE cluster from the previous section. Start by taking a look at the microservices running the Bank of Anthos application using Prisma Cloud’s Radar feature.

1. The Radar feature lets you gain a bird’s eye view to monitor and understand your cloud applications. It helps you visualize the connectivity between microservices and search for vulnerabilities. Navigate to **Compute -> Radar -> Containers** and select the cluster **bank-of-anthos**.

![Alt text for image](/screenshots/maintaining-visibility-1.png "Optional title")

2. Once you have selected the correct cluster your screen should look similar the the screenshot below:

![Alt text for image](/screenshots/maintaining-visibility-2.png "Optional title")

3. Radar provides a visual depiction of the connections between containers, apps, and cluster services across your environment. Take some time to play around with the Radar feature and think through the following questions:

**What type of information can you learn by clicking on the nodes?
How does this visibility help you protect your applications?**

4. Let’s dive deeper into the **frontend:v0.5.5** microservice. Click on the associated container. Your screen should look similar to the screenshot below:

![Alt text for image](/screenshots/preventing-attacks-3-v2.png "Optional title")

5. Take some time to review the **Vulnerabilities** page.

![Alt text for image](/screenshots/preventing-attacks-4.png "Optional title")

6. Of the identified OS vulnerabilities, which one has the highest CVE? Do all the identified vulnerabilities contain a fix?

7. Take a look at the **Layers** tab to view the dockerfile that built this image and find where vulnerabilities were introduced.

![Alt text for image](/screenshots/preventing-attacks-6.png "Optional title")

8. Find the file that added the most severe vulnerabilities and open it up by clicking on it to learn more about specifically what CVEs were added. Your screen should look similar to the screen capture below :

![openssl-1](https://github.com/c-haisten/c2c_summit/assets/98335592/7d522d07-18c8-4ce0-afe2-4d12cb44d370)

**We can see that this particular file introduced a ton of vulnerabilities including the usage of openssl version 1.1 which is susceptable to a number of malicious exploits.** 

9. Now that we have established some understanding of this container and have found some CVE's lets expand our knowledge by observing this workload's behavior using Prisma Cloud's foresnic modeling capabilities. Click the back arrow at the top right hand side of the UI and arrive back at the container summary view. Your screen should look similar to the screen capture below :

![Alt text for image](/screenshots/preventing-attacks-3-v2.png "Optional title")

#### Modeleing Application Behavior

Prisma Cloud observes and logs behavior such as running processes, network behavior, and even binary executions. Prisma Cloud then takes this data and builds a model for each workload giving administrators an understanding of what is the normal working conditions of their applications. Armed with this information administrators both understand the behavior of their workloads and can prevent malicious actions from taking place.

1. Begin by clicking on the forensic microscope underneath the **Runtime** tab.

![forensic-model](https://github.com/c-haisten/c2c_summit/assets/98335592/39476dcb-54cc-418e-bca4-cfeeb42cac71)

2. Here you can see all the events displayed. Let’s take a deeper look at these events to get some details and see what has been happening with our bank-of-anthos-frontend.

![Alt text for image](/screenshots/investigate-incidents-at-runtime-5.png "Optional title")

3. To learn more please find the following documentation covering more details around runtime protection.(https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/runtime_defense/runtime_defense_containers)

4. Now let's take a look at a summary view of some of the suscipious behaviors taking place on this workload. Please click the close button at the bottom left of the UI. You should be back at the summary page and your screen should look similar to the screen capture below :

![Alt text for image](/screenshots/preventing-attacks-3.png "Optional title")

5. Next, click on **Runtime** tab on the summary view. Here we can view highlights from the container's behavior and see if there are any security concerns with what the container is doing.

![runtime-events](https://github.com/c-haisten/c2c_summit/assets/98335592/92d8f7c6-a14f-4a7a-8420-07afcedd0125)

6. On this screen you will find a summarized list of findings from the defender including behavior that is not in the container's model. Your screen should look similar to the screen capture below :

![runtime-summary](https://github.com/c-haisten/c2c_summit/assets/98335592/d751a357-11a1-437a-a0c3-95e30404752d)

7. Find the audit finding of a foriegn binary execution of tcpdump and click on it. If you have trouble finding it you can type tcpdump in the search bar at the top of the UI.

![runtime-summary-1](https://github.com/c-haisten/c2c_summit/assets/98335592/24adb5ff-5f69-43af-b388-8ab63ae9929b)

![runtime-summary-filter](https://github.com/c-haisten/c2c_summit/assets/98335592/d955e32c-eee3-45c2-8e80-3c9dd9d65d77)

8. This view provides an expanded understanding of the finding. We can see that Prisma Cloud alerted on this finding due to the default rule to alert on suspicious behavior. Administrators can configure their own rules alert on or block malicious activity.

9. Creating rules to defend applications is easy in Prisma Cloud. Use the navigation bar on the left hand side of the UI and select **Compute -> Defend -> Runtime**.

![runtime-rules](https://github.com/c-haisten/c2c_summit/assets/98335592/1332f7ea-c45f-4004-8eba-2d30a98b9cfc)

10. On this page administrators can configure rules that make sense for their applications. There is a great deal of granularity given to Prisma Cloud administrators to configure allowed process, networking, and file system actitivies. Prisma Cloud defenders are also integrated with Palo Alto Network's WildFire anti-malware service allowing for the blocking of malware found on the application.

![runtime-rules-blocking](https://github.com/c-haisten/c2c_summit/assets/98335592/3b0f5dcb-7e1f-4668-bf90-40d41964bf41)

**Feel free to explore the different pages, because this is a lab you will have limited permissions and are not able to edit or create rules.**

For more information about runtime rules and protection from Prisma Cloud check out our public documentation here. (https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/runtime_defense/runtime_defense_containers)



## Summary \ Resources

The Prisma Cloud team here at Palo Alto sincerely hopes you enjoyed this workshop. Today, organizations need a growing set of capabilities to secure modern cloud applications. Implementing AppSec into your development and security workflows with Prisma Cloud can provide the increased speed and agility your organization needs to implement zero trust throughout the entire development lifecycle. Check out the resources below for more information!

[Live Workshops](https://bridgecrew.io/resource/workshops/)

[DevSecTalks Podcast](https://www.paloaltonetworks.com/devsectalks/)

[Supply Chain Security](https://bridgecrew.io/software-supply-chain-security/)

[Cloud DevSecOps](https://bridgecrew.io/cloud-devsecops/)

[Learn More](https://www.paloaltonetworks.com/prisma/cloud)

##### Sample Git Repositories

[TerraGoat - Vulnerable by design Terraform Infrastructure](https://github.com/bridgecrewio/terragoat)

[Cfngoat - Vulnerable by design Cloudformation Template](https://github.com/bridgecrewio/cfngoat)

[CdkGoat - Vulnerable by design AWS CDK Infrastructure](https://github.com/bridgecrewio/cdkgoat)

[BicepGoat - Vulnerable by design Bicep and ARM Infrastructure](https://github.com/bridgecrewio/bicepgoat)

[KubernetesGoat-Vulnerable by design KubernetesCluster](https://github.com/bridgecrewio/kubernetes-goattest)

[KustomizeGoat - Vulnerable by design Kustomize deployment](https://github.com/bridgecrewio/kustomizegoat)

[SupplyGoat- Vulnerable by design SCA](https://github.com/bridgecrewio/supplygoat)

