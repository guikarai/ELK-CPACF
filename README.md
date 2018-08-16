# Protect data on LinuxONE with "Pervasive Encryption" and Monitor Hardware Cryptographic Activities with ELK
Protect your data on data LinuxONE using pervasive encryption with nearly no CPU overhead.

In this Code Pattern, you will build and deploy a crypto dashboard in a LinuxONE guest running in the LinuxONE Community Cloud.

The LinuxONE Community Cloud provides an open access to Linux running on a mainframe, primarily targeted at development, porting and functional testing. Registered users can deploy recent SLES and RHEL instances.. It is an integrated environment that enables you to design, develop, deploy and manage on-premises, containerized cloud applications behind a firewall.

When you will complete this Code Pattern, you will understand how to:
* Configure a LinuxONE Linux guest to use the hardware cryptographic acceleration.
* Use the LinuxONE crypto APIS to get monitoring data about hardware cryptographic use.
* Deploy Docker images in your LinuxONE Linux guest to create an ELK stack.
* Build an ELK Dashboard to monitor hardware cryptographic activity of LinuxONE Linux guest.

# Architecture
This journey stats with a LinuxONE Linux guest which after some optimization will be able to claim hardware cryptographic assistance. From there, captured encryption activities to be magnified thanks to a docker based ELK dashboard.

![Image of the Crypto Stack](https://github.com/guikarai/ELK-CPACF/blob/master/images/code-pattern-architecture.png)

1. User optimizes, collects and captures Enterprise Legacy environment encryption activity.
3. User deploys a docker based ELK stack running on LinuxONE Community Cloud.
3. User creates and then enjoys a crypto activity dashboard running on LinuxONE Community Cloud.

# Included components

* [LinuxONE Crypto](https://www.ibm.com/it-infrastructure/linuxone/capabilities/secure-cloud)
* [OpenSSL](https://www.openssl.org/)
* [Curl](https://curl.haxx.se/)

# Featured technologies

* [Docker](https://www.docker.com/)
* [IBM LinuxONE](https://www.ibm.com/it-infrastructure/linuxone)
* [ELK](https://www.elastic.co/fr/elk-stack)

# Steps

## Step 1 - [Enabling Linux to use hardware encryption](https://github.com/guikarai/ELK-CPACF/blob/master/part1.md)

    1. Introduction to the pervasive encryption
    2. Introduction to the Linux crypto stack
    2. Enabling Linux to use the Hardware
    3. Enabling OpenSSL to use the hardware acceleration support
    4. Checking Hardware Crypto functions

## Step 2 - [Deploying a docker based ELK stack running on LinuxONE Community Cloud.](https://github.com/guikarai/ELK-CPACF/blob/master/part2.md)
    
    1. What the ELK..?!
    2. What to keep in mind about ELK?
    3. Cloning the ELK-CPACF github repository
    4. Deploying an ELK Docker based stack
    5. Tooling for Elasticsearch
    6. Seting-up local linux and crypto data collection

## Step 3 - [Creating a crypto activity dashboard running on LinuxONE Community Cloud.](https://github.com/guikarai/ELK-CPACF/blob/master/part3.md)

    1. Accessing to Kibana
    2. Sourcing the ElasticSearch DataSource
    3. Creating your first search with Kibana
    4. Creating your first charts with Kibana
    5. Creating your first dashboard with Kibana
    6. Sharing your first crypto dashboard
  
