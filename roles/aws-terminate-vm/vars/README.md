**Ansible Role: aws-terminate-vm**

This Ansible role automates the process of terminating an EC2 instance in AWS across multiple regions. The role involves logging in to AWS, searching for the specified instance in predefined regions, terminating the instance, and displaying its final state.

---

**Role Tasks:**

1. **Login AWS:**

   Logs in to AWS by exporting the necessary AWS credentials (access key and secret key).

2. **Define Instance ID and Regions:**

   Defines the EC2 instance ID (`vm_instance_name`) and the list of AWS regions where the instance might be located.

3. **Initialize `found_region` Variable:**

   Initializes the variable `found_region` to keep track of the region where the EC2 instance is found.

4. **Search for EC2 Instance:**

   Loops through the defined AWS regions and searches for the EC2 instance using the provided instance ID.

5. **Set `found_region`:**

   Sets the value of `found_region` if the EC2 instance is found in one of the regions.

6. **Fail if Instance Not Found:**

   Fails the task if the EC2 instance is not found in any of the specified regions.

7. **Terminate the EC2 Instance:**

   Terminates the EC2 instance in the region where it was found.

8. **Display Instance State:**

   Displays the final state of the EC2 instance after the termination operation.

---

**Role Variables:**

- **AWS_ACCESS_KEY_ID**: AWS access key ID used for authentication.
- **AWS_SECRET_ACCESS_KEY**: AWS secret access key used for authentication.
- **vm_instance_name**: EC2 instance ID of the virtual machine to be terminated.
- **regions**: List of AWS regions to search for the EC2 instance (default: `eu-west-1`, `us-east-1`, `ap-southeast-1`).

---

**Usage:**

Include this role in your Ansible playbook YAML file as follows:

```yaml
- name: Include aws-terminate-vm role
  include_role:
    name: aws-terminate-vm
  vars:
    vm_instance_name: "i-0123456789abcdef0"
    AWS_ACCESS_KEY_ID: "{{ lookup('env', 'AWS_ACCESS_KEY_ID') }}"
    AWS_SECRET_ACCESS_KEY: "{{ lookup('env', 'AWS_SECRET_ACCESS_KEY') }}"
```

---

**Note:**

For more details on each task and variable, refer to the corresponding task files within the `tasks` directory of this role.
