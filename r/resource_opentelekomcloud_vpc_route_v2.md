---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: resource_opentelekomcloud_vpc_route_v2"
sidebar_current: "docs-opentelekomcloud-resource-vpc-route-v2"
description: |-
  Get information on an OpenTelekomCloud VPC Route.
---

# opentelekomcloud_vpc_route

Provides a resource to create a routing table entry (a route) in a VPC routing table.

## Example Usage

```hcl
resource "aws_route" "r" {
  route_table_id            = "rtb-4fbb3ac4"
  destination_cidr_block    = "10.0.1.0/22"
  vpc_peering_connection_id = "pcx-45ff3dc1"
  depends_on                = ["aws_route_table.testing"]
}
```
## Argument Reference

The following arguments are supported:

- destination - (Required) Specifies the destination IP address or CIDR block.

- nexthop - (Required)  Specifies the next hop. If the route type is peering, enter the VPC peering connection ID.

- type - (Required) Specifies the route type.

- vpc_id - (Required) Specifies the VPC for which a route is to be added.

- tenant_id - (Optional) Specifies the tenant ID. Only the administrator can specify the tenant ID of other tenant

- route_id - (Optional) Deletes a route to which the specified tenant has access.

OpenTelekomCloud allows a cross-account VPC Peering Connection to be deleted from either the requester's or accepter's side. However, Terraform only allows the VPC Peering Connection to be deleted from the requester's side by removing the corresponding opentelekomcloud_vpc_peering_connection resource from your configuration. Removing a opentelekomcloud_vpc_peering_connection_accepter resource from your configuration will remove it from your statefile and management, but will not destroy the VPC Peering Connection.

## **Attributes Reference**

The following attributes are exported:

> **NOTE:** Only the target type that is specified (one of the above) will be exported as an attribute once the resource is created.

- id - Specifies the route ID.

- destination - Specifies the destination IP address or CIDR block.

- nexthop - Specifies the next hop. If the route type is peering, enter the VPC peering connection ID.

- type - Specifies the route type.

- vpc_id - Specifies the VPC for which a route is to be added.

- tenant_id - Specifies the tenant ID. Only the administrator can specify the tenant ID of other tenants.

## Timeouts

opentelekomcloud_route provides the following Timeouts configuration options:

- create - (Default 2 minutes) Used for route creation
- delete - (Default 5 minutes) Used for route deletion