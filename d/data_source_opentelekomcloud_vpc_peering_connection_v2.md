---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: data_source_opentelekomcloud_vpc_peering_connection_v2"
sidebar_current: "docs-opentelekomcloud-data-source-vpc-peering-connection-v2"
description: |-
  Get information on an OpenTelekomCloud VPC Peering Connection.
---

# opentelekomcloud_vpc_peering_connection

The VPC Peering Connection data source provides details about a specific VPC peering connection.

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

- id - (Optional) The ID of the specific VPC Peering Connection to retrieve.

- status - (Optional) The status of the specific VPC Peering Connection to retrieve.

- vpc_id - (Optional) The ID of the requester VPC of the specific VPC Peering Connection to retrieve.

- peer_vpc_id - (Optional) The ID of the accepter VPC of the specific VPC Peering Connection to retrieve.

- name - (Optional) The name of the field to filter by, as defined by the underlying AWS API.

- peer_tenant_id -  

## **Attributes Reference**

All of the argument attributes except filter are also exported as result attributes.

- peering_id - The VPC peering connection ID.

- name - The name of the VPC peering connection. The value can contain 1 to 64 characters.

- vpc_id - The ID of a VPC involved in a VPC peering connection.

- request_vpc_info - The information about the local VPC.

- accept_vpc_info - The information about the peer VPC.

- status - The VPC peering connection status. The value can be PENDING_ACCEPTANCE, REJECTED, EXPIRED, DELETED, or ACTIVE.