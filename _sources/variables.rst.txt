Runtime Variables
*****************






oVirt
=====




ovirt_auth
----------

An authentication token needed to perform authentication to oVirt.

**Type:** String

**Created In:** ``roles/ovirt/connect``




ovirt_datacentre_exists
-----------------------

A list of datacenters returned by the ``ovirt.ovirt.ovirt_datacenter_info`` module.

Used to to assert that the :ref:`datacenter <defaults:ovirt_engine_datacenter_name>` exists.

**Type:** List

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/dc_cluster/tasks/main.yaml`




ovirt_cluster_exists
--------------------

A list of clusters returned by the ``ovirt.ovirt.ovirt_cluster_info`` module.

Used to to assert that the :ref:`cluster <defaults:ovirt_engine_cluster_name>` exists.

**Type:** List

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/dc_cluster/tasks/main.yaml`




ovirt_temp_vm_network_exists
----------------------------

A list of networks returned by the ``ovirt.ovirt.ovirt_network_info`` module.

Used to to assert that the :ref:`temporary vm network <defaults:temp_vm_network>` exists.

**Type:** List

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/networks/tasks/main.yaml`




ovirt_kubernetes_network_exists
-------------------------------

A list of networks returned by the ``ovirt.ovirt.ovirt_network_info`` module.

Used to to assert that the :ref:`kubernetes network <defaults:kubernetes_cluster_network>` exists.

**Type:** List

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/networks/tasks/main.yaml`




ovirt_template_storage_exists
-----------------------------

A list of storage domains returned by the ``ovirt.ovirt.ovirt_storage_domain_info`` module.

Used to to assert that the :ref:`storage domain <defaults:template_storage_location>` exists.


**Type:** List

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/storage/tasks/main.yaml`





ovirt_template_exists
---------------------

A list of templates returned by the ``ovirt.ovirt.ovirt_template_info`` module.

Used to determine if the template has been made, and if so, how many.

**Type:** List

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/templates/tasks/main.yaml`






Template
========




template_exists
---------------

Boolean value used to determine if the template *exists*.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/templates/tasks/main.yaml`




template_modified
-----------------

Boolean value used to determine if the template has been *modified* to create the base image yet.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/templates/tasks/main.yaml`




template_version_number
-----------------------

The version number of the template that is most recent.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/templates/tasks/main.yaml`






Common
======




ssh_key
-------

Contents of an SSH Public key retrieved either from Github or local filesystem.

**Type:** String

**Role:** :ref:`roles:grab_ssh_key`

**Source:** :role:`common/grab_ssh_key/tasks/main.yaml`






Kubernetes
==========




new_cluster
-----------

Boolean set when there are no control plane nodes detected.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/virtual_machines/tasks/gather_vms.yaml`




certificate_key
---------------

Boolean set when there are no control plane nodes detected.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/virtual_machines/tasks/gather_vms.yaml`





token
-----

Boolean set when there are no control plane nodes detected.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/virtual_machines/tasks/gather_vms.yaml`




kube_config
-----------

Boolean set when there are no control plane nodes detected.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/virtual_machines/tasks/gather_vms.yaml`




kubeadm_init
------------

Boolean set when there are no control plane nodes detected.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/virtual_machines/tasks/gather_vms.yaml`




endpoint
--------

Boolean set when there are no control plane nodes detected.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/virtual_machines/tasks/gather_vms.yaml`




node_ready
----------

Boolean set when there are no control plane nodes detected.

**Type:** Boolean

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`common/gather_env_info/virtual_machines/tasks/gather_vms.yaml`





Control Plane Nodes
===================




kubernetes_control_plane_nodes_list
-----------------------------------

List of control plane nodes that match the pattern of:
:ref:`kubernetes_cluster_name<defaults:kubernetes_cluster_name>`-:ref:`kubernetes_control_plane_node_name<defaults:kubernetes_control_plane_node_name>`-*

**Type:** List

**Role:** :ref:`roles:gather_env_info`

**Source:** :role:`gather_env_info/virtual_machines/tasks/gather_vms.yaml`




kubernetes_control_plane_count_difference
-----------------------------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




increase_control_plane_nodes
----------------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




decrease_control_plane_nodes
----------------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




maintain_control_plane_nodes
----------------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




kubernetes_control_plane_node_modify_count
------------------------------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Type:** String

**Role:** :ref:`roles:grab_ssh_key`

**Source:** :role:`common/grab_ssh_key/tasks/main.yaml`






Worker nodes
============




kubernetes_worker_nodes_list
----------------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




kubernetes_worker_node_count_difference
---------------------------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




kubernetes_worker_node_modify_count
-----------------------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




increase_worker_nodes
---------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




decrease_worker_nodes
---------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``




maintain_worker_nodes
---------------------

The username to perform all oVirt operations with.

Must contain an ``@`` (usually ``@local``)

**Default:** ``admin@internal``

**Optional:** Yes

**Type:** String

**Created In:** ``roles/common/``
