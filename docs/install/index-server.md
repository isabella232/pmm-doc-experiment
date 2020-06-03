# Installing PMM Server


* Running {{ pmm_server }} via {{ docker }}


    * Setting Up a {{ docker }} Container for {{ pmm_server }}


        * Pulling the PMM Server Docker Image


        * Creating the pmm-data Container


        * Creating and Launching the PMM Server Container


        * Installing and using specific PMM Server version


    * Updating {{ pmm_server }} Using {{ docker }}


        * Creating a backup version of the current pmm-server Docker container


        * Pulling a new Docker Image


        * Creating a new Docker container based on the new image


        * Removing the backup container


    * Backing Up {{ pmm }} Data from the {{ docker }} Container


    * Restoring the Backed Up Information to the PMM Data Container


* Running PMM Server Using AWS Marketplace


    * Setting Up a PMM Instance Using the website GUI


        * Setting up a VPC and an EC2 Instance Type


        * Limiting Access to the instance: security group and a key pair


        * Applying settings


        * Adjusting instance settings in the EC2 Console


        * Running the instance


            * Resizing the EBS Volume


            * \`Upgrading PMM Server on AWS


* PMM Server as a Virtual Appliance


    * Supported Platforms for Running the PMM Server Virtual Appliance


    * Identifying PMM Server IP Address


    * Accessing PMM Server


    * Accessing the Virtual Machine


    * Next Steps


* Verifying PMM Server


* Configuring PMM Server


    * PMM Settings Page


        * Settings


        * Metrics resolution


        * Telemetry


        * Check for updates


        * Security Threat Tool


        * SSH Key Details


        * Prometheus Alertmanager integration


        * Diagnostics


    * Exploring PMM API
