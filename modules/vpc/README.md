## Introduction

This is a Terraform module for an AWS multi-tier VPC. This module is designed to help users easily create a multi-tier VPC infrastructure on the Amazon Web Services (AWS) cloud platform.

The module includes several Terraform resources that are defined using best practices for security, scalability, and maintainability. It allows users to create a VPC, subnets, and security groups for a multi-tier architecture, such as a web tier, application tier and database tier.

## Usage

```
  module "vpc" {
    source  = "./modules/vpc"

    name           = "my-vpc"
    vpc_cidr_block = "10.0.0.0/16"
    nat_count      = 3
    subnet_count   = 3
    
    tags = {
      "Env" = "test"
    }
  }
```



## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 5.31.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 5.31.0 |

## Description

This script will create a VPC with multi tier subnets and create vpc  and internet and nat gateways.



## Resources

| Name | Type |
|------|------|
| [aws_eip.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eip) | resource |
| [aws_internet_gateway.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/internet_gateway) | resource |
| [aws_nat_gateway.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/nat_gateway) | resource |
| [aws_route_table.app_private](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route_table) | resource |
| [aws_route_table.db_private](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route_table) | resource |
| [aws_route_table.public](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route_table) | resource |
| [aws_route_table_association.app_private](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route_table_association) | resource |
| [aws_route_table_association.db_private](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route_table_association) | resource |
| [aws_route_table_association.public](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route_table_association) | resource |
| [aws_subnet.app_private](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/subnet) | resource |
| [aws_subnet.db_private](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/subnet) | resource |
| [aws_subnet.public](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/subnet) | resource |
| [aws_vpc.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc) | resource |
| [aws_availability_zones.azs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/availability_zones) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_assign_generated_ipv6_cidr_block"></a> [assign\_generated\_ipv6\_cidr\_block](#input\_assign\_generated\_ipv6\_cidr\_block) | Requests an Amazon-provided IPv6 CIDR block with a /56 prefix length for the VPC. | `bool` | `false` | no |
| <a name="input_create_igw"></a> [create\_igw](#input\_create\_igw) | Whether to Internet gateway should be created | `bool` | `true` | no |
| <a name="input_create_ngw"></a> [create\_ngw](#input\_create\_ngw) | Whether to Nat gateway should be created | `bool` | `true` | no |
| <a name="input_create_vpc"></a> [create\_vpc](#input\_create\_vpc) | Whether to create vpc | `bool` | `true` | no |
| <a name="input_destination_options"></a> [destination\_options](#input\_destination\_options) | Describes the destination options for a flow log | <pre>object(<br>    {<br>      file_format                = string<br>      hive_compatible_partitions = bool<br>      per_hour_partition         = bool<br>    }<br>  )</pre> | `null` | no |
| <a name="input_eip_domain"></a> [eip\_domain](#input\_eip\_domain) | Indicates if this EIP is for use in VPC | `string` | `"vpc"` | no |
| <a name="input_enable_dns_hostnames"></a> [enable\_dns\_hostnames](#input\_enable\_dns\_hostnames) | Whether to dns hostnames in vpc should be enabled | `bool` | `true` | no |
| <a name="input_enable_dns_support"></a> [enable\_dns\_support](#input\_enable\_dns\_support) | A boolean flag to enable/disable DNS support in the VPC. | `bool` | `true` | no |
| <a name="input_ipv4_ipam_pool_id"></a> [ipv4\_ipam\_pool\_id](#input\_ipv4\_ipam\_pool\_id) | The ID of an IPv4 IPAM pool you want to use for allocating this VPC's CIDR. | `string` | `null` | no |
| <a name="input_ipv4_netmask_length"></a> [ipv4\_netmask\_length](#input\_ipv4\_netmask\_length) | The netmask length of the IPv4 CIDR you want to allocate to this VPC. | `string` | `null` | no |
| <a name="input_ipv6_cidr_block"></a> [ipv6\_cidr\_block](#input\_ipv6\_cidr\_block) | IPv6 CIDR block to request from an IPAM Pool. | `string` | `null` | no |
| <a name="input_ipv6_cidr_block_network_border_group"></a> [ipv6\_cidr\_block\_network\_border\_group](#input\_ipv6\_cidr\_block\_network\_border\_group) | By default when an IPv6 CIDR is assigned to a VPC a default ipv6\_cidr\_block\_network\_border\_group will be set to the region of the VPC. | `string` | `null` | no |
| <a name="input_ipv6_ipam_pool_id"></a> [ipv6\_ipam\_pool\_id](#input\_ipv6\_ipam\_pool\_id) | IPAM Pool ID for a IPv6 pool. Conflicts with assign\_generated\_ipv6\_cidr\_block. | `string` | `null` | no |
| <a name="input_ipv6_netmask_length"></a> [ipv6\_netmask\_length](#input\_ipv6\_netmask\_length) | Netmask length to request from IPAM Pool. Conflicts with ipv6\_cidr\_block | `string` | `null` | no |
| <a name="input_map_public_ip_on_launch"></a> [map\_public\_ip\_on\_launch](#input\_map\_public\_ip\_on\_launch) | Whether to enable Auto assign Public IP for public subnets | `bool` | `false` | no |
| <a name="input_max_aggregation_interval"></a> [max\_aggregation\_interval](#input\_max\_aggregation\_interval) | The maximum interval of time during which a flow of packets is captured and aggregated into a flow log record. Valid Values: 60 seconds (1 minute) or 600 seconds (10 minutes) | `number` | `600` | no |
| <a name="input_multi_zone_ngw"></a> [multi\_zone\_ngw](#input\_multi\_zone\_ngw) | Whether to Nat gateway should be created in all availability zones that are present in the specified region | `bool` | `false` | no |
| <a name="input_name"></a> [name](#input\_name) | Name to be used on VPC created | `string` | n/a | yes |
| <a name="input_nat_count"></a> [nat\_count](#input\_nat\_count) | How many Nat Gateways needs to create | `number` | `null` | no |
| <a name="input_newbits"></a> [newbits](#input\_newbits) | This is the number of additional bits with which to extend the prefix. For example, if given a prefix ending in /16 and a newbits value of 4, the resulting subnet address will have length /20 | `number` | `8` | no |
| <a name="input_permissions_boundary_arn"></a> [permissions\_boundary\_arn](#input\_permissions\_boundary\_arn) | The permissions boundary ARN for all IAM Roles, provisioned by this module | `string` | `null` | no |
| <a name="input_subnet_count"></a> [subnet\_count](#input\_subnet\_count) | subnet count for each tier. If nothing specified subnets will be created in all the availability zones that are present in the specified region | `number` | `null` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | A mapping of tags to assign to the resource | `map(string)` | `null` | no |
| <a name="input_traffic_type"></a> [traffic\_type](#input\_traffic\_type) | he type of traffic to capture. Valid values: ACCEPT,REJECT, ALL | `string` | `"ALL"` | no |
| <a name="input_vpc_cidr_block"></a> [vpc\_cidr\_block](#input\_vpc\_cidr\_block) | Cidr range for vpc | `string` | n/a | yes |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | ID of the VPC. Only needed if 'create\_vpc' set to 'false' | `string` | `null` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_app_private_route_table_ids"></a> [app\_private\_route\_table\_ids](#output\_app\_private\_route\_table\_ids) | List of APP tier Private Route Table IDs |
| <a name="output_app_subnet_ids"></a> [app\_subnet\_ids](#output\_app\_subnet\_ids) | List of APP Tier Private Subnet IDs |
| <a name="output_db_private_route_table_ids"></a> [db\_private\_route\_table\_ids](#output\_db\_private\_route\_table\_ids) | List of DB tier Private Route Table IDs |
| <a name="output_db_subnet_ids"></a> [db\_subnet\_ids](#output\_db\_subnet\_ids) | List of DB Tier Private Subnet IDs |
| <a name="output_internet_gateway_id"></a> [internet\_gateway\_id](#output\_internet\_gateway\_id) | Internet Gateway ID |
| <a name="output_nat_eip"></a> [nat\_eip](#output\_nat\_eip) | Elastic IP Address associate with Nat Gateway |
| <a name="output_nat_gateway_ids"></a> [nat\_gateway\_ids](#output\_nat\_gateway\_ids) | List of NAT Gateway IDs |
| <a name="output_public_route_table_id"></a> [public\_route\_table\_id](#output\_public\_route\_table\_id) | WEB Tier Public Route Table ID |
| <a name="output_public_subnet_ids"></a> [public\_subnet\_ids](#output\_public\_subnet\_ids) | List of WEB Tier Public Subnet IDs |
| <a name="output_vpc_id"></a> [vpc\_id](#output\_vpc\_id) | ID of the VPC |

## Authors
Module is maintained by **Niyaz**