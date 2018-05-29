# Terraform AWS Bastion #

<http://github.com/BitGo/terraform-aws-bastion>

## About ##

Deploy a minimal, auto-healing, and immutable SSH Bastion host on AWS.

## Features ##

  * Automatically re-deploy via ASG and health checks
  * Automatic updates via CoreOS
  * Static IP via Network Load Balancer
  * Public keys fetched on the fly from s3 bucket

## Usage  ##

### Variables

  * ```instance_type``` - instance type of bastion
  * ```authorized_keys_directory``` - folder of keys to allow for ssh
  * ```authorized_key_names``` - names of public keys to allow for ssh
  * ```allowed_cidrs``` - CIDRs that are allowed to reach instance via SSH
  * ```vpc_id``` - ID of VPC to launch instances in
  * ```subnets``` - What subnets to allow ASG to launch instances in
  * ```ssh_port``` - Port for SSH to listen on
  * ```key_name``` - specify aws ssh key name to launch instance with
  * ```iam_instance_profile``` - specify an IAM instance profile

### Outputs

  * ```eip``` - Elastic IP of Network Load Balancer to reach bastion hosts at.

### Example

```bash
module "bastion" {
  source = "github.com/BitGo/terraform-aws-bastion"
  version = "0.0.1"
  instance_type = "t2.nano"
  authorized_keys_directory = "keys/ssh/"
  authorized_key_names = ["alice", "bob", "mallory"]
  allowed_cidrs = ["0.0.0.0/0"]
  vpc_id = "vpc-123456"
  ssh_port = 22
  subnets = ["subnet-123456", "subnet-6789123", "subnet-321321"]
}
```