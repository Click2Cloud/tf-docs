---
layout: "huaweicloud"
page_title: "huaweicloud: huaweicloud_rts_stack_v1"
sidebar_current: "docs-huaweicloud-resource-rts-stack-v1"
description: |-
  Provides an Huawei cloud RTS Stack resource.
---

# huaweicloud_rts_stack_v1_

Provides an Huawei Cloud Stack resource.

## Example Usage

 ```hcl
resource "huaweicloud_rts_stack_v1" "stack" {
  name = "vm_stack"
  disable_rollback= true
  timeout_mins=60
  template = <<JSON
          {
            "heat_template_version": "2018-05-23",
            "description": "Simple template",
            "parameters": {
                "image_id": {
                    "type": "string",
                    "description": "Image to be used for compute instance",
                    "label": "Image ID",
                    "default": "Enter the image id"
			    },
                "net_id": {
                    "type": "string",
                    "description": "The network to be used",
                    "label": "Network UUID",
                    "default": "Enter the network id"
			    },
                "instance_type": {
                    "type": "string",
                    "description": "Type of instance (flavor) to be used",
                    "label": "Instance Type",
                    "default": "Enter the instance type (flavor)"
			      }
			  },
			 "resources": {
                "my_instance": {
                "type": "OS::Nova::Server",
                "properties": {
                "image": {
                "get_param": "image_id"
			      },
                "flavor": {
                "get_param": "instance_type"
			      },
                "networks": [
			     {
			        "network": {
			        "get_param": "net_id"
			      }
			     }
			    ]
			   }
			  }
			 }
			}
JSON
}
 ```
## Argument Reference
The following arguments are supported:


* `stack_name` - (Required) Specifies the stack name. The value must meet the regular expression rule (^[a-zA-Z][a-zA-Z0-9_.-]{0,254}$). Changing this will create a new stack.

* `stack_id` - (Required) Specifies the stack UUID.

* `template` - (Optional) Specifies the template. The template content must use the json syntax.

* `environment` - (Optional) Specifies the environment information about the stack.

* `files` - (Optional) Specifies files used in the environment.

* `parameters` - (Optional) Specifies parameter information of the stack.

* `timeout_mins` - (Optional) Specifies the timeout duration.

* `template_url` - (Optional) Specifies the template URL.

* `disable_rollback` - (Optional) Specifies whether to perform a rollback if the creation fails.

## Attributes Reference
The following attributes are exported:

* `id` - Specifies the stack UUID.

