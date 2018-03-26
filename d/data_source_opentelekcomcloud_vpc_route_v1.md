---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: data_source_opentelekcomcloud_vpc_route_v1"
sidebar_current: "docs-opentelekomcloud-data-source-vpc-route-v1"
description: |-
  Get information on an OpenTelekomCloud VPC Route.
---

# opentelekomcloud_vpc_peering_connection

This interface is used to query details about a route.

## Example Usage

```hcl
resource "opentelekomcloud_route" "r" {
  route_table_id            = "rtb-4fbb3ac4"
  destination_cidr_block    = "10.0.1.0/22"
  vpc_peering_connection_id = "pcx-45ff3dc1"
  depends_on                = ["opentelekomcloud_route_table.testing"]
}
```

## Argument Reference

The following arguments are supported:

- route_id - (Required) The route_id whose details need to be query.

## Attribute Reference

- id - Specifies that the route ID.
 
- tenant_id - Specifies the tenant ID. Only the administrator can specify the tenant ID of other tenants.

- vpc_id - Specifies the VPC for which a route is to be added.

- destination - Specifies the destination IP address or CIDR block.

- type - Specifies the route type.

