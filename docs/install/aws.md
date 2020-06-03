# Running PMM Server Using AWS Marketplace

You can run an instance of {{ pmm_server }} hosted at AWS Marketplace. This
method replaces the outdated method where you would have to accessing
an AMI (Amazon Machine Image) by using its ID, different for each region.

Assuming that you have an AWS (Amazon Web Services) account, locate
*Percona Monitoring and Management Server* in [AWS Marketplace](https://aws.amazon.com/marketplace/pp/B077J7FYGX).

The {{ gui_pricing_information }} section allows to select your region and choose an
instance type in the table that shows the pricing for the software and
infrastructure hosted in the region you have selected (the recommended
EC2 instance type is preselected for you). Note that actual choice will be done
later, and this table serves the information purposes, to plan costs.

!!! note
    Disk space consumed by {{ pmm_server }} depends on the number of hosts under monitoring. Each environment will be unique, however consider modeling your data consumption based on [PMM Demo](https://pmmdemo.percona.com/) web site, which consumes ~230MB/host/day, or ~6.9GB/host at the default 30 day retention period. See [this blog post](https://www.percona.com/blog/2017/05/04/how-much-disk-space-should-i-allocate-for-percona-monitoring-and-management/) for more details.


* Clicking the {{ gui_continue_to_subscribe }} button will proceed to the terms and
conditions page.


* Clicking {{ gui_continue_to_configuration }} there will bring a new page to start
setting up your instance. You will be able to re-check the PMM Server version
and the region. When done, continue to the launch options by clicking
{{ gui_continue_to_launch }}.

Select the previously chosen instance type from the *EC2 Instance Type*
drop-down menu. Also chose the launch option. Available launch options in the
*Chose Action* drop-down menu include *Launch from Website* and
*Launch through EC2*. The first one is a quick way to make your instance ready.
For more control, use the Manual Launch through EC2 option.

## [Setting Up a PMM Instance Using the website GUI](aws.md#run-server-aws-pmm-instance-1-click-launch-option-setting-up)

Choose *Launch from Website* option, your region, and the EC2 instance type on
the launch options page. On the previous screenshot, we use the
`US East (N. Virginia)` region and the EC2 Instance Type named
`t2.medium`. To reduce cost, you need to choose the region closest to
your location.

### [Setting up a VPC and an EC2 Instance Type](aws.md#run-server-aws-pmm-instance-1-click-launch-option-vpc-ec2-instance-type)

> In this demonstration, we use the VPC (virtual private cloud) named `vpc-484bb12f`. The exact name of VPC may be different from the example discussed here.

Instead of a VPC (virtual private cloud) you may choose the `EC2 Classic
(no VPC)` option and use a public cloud.

Selecting a subnet, you effectively choose an availability zone in the selected
region. We recommend that you choose the availability zone where your RDS is
located.

Note that the cost estimation is automatically updated based on your choice.

### [Limiting Access to the instance: security group and a key pair](aws.md#run-server-aws-security-group-key-pair)

In the {{ gui_security_group }} section, which acts like a firewall, you may use the
preselected option `Create new based on seller settings` to create a
security group with recommended settings. In the Key Pair select an
already set up EC2 key pair to limit access to your instance.

### [Applying settings](aws.md#run-server-aws-setting-applying)

Scroll up to the top of the page to view your settings. Then, click the
Launch with 1 click button to continue and adjust your settings in
the **EC2 console**.

!!! note
    The Launch with 1 click button may alternatively be titled as Accept Software Terms & Launch with 1-Click.

### [Adjusting instance settings in the EC2 Console](aws.md#pmm-aws-instance-setting-ec2-console-adjusting)

Your clicking the Launch with 1 click button, deploys your
instance. To continue setting up your instance, run the **EC2
console**. It is available as a link at the top of the page that opens after you
click the Launch with 1 click button.

Your instance appears in the **EC2 console** in a table that lists all
instances available to you. When a new instance is only created, it has no
name. Make sure that you give it a name to distinguish from other instances
managed via the **EC2 console**.

### [Running the instance](aws.md#pmm-server-aws-running-instance)

After you add your new instance it will take some time to initialize it. When
the AWS console reports that the instance is now in a running state, you many
continue with configuration of {{ pmm_server }}.

!!! note
    When started the next time after rebooting, your instance may acquire another IP address. You may choose to set up an elastic IP to avoid this problem.

With your instance selected, open its IP address in a web browser. The IP
address appears in the IPv4 Public IP column or as value of the
Public IP field at the top of the Properties panel.

To run the instance, copy and paste its public IP address to the location bar of
your browser. In the {{ pmm_name }} welcome page that opens, enter the instance ID.

You can copy the instance ID from the Properties panel of your
instance, select the Description tab back in the **EC2
console**. Click the Copy button next to the Instance
ID field. This button appears as soon as you hover the cursor of your mouse
over the ID.

Paste the instance in the Instance ID field of the {{ pmm_name }}
welcome page and click {{ gui_submit }}.

{{ pmm_server }} provides user access control, and therefore you will need user
credentials to access it:

The default user name is `admin`, and the default password is `admin` also.
You will be proposed to change the default password at login if you didn’t it.

The {{ pmm_server }} is now ready and the home page opens.

You are creating a username and password that will be used for two purposes:


1. authentication as a user to PMM - this will be the credentials you need in order
to log in to PMM.


2. authentication between PMM Server and PMM Clients - you will
re-use these credentials when configuring pmm-client for the first time on a
server, for example:

{{ tip_run_this_root }}

```
pmm-admin config --server-insecure-tls --server-url=https://admin:admin@<IP Address>:443
```

!!! note
    **Accessing the instance by using an SSH client.**

For instructions about how to access your instances by using an SSH client, see
[Connecting to Your Linux Instance Using SSH](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)

Make sure to replace the user name `ec2-user` used in this document with
`admin`.


* Resizing the EBS Volume


* \`Upgrading PMM Server on AWS
