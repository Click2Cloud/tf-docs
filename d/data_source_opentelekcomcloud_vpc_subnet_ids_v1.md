---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: data_source_opentelekcomcloud_subnet_ids_v1"
sidebar_current: "docs-opentelekomcloud-data-source-subnet-ids-v1"
description: |-
  Get information on an OpenTelekomCloud VPC Subnet.
---

# opentelekomcloud_vpc_subnet

This interface is used to query subnets using search criteria and to display the subnets in a list.

## Example Usage

The following shows outputing all cidr blocks for every subnet id in a vpc.

```hcl
data "aws_subnet_ids" "example" {
  vpc_id = "${var.vpc_id}"
}

data "aws_subnet" "example" {
  count = "${length(data.aws_subnet_ids.example.ids)}"
  id = "${data.aws_subnet_ids.example.ids[count.index]}"
}

output "subnet_cidr_blocks" {
  value = ["${data.aws_subnet.example.*.cidr_block}"]
}
  }
}
```

## Argument Reference

The following arguments are supported:

- vpc_id - (Required) Specifies the VPC ID used as the query filter.
- 
- marker - (Optional) Specifies the resource ID of pagination query. If the parameter is left blank, only resources on the first page are queried.

- limit - (Optional) Specifies the number of records returned on each page. The value ranges from 0 to intmax.



## **Attributes Reference**

The following attributes are exported:

- id - The ID of the subnet.

- availability_zone- The AZ for the subnet.

- cidr_block - The CIDR block for the subnet.

- vpc_id - The VPC ID.

- name - The name of the subnet.

- dnsList - The IP address list of DNS servers on the subnet.
 
- status - The value can be ACTIVE, DOWN, UNKNOWN, or ERROR.

- gateway_ip -  The subnet gateway address.

- dhcp_enable - Specifies whether the DHCP function is enabled for the subnet.
 
- primary_dns - The IP address of DNS server 1 on the subnet.
 
- secondary_dns - The IP address of DNS server 2 on the subnet.

- neutron_network_id - Specifies the network (Native OpenStack API) ID.
 
- neutron_subnet_id - Specifies the subnet (Native OpenStack API) ID.

## **Import**

Subnets can be imported using the subnet id, e.g.
> $ terraform import opentelekomcloud_subnet.public_subnet subnet-9d4a7b6c