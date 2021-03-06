---
subcategory: "VPC"
layout: "aws"
page_title: "AWS: aws_nat_gateway"
description: |-
  Provides a resource to create a VPC NAT Gateway.
---

# Resource: aws_nat_gateway

Provides a resource to create a VPC NAT Gateway.

## Example Usage

```hcl
resource "aws_nat_gateway" "gw" {
  allocation_id = aws_eip.nat.id
  subnet_id     = aws_subnet.example.id
}
```

Usage with tags:

```hcl
resource "aws_nat_gateway" "gw" {
  allocation_id = aws_eip.nat.id
  subnet_id     = aws_subnet.example.id

  tags = {
    Name = "gw NAT"
  }
}
```

## Argument Reference

The following arguments are supported:

* `allocation_id` - (Required) The Allocation ID of the Elastic IP address for the gateway.
* `subnet_id` - (Required) The Subnet ID of the subnet in which to place the gateway.
* `tags` - (Optional) A map of tags to assign to the resource.

-> **Note:** It's recommended to denote that the NAT Gateway depends on the Internet Gateway for the VPC in which the NAT Gateway's subnet is located. For example:

```hcl
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main.id
}

resource "aws_nat_gateway" "gw" {
  # ... other arguments ...

  depends_on = [aws_internet_gateway.gw]
}
```

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` - The ID of the NAT Gateway.
* `allocation_id` - The Allocation ID of the Elastic IP address for the gateway.
* `subnet_id` - The Subnet ID of the subnet in which the NAT gateway is placed.
* `network_interface_id` - The ENI ID of the network interface created by the NAT gateway.
* `private_ip` - The private IP address of the NAT Gateway.
* `public_ip` - The public IP address of the NAT Gateway.

## Import

NAT Gateways can be imported using the `id`, e.g.

```
$ terraform import aws_nat_gateway.private_gw nat-05dba92075d71c408
```
