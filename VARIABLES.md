# oVirt

## ovirt_engine_username

The username to perform all oVirt operations with.

Must contain an `@` (usually `@local`)

**Default:** `admin@internal`

**Optional:** Yes

**Type:** String

## ovirt_engine_password

The password to connect to oVirt with.

**Default:** `NONE`

**Optional:** No

**Type:** String

## ovirt_engine_endpoint

The endpoint of your oVirt engine. Must end with `/ovirt-engine`.

**Default:** `NONE`

**Optional:** No

**Type:** String

## ovirt_engine_datacenter_name

The datacenter name you want to deploy Haikoo into.

**Default:** `Default`

**Optional:** Yes

**Type:** String

## ovirt_engine_cluster_name

The Cluster name you want to deploy Haikoo into.

**Default:** `Default`

**Optional:** Yes

**Type:** String

---

# Template

## template_name

The name of the template to be created.

Defaults to the cluster name.

**Default:** `{{ kubernetes_cluster_name }}`

**Optional:** Yes

**Type:** String

## template_imported_image_name

The name of the image to import from the ovirt-image-repository storage domain.

Currently Haikoo supports Fedora based systems only.

**Default:** `Fedora 33 Cloud Base Image v1.2 for x86_64`

**Optional:** Yes

**Type:** String

## template_storage_location

The Storage domain to import and save the Template(s) to.

**Default:** `data`

**Optional:** Yes

**Type:** String

## template_import_timeout

The time, in seconds to wait for the import to run.

Increase this if your import fails.

**Default:** `600`

**Optional:** Yes

**Type:** Integer

## template_description

The description to give to the imported template.

**Default:** `Created by haikoo`

**Optional:** *Yes*

**Type:** String

## template_extra_repos

A list of extra repos to package into the template.

**Default:** `Created by haikoo`

**Optional:** *Yes*

**Type:** List

## template_upgrade_packages

A boolean to determine whether to upgrade all the packages on the template before packaging into the base image. Disable if template takes too long.

**Default:** `True`

**Optional:** *Yes*

**Type:** Boolean

## template_timezone

The timezone of the template.

**Default:** `Etc/GMT`

**Optional:** *Yes*

**Type:** String

## template_extra_packages

A list of extra packages to install into the base image.

**Default:** `NONE`

**Optional:** *Yes*

**Type:** List

## template_extra_services

A list of extra services to enable on boot.

**Default:** `NONE`

**Optional:** *Yes*

**Type:** List

## template_selinux_enabled

Boolean to determine whether to enable SELinux.

Please do not enable this until further testing is done :)

**Default:** `False`

**Optional:** *Yes*

**Type:** Boolean

## template_subversion_name

The subversion name to give to the template after modifications have been made.

**Default:** `post-modification`

**Optional:** *Yes*

**Type:** String

---

# Temporary virtual machine

## temp_vm_name

The name of the temporary virtual machine to create.

**Default:** `haikoo-temp-vm`

**Optional:** *Yes*

**Type:** String

## temp_vm_network

The network to assign the temporary virtual machine to

**Default:** `ovirtmgmt`

**Optional:** *Yes*

**Type:** String

## temp_vm_cores

The number of cores to give the temporary virtual machine.

Change this value if you do not have enough cores on a single hypervisor.

**Default:** `6`

**Optional:** *Yes*

**Type:** Integer

## temp_vm_memory

The amount (in MB) to give the temporary virtual machine.

**Default:** `3072`

**Optional:** *Yes*

**Type:** Integer

---

# Kubernetes

## kubernetes_login_username

The username to provision as the administrator within the template, and the cluster.

**Default:** `kubeadmin`

**Optional:** *Yes*

**Type:** String

## crio_version

The version of cri-o to enable within the cluster.

**Default:** `1.18`

**Optional:** *Yes*

**Type:** String

## kubernetes_cluster_name

The name of the cluster to deploy.

**Default:** `haikoo`

**Optional:** *Yes*

**Type:** String

## domain

The domain to append onto the end of all node names.

**Default:** `NONE`

**Optional:** *Yes*

**Type:** String

## kubernetes_control_plane_endpoint_ip

The endpoint IP that the control plane nodes will share over VRRP.

**Default:** `NONE`

**Optional:** *No*

**Type:** String

## kubernetes_control_plane_endpoint_dns

A DNS endpoint that the cluster will be available at.

**Default:** `NONE`

**Optional:** *Yes*

**Type:** String

## kubernetes_cluster_network

The network to deploy the kubernetes cluster into.

**Default:** `ovirtmgmt`

**Optional:** *Yes*

**Type:** String

## startup_timeout

The timeout, in minutes to wait for all the virtual machines to power on.

**Default:** `60`

**Optional:** *Yes*

**Type:** Integer

---

# Control Plane Nodes

## kubernetes_control_plane_node_name

The naming sheme for control plane nodes.

Done in case you want your nodes to be named something other than `control-plane`

**Default:** `control-plane`

**Optional:** *Yes*

**Type:** String

## kubernetes_control_plane_node_count

The number of control plane nodes to _result_ in.

If the number deployed is different, the playbooks will ensure the end result is equal to this amount.

**Default:** `3`

**Optional:** *Yes*

**Type:** Integer

## kubernetes_control_plane_node_cores

The number of cores to give to each control plane node.

**Default:** `4`

**Optional:** *Yes*

**Type:** Integer

## kubernetes_control_plane_node_memory

The amount (in MB) to give each control plane node

**Default:** `4096`

**Optional:** *Yes*

**Type:** Integer

## kubernetes_control_plane_node_disk_size

The size (in GB) to give to each control plane node.

**Default:** `30`

**Optional:** *Yes*

**Type:** Integer

## kubernetes_control_plane_node_roles

A list of roles to assign to each new control plane node.

**Default:** `NONE`

**Optional:** *Yes*

**Type:** List

---

# Worker nodes

## kubernetes_worker_node_name

The naming sheme for worker nodes.

Done in case you want your nodes to be named something other than `worker`.

Please don't name it the same as your control plane nodes.

**Default:** `worker`

**Optional:** *Yes*

**Type:** String

## kubernetes_worker_node_count

The number of worker nodes to *result* in.

If the number deployed is different, the playbooks will ensure the end result is equal to this amount.

**Default:** `3`

**Optional:** *Yes*

**Type:** Integer

## kubernetes_worker_node_cpu_cores

The number of cores to give to each worker node.

**Default:** `4`

**Optional:** *Yes*

**Type:** Integer

## kubernetes_worker_node_memory

The amount (in MB) to give each worker node

**Default:** `4096`

**Optional:** *Yes*

**Type:** Integer

## kubernetes_worker_node_disk_size

The size (in GB) to give to each worker node.

**Default:** `30`

**Optional:** *Yes*

**Type:** Integer

## kubernetes_worker_node_roles

A list of roles to assign to each new worker node.

**Default:** `NONE`

**Optional:** *Yes*

**Type:** List
