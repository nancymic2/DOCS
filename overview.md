# HPE Helion OpenStack 2.1 and HPE Helion OpenStack 2.0
## Overview
### Applies to HPE Helion OpenStack® 2.1 and HPE Helion OpenStack® 2.0.
HPE Helion OpenStack 2.1 is the latest OpenStack-based infrastructure-as-a-service cloud platform release from HP. It is based on the OpenStack Kilo release and implements core services and features of Kilo while providing new installation and management features.
Installation, Configuration, and Management.

With the release of HPE Helion OpenStack 2.1 comes an easy installation and configuration workflow. Installation of the basic cloud requires that you run a handful of commands, or use the new installation GUI to step through installation in a wizard-like fashion.
OpenStack services are installed during the installation process, so there is no need to install and configure them individually.

Instead, in HPE Helion OpenStack 2.1, configuration, including which services to install, how many nodes you will have, what their
individual roles will be, what storage will be used, which networks will handle which traffic, and installation and configuration
of the underlying operating system on each node is declared in configuration objects stored in YAML files.
These files allow customization, and HPE Helion OpenStack 2.1 ships with complete sets describing a few common configurations. 

You may base your deployment on one of these templates and customize from there if you wish.
This installation and configuration is made possible by a new feature in HPE Helion OpenStack 2.1, the configuration processor,
a set of Python scripts that consume the data stored in the configuration YAML files and output Ansible variables used to 
configure networks, services, servers, and the other applications upon which the cloud runs.

As you will read in the HPE Helion OpenStack 2.1 Input Model topic, the Configuration Processor reads and validates the input
model described in the YAML files discussed above, combines it with the service definitions provided by HPE Helion OpenStack
and any persisted state information about the current deployment to produce a set of Ansible variables that can be used to deploy
the cloud. It also produces a set of information files that provide details about the configuration. Reading this document you will
gain a thorough understanding of how HPE Helion OpenStack 2.1 allows you to deploy and manage your cloud via this comprehensive "wrapper" around cloud configuration.

The example configurations that ship with HPE Helion OpenStack 2.1 are described in HPE Helion OpenStack 2.1: 

Example Configurations:
* Entry-scale KVM with VSA model
* Entry-scale ESX model
* Entry-scale Swift model
* Entry-scale KVM with Ceph model
* Mid-scale KVM with VSA model
* Post-deployment Reconfiguration and Management

In addition to initial installation and deployment, the addition of the Configuration Processor means that you can reconfigure your
cloud easily after deployment. Note that due to its combination of deployment and lifecycle-management features, we may use the terms
deployer and lifecycle manager interchangeably throughout the HPE Helion OpenStack 2.1documentation to refer to the features described
in this document.

By executing pre-written, supplied Ansible playbooks in the form of a single command, you may perform management tasks such as those
below, along with many others.

* start, stop, and get the status of OpenStack services
* add and remove controller, compute, and storage nodes
* back up or restore control plane nodes
* migrate Cinder volumes
* get Ceph status
* start and stop logging
* erase nodes to baremetal
* re-image nodes
* reconfigure Swift to add or replace drives
* validate Swift drives against the storage model declared

While the internal management of OpenStack services and the configuration of their functionality still occurs 
via the service APIs and follows the methodology outlined by OpenStack, the high-level management of the services 
themselves and their interaction with the cloud is accomplished via the Ansible playbooks mentioned here.

## Configuration Versioning
In HPE Helion OpenStack 2.1, the YAML files that define your cloud configuration are stored in a local git repository
that is installed along with the cloud. The cloud deployment Ansible playbooks look in the appropriate git directories
and execute changes when run. This allows you to keep an historical record of configuration changes as well as help you 
identify issues that arise later.

_The OpenStack® Word Mark and OpenStack Logo are either registered trademarks/service marks or trademarks/service marks
of the OpenStack Foundation in the United States and other countries and are used with the OpenStack Foundation's permission.
We are not affiliated with, endorsed or sponsored by the OpenStack Foundation or the OpenStack community._

_Cloud Foundry is a trademark and/or registered trademark of CloudFoundry.org Foundation in the United States and/or other countries.
© Copyright 2016 Hewlett Packard Enterprise Development LP
Terms of Use and Privacy Policy_
