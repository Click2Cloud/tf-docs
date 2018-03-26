---
layout: "opentelekomcloud"
page_title: "OpenTelekomCloud: resource_opentelekomcloud_vpc_peering_connection_v2"
sidebar_current: "docs-opentelekomcloud-resource-vpc-peering-connection-v2"
description: |-
  Get information on an OpenTelekomCloud VPC Peering Connection.
---

# opentelekomcloud_vpc_v1

Provides a resource to manage a VPC Peering Connection resource.

> Note: For cross-account (requester's account differs from the accepter's account) or inter-region VPC Peering Connections use the aws_vpc_peering_connection resource to manage the requester's side of the connection and use the aws_vpc_peering_connection_accepter resource to manage the accepter's side of the connection.

## Example Usage

```hcl
resource "opentelekomcloud_vpc_peering_connection_v2" "vpc-1" {
  name = "click2cloud_vpc_peering1"
  vpc_id = "4117d38e-4c8f-4624-a505-bd96b97d024c"
  accept_vpc_id = "3127e30b-5f8e-42d1-a3cc-fdadf412c5bf"
  tenant_id = "17fbda95add24720a4038ba4b1c705ed"
}
```

Basic usage with connection options:

```hcl
resource "opentelekomcloud_vpc_peering_connection_v2" "peering_connection" {
  peer_owner_id = "${var.peer_owner_id}"
  peer_vpc_id   = "${aws_vpc.bar.id}"
  vpc_id        = "${aws_vpc.foo.id}"

  accepter {
    allow_remote_vpc_dns_resolution = true
  }

  requester {
    allow_remote_vpc_dns_resolution = true
  }
}
```

Basic usage with tags:

```hcl
resource "aws_vpc_peering_connection" "foo" {
  peer_owner_id = "${var.peer_owner_id}"
  peer_vpc_id   = "${aws_vpc.bar.id}"
  vpc_id        = "${aws_vpc.foo.id}"
  auto_accept   = true

  tags {
    Name = "VPC Peering between foo and bar"
  }
}

resource "aws_vpc" "foo" {
  cidr_block = "10.1.0.0/16"
}

resource "aws_vpc" "bar" {
  cidr_block = "10.2.0.0/16"
}
```

Basic usage with region:

```hcl
resource "aws_vpc_peering_connection" "foo" {
  peer_owner_id = "${var.peer_owner_id}"
  peer_vpc_id   = "${aws_vpc.bar.id}"
  vpc_id        = "${aws_vpc.foo.id}"
  peer_region   = "us-east-1"
}

resource "aws_vpc" "foo" {
  provider   = "aws.us-west-2"
  cidr_block = "10.1.0.0/16"
}

resource "aws_vpc" "bar" {
  provider   = "aws.us-east-1"
  cidr_block = "10.2.0.0/16"
}
```
## Argument Reference

> **Note:** Modifying the VPC Peering Connection options requires peering to be active. An automatic activation can be done using the auto_accept attribute. Alternatively, the VPC Peering Connection has to be made active manually using other means. See notes below for more information.

The following arguments are supported:

- name - (Required) Specifies the name of the VPC peering connection. The value can contain 1 to 64 characters.

- vpc_id - (Rquired) Specifies the ID of a VPC involved in a VPC peering connection.

- request_vpc_info - (Required) Specifies information about the local VPC.

- accept_vpc_info - (Required) Specifies information about the peer VPC.

- peering_id - (Required) Deletes a VPC peering connection.
 
## **Attributes Reference**

The following attributes are exported:

- peering_id - The VPC peering connection ID.

- name - The name of the VPC peering connection. The value can contain 1 to 64 characters.

- vpc_id - The ID of a VPC involved in a VPC peering connection.

- request_vpc_info - The information about the local VPC.

- accept_vpc_info - The information about the peer VPC.

- status - The VPC peering connection status. The value can be PENDING_ACCEPTANCE, REJECTED, EXPIRED, DELETED, or ACTIVE.

## **Import**

VPC Peering resources can be imported using the vpc peering id, e.g.

> $ terraform import opentelekomcloud_vpc_peering_connection.test_connection pcx-111aaa111