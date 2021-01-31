Common Role Documentation
*************************

Config Checks
=============

Path: ``roles/common/config_checks``

Performs basic config checks to ensure that variables are configured
properly.

There are two ‘sub’ roles within the ``config_checks`` role, and these
are as follows.

Kubernetes
----------

**Path:** ``kubernetes/tasks/main.yaml``

Ensures that the controlplane endpoint is defined, as there is no
suitable default, given the target networks could theoretically be
anything.

**Variables used:**

-  ``kubernetes_control_plane_endpoint_ip``

oVirt
-----

**Path:** ``ovirt/tasks/main.yaml``

Performs a number of checks against the oVirt related variables.

The checks validate the following when they exist:

-  Username

-  Endpoint

-  Password

-  Datacentre name

-  Cluster name

**Variables used**

-  ``ovirt_engine_endpoint``

-  ``ovirt_engine_username``

-  ``ovirt_engine_password``

-  ``ovirt_engine_datacenter_name``

-  ``ovirt_engine_cluster_name``

-  ``template_name``


Gather Environment Info
=======================

Path: ``roles/common/gather_env_info``

Performs a number of calls to gather environment information. Determines
what state haikoo is in for use later. This role contains a number of
sub-roles.

Datacentre/Cluster
------------------

Path: ``dc_cluster/``

Validates that the datacentre defined in
``ovirt_engine_datacenter_name`` exists within oVirt, as well as the
cluster defined in ``ovirt_engine_cluster_name``.

Fails the playbook if either do not exist.

**Variables used:**

-  ``ovirt_auth``

-  ``ovirt_engine_datacenter_name``

-  ``ovirt_engine_cluster_name``

**Variables created:**

-  ``ovirt_datacentre_exists``

-  ``ovirt_cluster_exists``

Networks
--------

Path: ``networks/``

Validates that the networks defined in ``temp_vm_network`` and
``kubernetes_cluster_network`` exist in the datacentre.

Fails the playbook if any do not exist.

**Variables used:**

-  ``ovirt_auth``

-  ``temp_vm_network``

-  ``ovirt_engine_datacenter_name``

-  ``kubernetes_cluster_network``

**Variables created:**

-  ``ovirt_temp_vm_network_exists``

-  ``ovirt_kubernetes_network_exists``

Storage
-------

Path: ``storage/``

Checks to see if the storage domain defined in
``template_storage_location`` exists within the oVirt cluster. Fails if
it does not exist.

**Variables used:**

-  ``ovirt_auth``

-  ``template_storage_location``

-  ``ovirt_engine_datacenter_name``

-  ``ovirt_engine_cluster_name``

**Variables created:**

-  ``ovirt_template_storage_exists``

Templates
---------

Path: ``templates/``

Checks to see whether the base image exists within oVirt as a template.
Also checks to see how many subversions exist. If only one, we can
assume that the template has *not* been modified for use within haikoo.

**Variables used:**

-  ``ovirt_auth``

-  ``template_name``

-  ``ovirt_engine_datacenter_name``

-  ``ovirt_engine_cluster_name``

**Variables created:**

``ovirt_template_exists``

``template_exists``

``template_modified``

``template_version_number``

Virtual Machines
----------------

Path: ``virtual_machines``

Gathers information about the virtual machines in the cluster. Adds all
existing hosts to the inventory and schedules nodes to be created or
deleted. Ultimately this sub-role is what controls whether to create a
new cluster, to expand/shrink an existing one.

**Variables Used:**

**Common**

-  ``domain``

-  ``ssh_key``

**oVirt**

-  ``ovirt_auth``

-  ``ovirt_engine_datacenter_name``

-  ``ovirt_engine_cluster_name``

**Kubernetes**

-  ``kubernetes_cluster_name``

-  ``kubernetes_control_plane_node_name``

-  ``kubernetes_worker_node_name``

-  ``kubernetes_control_plane_node_count``

-  ``kubernetes_worker_node_count``

-  ``kubernetes_control_plane_node_name``

-  ``kubernetes_control_plane_node_cores``

-  ``kubernetes_control_plane_node_memory``

-  ``kubernetes_control_plane_node_disk_size``

-  ``kubernetes_control_plane_node_roles``

-  ``kubernetes_worker_node_cpu_cores``

-  ``kubernetes_worker_node_memory``

-  ``kubernetes_worker_node_disk_size``

-  ``kubernetes_worker_node_roles``

**Variables Set:**

**Control Plane**

-  ``kubernetes_control_plane_node_modify_count``

-  ``kubernetes_control_plane_nodes_list``

-  ``kubernetes_control_plane_count_difference``

-  ``increase_control_plane_nodes``

-  ``decrease_control_plane_nodes``

-  ``maintain_control_plane_nodes``

**Worker Node**

-  ``kubernetes_worker_nodes_list``

-  ``kubernetes_worker_node_count_difference``

-  ``kubernetes_worker_node_modify_count``

-  ``increase_worker_nodes``

-  ``decrease_worker_nodes``

-  ``maintain_worker_nodes``

-  ``new_cluster``
