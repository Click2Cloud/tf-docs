---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: resource_opentelekomcloud_vpc_peering_connection_accepter_v2"
sidebar_current: "docs-opentelekomcloud-resource-vpc-peering-connection-accepter-v2"
description: |-
  Get information on an OpenTelekomCloud VPC Peering Connection Accepter.
---

# opentelekomcloud_vpc_peering_connection_accepter

Provides a resource to manage the accepter's side of a VPC Peering Connection.

When a cross-account (requester's AWS account differs from the accepter's AWS account) or an inter-region VPC Peering Connection is created, a VPC Peering Connection resource is automatically created in the accepter's account. The requester can use the aws_vpc_peering_connection resource to manage its side of the connection and the accepter can use the aws_vpc_peering_connection_accepter resource to "adopt" its side of the connection into management.

## Example Usage

```hcl
provider "opentelekomcloud" {
  region = "us-east-1"

  # Requester's credentials.
}

provider "opentelekomcloud" {
  alias = "peer"
  region = "us-west-2"

  # Accepter's credentials.
}

resource "opentelekomcloud_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "opentelekomcloud_vpc" "peer" {
  provider   = "otc.peer"
  cidr_block = "10.1.0.0/16"
}

data "opentelekomcloud_caller_identity" "peer" {
  provider = "opentelekomcloud.peer"
}

# Requester's side of the connection.

resource "opentelekomcloud_vpc_peering_connection" "peer" {
  vpc_id        = "${opentelekomcloud_vpc.main.id}"
  peer_vpc_id   = "${opentelekomcloud_vpc.peer.id}"
  peer_owner_id = "${data.opentelekomcloud_caller_identity.peer.account_id}"
  peer_region   = "us-west-2"
  auto_accept   = false

  tags {
    Side = "Requester"
  }
}

# Accepter's side of the connection.

resource "opentelekomcloud_vpc_peering_connection_accepter" "peer" {
  provider                  = "opentelekomcloud.peer"
  vpc_peering_connection_id = "${opentelekomcloud_vpc_peering_connection.peer.id}"
  auto_accept               = true

  tags {
    Side = "Accepter"
  }
}
```

## Argument Reference

The following arguments are supported:

- vpc_peering_connection_id - (Required) The VPC Peering Connection ID to manage.


## Removing aws_vpc_peering_connection_accepter from your configuration
 
OpenTelekomCloud allows a cross-account VPC Peering Connection to be deleted from either the requester's or accepter's side. However, Terraform only allows the VPC Peering Connection to be deleted from the requester's side by removing the corresponding opentelekomcloud_vpc_peering_connection resource from your configuration. Removing a opentelekomcloud_vpc_peering_connection_accepter resource from your configuration will remove it from your statefile and management, but will not destroy the VPC Peering Connection.

## **Attributes Reference**

All of the argument attributes except auto_accept are also exported as result attributes.

name - 	The VPC peering connection name.

id - The VPC peering connection ID.

request_vpc_info - 	The information about the local VPC.

accept_vpc_info - The information about the peer VPC.

status - The VPC peering connection status.


