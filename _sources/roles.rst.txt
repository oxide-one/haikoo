Role Documentation
##################

common
******

These roles are called common for no other reason than because I can't think of a better name.
Refactoring is also a pain :)






config_checks
=============

**Source:** :role:`common/config_checks`

Performs basic config checks to ensure that variables are configured
properly.

There are two ‘sub’ roles within the ``config_checks`` role, and these
are as follows.




kubernetes.
-----------

Ensures that the controlplane endpoint is defined, as there is no
suitable default, given the target networks could theoretically be
anything.

**Variables used:**

-  :ref:`defaults:kubernetes_control_plane_endpoint_ip`




ovirt.
------

Performs a number of checks against the oVirt related variables.

The checks validate the following when they exist:

-  Username

-  Endpoint

-  Password

-  Datacentre name

-  Cluster name

**Variables used**

-  :ref:`defaults:ovirt_engine_username`

-  :ref:`defaults:ovirt_engine_username`

-  :ref:`defaults:ovirt_engine_password`

-  :ref:`defaults:ovirt_engine_datacenter_name`

-  :ref:`defaults:ovirt_engine_cluster_name`

-  :ref:`defaults:template_name`






gather_env_info
===============

**Source:** :role:`common/gather_env_info`

Performs a number of calls to gather environment information. Determines
what state haikoo is in for use later. This role contains a number of
sub-roles.




Datacentre/Cluster
------------------

**Source:** :role:`common/gather_env_info/dc_cluster/tasks/main.yaml`

Validates that the datacentre defined in
``ovirt_engine_datacenter_name`` exists within oVirt, as well as the
cluster defined in ``ovirt_engine_cluster_name``.

Fails the playbook if either do not exist.

**Variables used:**

-  :ref:`variables:ovirt_auth`

-  :ref:`defaults:ovirt_engine_datacenter_name`

-  :ref:`defaults:ovirt_engine_cluster_name`

**Variables created:**

-  :ref:`variables:ovirt_datacentre_exists`

-  :ref:`variables:ovirt_cluster_exists`




Networks
--------

**Source:** :role:`common/gather_env_info/networks/tasks/main.yaml`

Validates that the networks defined in ``temp_vm_network`` and
``kubernetes_cluster_network`` exist in the datacentre.

Fails the playbook if any do not exist.

**Variables used:**

-  :ref:`variables:ovirt_auth`

-  :ref:`defaults:temp_vm_network`

-  :ref:`defaults:ovirt_engine_datacenter_name`

-  :ref:`defaults:kubernetes_cluster_network`

**Variables created:**

-  :ref:`variables:ovirt_temp_vm_network_exists`

-  :ref:`variables:ovirt_kubernetes_network_exists`




Storage
-------

**Source:** :role:`common/gather_env_info/storage/tasks/main.yaml`

Checks to see if the storage domain defined in
``template_storage_location`` exists within the oVirt cluster. Fails if
it does not exist.

**Variables used:**

-  :ref:`variables:ovirt_auth`

-  :ref:`defaults:template_storage_location`

-  :ref:`defaults:ovirt_engine_datacenter_name`

-  :ref:`defaults:ovirt_engine_cluster_name`

**Variables created:**

-  :ref:`variables:ovirt_template_storage_exists`




Templates
---------

**Source:** :role:`common/gather_env_info/templates/tasks/main.yaml`

Checks to see whether the base image exists within oVirt as a template.
Also checks to see how many subversions exist. If only one, we can
assume that the template has *not* been modified for use within haikoo.

**Variables used:**

-  :ref:`variables:ovirt_auth`

-  :ref:`defaults:template_name`

-  :ref:`defaults:ovirt_engine_datacenter_name`

-  :ref:`defaults:ovirt_engine_cluster_name`

**Variables created:**

-  :ref:`variables:ovirt_template_exists`

-  :ref:`variables:template_exists`

-  :ref:`variables:template_modified`

-  :ref:`variables:template_version_number`




Virtual Machines
----------------

**Source:** :role:`common/gather_env_info/virtual_machines`

Gathers information about the virtual machines in the cluster. Adds all
existing hosts to the inventory and schedules nodes to be created or
deleted. Ultimately this sub-role is what controls whether to create a
new cluster, to expand/shrink an existing one.

**Variables Used:**

**Common**

-  :ref:`defaults:domain`

-  :ref:`variables:ssh_key`

**oVirt**

-  :ref:`variables:ovirt_auth`

-  :ref:`defaults:ovirt_engine_datacenter_name`

-  :ref:`defaults:ovirt_engine_cluster_name`

**Kubernetes**

-  :ref:`defaults:kubernetes_cluster_name`

-  :ref:`defaults:kubernetes_control_plane_node_name`

-  :ref:`defaults:kubernetes_worker_node_name`

-  :ref:`defaults:kubernetes_control_plane_node_count`

-  :ref:`defaults:kubernetes_worker_node_count`

-  :ref:`defaults:kubernetes_control_plane_node_name`

-  :ref:`defaults:kubernetes_control_plane_node_cores`

-  :ref:`defaults:kubernetes_control_plane_node_memory`

-  :ref:`defaults:kubernetes_control_plane_node_disk_size`

-  :ref:`defaults:kubernetes_control_plane_node_roles`

-  :ref:`defaults:kubernetes_worker_node_cpu_cores`

-  :ref:`defaults:kubernetes_worker_node_memory`

-  :ref:`defaults:kubernetes_worker_node_disk_size`

-  :ref:`defaults:kubernetes_worker_node_roles`

**Variables Set:**

**Control Plane**

-  :ref:`variables:kubernetes_control_plane_node_modify_count`

-  :ref:`variables:kubernetes_control_plane_nodes_list`

-  :ref:`variables:kubernetes_control_plane_count_difference`

-  :ref:`variables:increase_control_plane_nodes`

-  :ref:`variables:decrease_control_plane_nodes`

-  :ref:`variables:maintain_control_plane_nodes`

**Worker Node**

-  :ref:`variables:kubernetes_worker_nodes_list`

-  :ref:`variables:kubernetes_worker_node_count_difference`

-  :ref:`variables:kubernetes_worker_node_modify_count`

-  :ref:`variables:increase_worker_nodes`

-  :ref:`variables:decrease_worker_nodes`

-  :ref:`variables:maintain_worker_nodes`

-  :ref:`variables:new_cluster`






grab_ssh_key
============

**Source:** :role:`common/grab_ssh_key`

Grabs the SSH key, either from Github or from the local disk and sets the public key as the `ssh_key` variable.

**Variables used:**

-  :ref:`defaults:ssh_key_github`

-  :ref:`defaults:ssh_key_path`


**Variables created:**

- :ref:`variables:ssh_key`





set_defaults
============

**Source:** :role:`common/set_defaults`

Performs basic config checks to ensure that variables are configured
properly.

There are two ‘sub’ roles within the ``config_checks`` role, and these
are as follows.







kubernetes
**********
These roles heavily involve kubernetes, and the setup around them.





init_cluster
============

**Source:** :role:`kubernetes/init_cluster`

Initializes a kubernetes cluster in multiple stages.

The stages are as follows:

1. Create certificate key and save as :ref:`variables:certificate_key`
2. Create a join token and save as :ref:`variables:token`
3. Read the contents of the certificate key and join token into their respective vars.
4. Set the :ref:`variables:kube_config` variable to ``/etc/kubernetes/{{ kubernetes_cluster_name }}-cluster.conf``
5. Determine whether to use the :ref:`DNS Endpoint <defaults:kubernetes_control_plane_endpoint_dns>` or the :ref:`IP Endpoint <defaults:kubernetes_control_plane_endpoint_ip>`
6. Template out the Kubernetes cluster config
7. Pull all the Kubernetes images
8. Run pre-flight Kubernetes checks
9. Generate Certificates and save to :ref:`variables:kubeadm_init`
10. Generate ``/etc/kubernetes/admin.conf`` file.
11. Write out the kubelet settings to ``/var/lib/kubelet/config.yaml`` and restart the kubelet
12. Generate the static pod manifests and save to ``/etc/kubernetes/manifests/``
13. Upload the kubelet configuration to a configmap.
14. Upload the certificates to kubeadm-certs.
15. Mark the node as a control plane
16. Generate the bootstrap tokens needed to join other nodes to the cluster
17. Enable client certificate rotation
18. Install all the addons (CoreDNS, kube-proxy)
19. Loop until the API is ready.


**Variables created:**

- :ref:`variables:certificate_key`
- :ref:`variables:token`
- :ref:`variables:kube_config`
- :ref:`variables:endpoint`
- :ref:`variables:node_ready`




control_plane_setup
===================

**Source:** :role:`kubernetes/control_plane_setup`

The necessary tasks required for setting a node up for use as a control plane.

**Variables used:**

-  :ref:`defaults:ssh_key_github`

-  :ref:`defaults:ssh_key_path`


**Variables created:**

- :ref:`variables:ssh_key`




prepare_node
============

**Source:** :role:`kubernetes/control_plane_setup`

Role to handle setting up a node for use as a kubernetes node.

**Variables used:**

-  :ref:`defaults:ssh_key_github`

-  :ref:`defaults:ssh_key_path`


**Variables created:**

- :ref:`variables:ssh_key`





ovirt
*****






connect
=======





resize_disk
===========





template
========





virtual_machine
===============





wait_for_ip
===========
