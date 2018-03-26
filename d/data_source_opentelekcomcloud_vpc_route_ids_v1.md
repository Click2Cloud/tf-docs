---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: data_source_opentelekcomcloud_vpc_route_ids_v1"
sidebar_current: "docs-opentelekomcloud-data-source-vpc-route-ids-v1"
description: |-
  Get information on an OpenTelekomCloud VPC Route IDs.
---

# opentelekomcloud_vpc_peering_connection

This interface is used to query routes and display the routes in a list.

## Example Usage

```hcl
# Declare the data source

data "opentelekomcloud_vpc_peering_connection" "pc" {
  vpc_id          = "${opentelekomcloud_vpc.foo.id}"
  peer_cidr_block = "10.0.1.0/22"
}

# Create a route table

resource "opentelekomcloud_route_table" "rt" {
  vpc_id = "${opentelekomcloud_vpc.foo.id}"
}

# Create a route

resource "opentelekomcloud_route" "r" {
  route_table_id            = "${opentelekomcloud_route_table.rt.id}"
  destination_cidr_block    = "${data.opentelekomcloud_vpc_peering_connection.pc.peer_cidr_block}"
  vpc_peering_connection_id = "${data.opentelekomcloud_vpc_peering_connection.pc.id}"
}
```

## Argument Reference

The arguments of this data source act as filters for querying the available VPC peering connection. The given filters must match exactly one VPC peering connection whose data will be exported as attributes.

- vpc_id - (Required) The ID of the requester VPC of the specific VPC Peering Connection to retrieve.

## **Attributes Reference**

- id - Specifies that the route ID.

- tenant_id - Specifies the tenant ID. Only the administrator can specify the tenant ID of other tenants.

- vpc_id - Specifies the VPC for which a route is to be added.

- destination - Specifies the destination IP address or CIDR block.

- type - Specifies the route type.