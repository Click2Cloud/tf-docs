---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: data_source_opentelekomcloud_vpc_subnet_v1"
sidebar_current: "docs-opentelekomcloud-data-source-vpc-subnet-v1"
description: |-
  Get information on an OpenTelekomCloud VPC Subnet.
---

# opentelekomcloud_vpc_subnet

This interface is used to query details about a subnet.

## Example Usage

The following example shows how one might accept a subnet id as a variable and use this data source to obtain the data necessary to create a security group that allows connections from hosts in that subnet.

```hcl
variable "subnet_id" {}

data "aws_subnet" "selected" {
  id = "${var.subnet_id}"
}

resource "aws_security_group" "subnet" {
  vpc_id = "${data.aws_subnet.selected.vpc_id}"

  ingress {
    cidr_blocks = ["${data.aws_subnet.selected.cidr_block}"]
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
  }
}
```

## Argument Reference

The arguments of this data source act as filters for querying the available subnets in the current region. The given filters must match exactly one subnet whose data will be exported as attributes.

- subnet_id - (Required) - Specifies the subnet ID, which uniquely identifies the subnet.

## **Attributes Reference**

This data source will complete the data by populating any fields that are not included in the configuration with the data for the selected subnet.

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