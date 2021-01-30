# Variables

## oVirt

oVirt related variables.

### ovirt_engine_username

    **Optional:** *Yes*

    **Default:** `admin@internal`

    **Type:** String

    The username to perform all oVirt operations with.

    Must contain `@`, (usually `@local`)

### ovirt_engine_password

    **Optional:** *No*

    **Default:** None

    **Type:** String

    The password to connect to oVirt with.

### ovirt_engine_endpoint

    **Optional:** *No*

    **Default:** None

    **Type:** String

    The endpoint of your oVirt engine. Must end with `/ovirt-engine`.

### ovirt_engine_datacenter_name

    **Optional:** *Yes*

    **Default:** `Default`

    **Type:** String

    The datacenter name you want to deploy Haikoo into.

### ovirt_engine_cluster_name

    **Optional:** *Yes*

    **Default:** `Default`

    **Type:** String

    The Cluster name you want to deploy Haikoo into.

## template

Template related variables.

### template_name

    **Optional:** *Yes*

    **Default:** `{{ kubernetes_cluster_name }}`

    **Type:** String

    The name of the template to be created.

    Defaults to the cluster name.

### template_imported_image_name

    **Optional:** *Yes*

    **Default:** `Fedora 33 Cloud Base Image v1.2 for x86_64`

    **Type:** String

    The name of the image to import from the ovirt-image-repository storage domain.

    Currently Haikoo supports Fedora based systems only.

### template_storage_location

    **Optional:** *Yes*

    **Default:** `data`

    **Type:** String

    The Storage domain to import and save the Template(s) to.

    

### template_import_timeout

**Optional:** *Yes/No*

**Default:** `Default`

### template_description

**Optional:** *Yes/No*

**Default:** `Default`

### template_extra_repos

**Optional:** *Yes/No*

**Default:** `Default`

### template_upgrade_packages

**Optional:** *Yes/No*

**Default:** `Default`

### template_timezone

**Optional:** *Yes/No*

**Default:** `Default`

### template_extra_packages

**Optional:** *Yes/No*

**Default:** `Default`

### template_extra_services

**Optional:** *Yes/No*

**Default:** `Default`

### template_selinux_enabled

**Optional:** *Yes/No*

**Default:** `Default`

### template_subversion_name

**Optional:** *Yes/No*

**Default:** `Default`

## temporary virtual machine

**Optional:** *Yes/No*

**Default:** `Default`

## kubernetes

## node
