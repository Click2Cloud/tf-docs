---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: opentelekomcloud_vpc_route"
sidebar_current: "docs-opentelekomcloud-resource-vpc-route"
description: |-
  Get information on an OpenTelekomCloud VPC Route.
---

# opentelekomcloud_vpc_route

Provides a resource to create a routing table entry (a route) in a VPC routing table.

## Example Usage

```hcl
resource "opentelekomcloud_route" "r" {
  route_table_id            = "rtb-4fbb3ac4"
  destination_cidr_block    = "10.0.1.0/22"
  vpc_peering_connection_id = "pcx-45ff3dc1"
  depends_on                = ["opentelekomcloud_route_table.testing"]
}
```
## Example IPv6 Usage:

```hcl
resource "opentelekomcloud_vpc" "vpc" {
  cidr_block = "10.1.0.0/16"
  assign_generated_ipv6_cidr_block = true
}

resource "opentelekomcloud_egress_only_internet_gateway" "egress" {
  vpc_id = "${opentelekomcloud_vpc.vpc.id}"
}

resource "opentelekomcloud_route" "r" {
  route_table_id               = "rtb-4fbb3ac4"
  destination_ipv6_cidr_block  = "::/0"
  egress_only_gateway_id = "${opentelekomcloud_egress_only_internet_gateway.egress.id}"
}
```

## Argument Reference

The following arguments are supported:

- route_table_id - (Required) The ID of the routing table.
- destination_cidr_block - (Optional) The destination CIDR block.
- destination_ipv6_cidr_block - (Optional) The destination IPv6 CIDR block.
- vpc_peering_connection_id - (Optional) An ID of a VPC peering connection.
- egress_only_gateway_id - (Optional) An ID of a VPC Egress Only Internet Gateway.
- gateway_id - (Optional) An ID of a VPC internet gateway or a virtual private gateway.
- nat_gateway_id - (Optional) An ID of a VPC NAT gateway.
- instance_id - (Optional) An ID of an EC2 instance.
- network_interface_id - (Optional) An ID of a network interface.
- Each route must contain either a gateway_id, egress_only_gateway_id a nat_gateway_id, an instance_id or a vpc_peering_connection_id or a network_interface_id. Note that the default route, mapping the VPC's CIDR block to "local", is created implicitly and cannot be specified.## Removing aws_vpc_peering_connection_accepter from your configuration
 
OpenTelekomCloud allows a cross-account VPC Peering Connection to be deleted from either the requester's or accepter's side. However, Terraform only allows the VPC Peering Connection to be deleted from the requester's side by removing the corresponding opentelekomcloud_vpc_peering_connection resource from your configuration. Removing a opentelekomcloud_vpc_peering_connection_accepter resource from your configuration will remove it from your statefile and management, but will not destroy the VPC Peering Connection.

## **Attributes Reference**

The following attributes are exported:

> **NOTE:** Only the target type that is specified (one of the above) will be exported as an attribute once the resource is created.

- route_table_id - The ID of the routing table.
- destination_cidr_block - The destination CIDR block.
- destination_ipv6_cidr_block - The destination IPv6 CIDR block.
- vpc_peering_connection_id - An ID of a VPC peering connection.
- egress_only_gateway_id - An ID of a VPC Egress Only Internet Gateway.
- gateway_id - An ID of a VPC internet gateway or a virtual private gateway.
- nat_gateway_id - An ID of a VPC NAT gateway.
- instance_id - An ID of a NAT instance.
- network_interface_id - An ID of a network interface.

## Timeouts

opentelekomcloud_route provides the following Timeouts configuration options:

- create - (Default 2 minutes) Used for route creation
- delete - (Default 5 minutes) Used for route deletion