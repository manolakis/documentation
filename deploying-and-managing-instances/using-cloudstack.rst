Using CloudStack
********************************

You can deploy and manage box configurations on Linux and Windows virtual machines through ElasticBox in your CloudStack environment. ElasticBox supports Linux and Windows compute services for all CloudStack implementations, such as XenServer, VMware, vSphere, KVM, and Xen.

**In this article:**

* `Getting CloudStack Credentials`_
* `Registering CloudStack in ElasticBox`_
* `Bootstrapping CloudStack Templates`_
* `Deploying in CloudStack`_

Getting CloudStack Credentials
---------------------------------------

ElasticBox uses the user API keys to authenticate access to your CloudStack environment. Follow these steps to get the credentials from CloudStack.

**Before You Begin**

You need a CloudStack environment and access to the management console.

**Steps**

1. Log in to your CloudStack management console as a user or administrator.

	.. raw:: html

		<div class="doc-image padding-1x">
	    	<img class="img-responsive" src="/../assets/img/docs/providers/cloudstack-log-in-console.png" alt="Log in as Admin or User to the CloudStack Console">
		</div>

2. Click **Accounts** > <your user account>.

	.. raw:: html

		<div class="doc-image padding-1x">
	    	<img class="img-responsive" src="/../assets/img/docs/providers/cloudstack-selectyouraccount-underaccounts.png" alt="Select Your Account">
		</div>

3. Click **View Users** and select your user account.

	.. raw:: html

		<div class="doc-image padding-1x">
	    	<img class="img-responsive" src="/../assets/img/docs/providers/cloudstack-clickviewusers-credentials.png" alt="Click View Users and Select Your Account">
		</div>

4. If available, copy the existing API and secret keys. Otherwise, click the generate keys icon to create them.

	.. raw:: html

		<div class="doc-image padding-1x">
	    	<img class="img-responsive" src="/../assets/img/docs/providers/cloudstack-copyorgenerateapiandsecretkeys-credentials.png" alt="Get Existing Keys or Generate Them">
		</div>

Registering CloudStack in ElasticBox
--------------------------------------

**Steps**

1. Log in to ElasticBox.
2. Click **Providers** > **New Provider**.
3. Select **CloudStack**.
4. Enter your CloudStack user API credentials.

	.. raw:: html

		<div class="doc-image padding-1x">
    		<img class="img-responsive" src="/../assets/img/docs/providers/cloudstack-enteruserapicredentials-register-elasticbox.png" alt="Enter Your API User Crendentials from the CloudStack Console">
		</div>

	* **URL**. API endpoint to the CloudStack management server that typically has this format, **http://10.0.128.21:8080/client/api**.
	* **API Key**. Part of the user `API credentials </../documentation/deploying-and-managing-instances/using-cloudstack/#getting-cloudstack-credentials>`_ generated for the user account in the CloudStack management console.
	* **Secret Key**. Part of the user `API credentials </../documentation/deploying-and-managing-instances/using-cloudstack/#getting-cloudstack-credentials>`_ generated for the user account in the CloudStack management console.

5. Click **Save**.

Bootstrapping CloudStack Templates
-------------------------------------

In order for ElasticBox to configure, deploy, and manage box configurations in CloudStack, both Linux and Windows templates must be bootstrapped with the ElasticBox init agent script. Follow these steps.

Linux
`````````
**Steps**

1. SSH into the Linux virtual machine template.
2. Run this shell script as the root admin in the terminal.

	.. raw:: html

		<pre>
		curl -L https://elasticbox.com/agent/linux/cloudstack/template_customization_script.sh | sudo bash
		</pre>

Windows
`````````
**Steps**

1. Log in to the Windows virtual machine template using remote desktop protocol (RDP).
2. `Download the script from this URL <http://elasticbox.com/agent/windows/cloudstack/template_customization_script.ps1>`_.
3. Right-click the script file and click Run PowerShell.

**Note**: For information on creating custom templates, see the `Apache CloudStack help <http://docs.cloudstack.apache.org/projects/cloudstack-administration/en/latest/templates.html#exporting-templates>`_.

Deploying in CloudStack
-------------------------------------

When you’re ready to `launch an instance </../documentation/deploying-and-managing-instances/deploying-managing-instances/#new-instance>`_ in CloudStack, you can define Linux or Windows deployment options in a deployment profile. ElasticBox passes the compute offering, disk offering, and template options you provide in the profile as parameters to CloudStack, which then spins up the virtual machine.

**Deployment**

+----------------------------------+------------------------------------------------+
| Option                           | Description                                    |
+==================================+================================================+
| Provider                         | CloudStack account in ElasticBox that you use  |
|                                  | to deploy.                                     |
+----------------------------------+------------------------------------------------+

**Resource**

+----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Option                           | Description                                                                                                                |
+==================================+============================================================================================================================+
| Zone                             | Availability zone or region isolated for data redundancy where you want to deploy the virtual machine. For example, Zone 1.|
+----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Template                         | Pre-configured OS image from which to boot the virtual machine. It can contain the base OS plus additional configuration   |
|                                  | like application files. If you’re deploying a Linux box type, you’ll see Linux templates such as Ubuntu Server 12.04 64-bit|
|                                  | . If you’re deploying a Windows box type, you’ll see Windows templates such as Windows Server 2008 R2 Enterprise.          |
+----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Compute Offering                 | Determines the allotted CPU cores, memory, high availability, and so on for the selected template. The list includes       |
|                                  | predefined offerings as well as those configured by you in CloudStack.                                                     |
+----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Disk Offering                    | Optional data storage in addition to the inherent disk space on the virtual machine. Choose from predefined offerings such |
|                                  | as small, medium, large or choose an offering that you configured in CloudStack.                                           |
+----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Instances                        | Number of instances to provision for a selected box.                                                                       |
+----------------------------------+----------------------------------------------------------------------------------------------------------------------------+ 

**Placement**

+----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
| Option                           | Description                                                                                                                                  |
+==================================+==============================================================================================================================================+
| Network                          | Default guest network configuration or a pre-configured network to allow traffic to the virtual machine. Consists of the permitted CIDR      |
|                                  | block of IP addresses from where traffic to the virtual machine is allowed. For more information, see the                                    |
|                                  | `CloudStack help <http://docs.cloudstack.apache.org/projects/cloudstack-administration/en/4.3/networking_and_traffic.html>`_.                |
+----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
| Security Groups                  | Filter incoming and outgoing traffic for the virtual machine based on a set of rules. Multiple security groups in a zone can be selected     |
|                                  | for a virtual machine. For more information, see                                                                                             |
|                                  | `Security Groups <http://docs.cloudstack.apache.org/projects/cloudstack-administration/en/4.3/networking_and_traffic.html#security-groups>`_.|
+----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+

