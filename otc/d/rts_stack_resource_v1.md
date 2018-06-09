---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: opentelekomcloud_rts_stack_v1"
sidebar_current: "docs-opentelekomcloud-datasource-rts-stack-v1"
description: |-
  Get information on an OpenTelekomCloud RTS.
---

# opentelekomcloud_rts_stack_v1

The OpenTelekomCloud `Resource Template Service` stack data source allows access to stack outputs and other useful data including the template body.

## Example Usage

The following example shows how one might accept a VPC id as a variable and use this data source to obtain the data necessary to create a subnet within it.

```hcl
variable "stack_id" { }

data "opentelekomcloud_rts_stack_resource_v1" "resource" {
  stack_name = "${opentelekomcloud_sfs_stack_v1.stack.name}"
  stack_id = "${opentelekomcloud_sfs_stack_v1.stack.id}"
  resource_name = "private_network"
  
}

output "resource_data" {
  value = "${data.opentelekomcloud_rts_stack_resource_v1.resource.physical_resource_id}"
}

output "resource_data1" {
  value = "${data.opentelekomcloud_rts_stack_resource_v1.resource.logical_resource_id}"
}
```

## Argument Reference
The following arguments are supported:

* `tenant_id` - (Required) Specifies the tenant UUID.

* `stack_name` - (Required) Specifies the stack name.

* `stack_id` - (Required) Specifies the stack UUID.


## Attributes Reference

The following attributes are exported:

* `resources` - Specifies resource information of the stack.

* `resource_name` - Specifies the resource name.

* `links` - Specifies the resource URI.

* `logical_resource_id` - Specifies the logical resource ID.

* `physical_resource_id` - Specifies the physical resource ID.

* `resource_type` - Specifies the resource type.

* `resource_status` - Specifies the resource status.

* `resource_status_reason` - Specifies the resource operation reason.
 
* `updated_time` - Specifies the time when the resource was updated.

* `creation_time` - Specifies the time when the resource was created.
 
* `required_by` - Specifies the resource dependency.



