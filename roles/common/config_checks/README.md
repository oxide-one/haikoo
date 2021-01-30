# Config Checks

Path:  `roles/common/config_checks`

Performs basic config checks to ensure that variables are configured properly.

There are two 'sub' roles within the `config_checks` role, and these are as follows.

## Kubernetes

**Path:** `kubernetes/tasks/main.yaml`

Ensures that the controlplane endpoint is defined, as there is no suitable default, given the target networks could theoretically be anything.

**Variables used:**

- `kubernetes_control_plane_endpoint_ip`

## oVirt

**Path:** `ovirt/tasks/main.yaml`

Performs a number of checks against the oVirt related variables.

The checks validate the following when they exist:

- Username

- Endpoint

- Password

- Datacentre name

- Cluster name

**Variables used**

- `ovirt_engine_endpoint`

- `ovirt_engine_username`

- `ovirt_engine_password`

- `ovirt_engine_datacenter_name`

- `ovirt_engine_cluster_name`

- `template_name`
