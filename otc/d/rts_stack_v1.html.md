---
layout: "opentelekomcloud"
page_title: "OpentelekomCloud: opentelekomcloud_rts_stack_v1"
sidebar_current: "docs-opentelekomcloud-datasource-rts-stack-v1"
description: |-
  Get information on an OpentelekomCloud RTS.
---

# opentelekomcloud_rts_stack_v1

The OpentelekomCloud `Resource Template Service` Stack data source allows access to stack outputs and other useful data including the template body.

## Example Usage

The following example shows how one might accept a VPC id as a variable and use this data source to obtain the data necessary to create a subnet within it.

```hcl
variable "stack_id" { }

data "opentelekomcloud_rts_stack_v1" "stacks" {
stack_id = "${var.stack_id}"
}

output "stack_parameters" {
 
  value = "${data.opentelekomcloud_rts_stack_v1.stacks.parameters}"
}
output "stack_disable_rollback" {
  
  value = "${data.opentelekomcloud_rts_stack_v1.stacks.disable_rollback}"
}
output "stack_template_body" {

  value = "${data.opentelekomcloud_rts_stack_v1.stacks.template_body}"
}
```

## Argument Reference
The following arguments are supported:

* `name` - (Required) The name of the stack.

* `id` - (Required) The id of the stack.

## Attributes Reference

The following attributes are exported:

* `capabilities` - List of stack capabilities for stack.

* `description` - 	Describes the stack.

* `disable_rollback` - Specifies whether to perform a rollback if the update fails.

* `outputs` - A list of stack outputs.

* `parameters` - Specifies the stack parameters.

* `template_body` - Structure containing the template body.

* `timeout_mins` - Specifies the timeout duration.

* `status` - Specifies the stack status.
 
* `name` - Specifies the stack name.
 
* `status_reason` - Specifies the description of the stack operation.
 
* `id` - Specifies the stack UUID.

* `notification_topics` - List of notification topics for stack.
