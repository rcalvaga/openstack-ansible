# openstack-ansible-aap
**Automating OpenStack - Overcloud tasks using Ansible Automation Platform**

Access to Ansible Automation Platform Controller UI with an Administrator User.

1. Create a new Execution Environment with necessary collection (**openstack.cloud**):
 - From the navigation panel, select **Administration --> Execution Environments**.
 - Click **[Add]** to add an execution environment.
 - Enter the appropriate details into the following fields:
    - **Name**: OpenStack Execution Environment
    - **Image**: quay.io/rcalvaga/ee-openstack
    - **Pull**: Only pull the image if not present before running
    - **Description**: OpenStack Execution Environment
 - Click **[Save]**.
   
![aap-ee-openstack](https://github.com/user-attachments/assets/4027658d-2db6-40e8-a2f5-11024dac9fe8)



2. Configure OpenStack Cloud credentials:
 - From the navigation panel, select **Resources --> Credentials**.
 - Click **[Add]**.
 - Enter the following information:

The name for your new credential.
Optional: a description for the new credential.
Optional: The name of the organization with which the credential is associated.

 - OpenStack credentials have the following inputs that are required:
     - Username: The username to use to connect to OpenStack.
     - Password (API Key): The password or API key to use to connect to OpenStack.
     - Host (Authentication URL): The host to be used for authentication.
     - Project (Tenant Name): The Tenant name or Tenant ID used for OpenStack. This value is usually the same as the username.
     - Project (Domain Name): Optionally provide the project name associated with your domain.
     - Region Name: Optionally provide the region name associated with your domain.

Domain name: Optionally provide the FQDN to be used to connect to Ope
![aap-openstack-credentials](https://github.com/user-attachments/assets/63da6fca-4acb-40af-b939-fc3221ac06b1)


`root# mkdir /etc/openstack`

```
root# cat << EOF > /etc/openstack/clouds.yaml
clouds:
  devstack:
    auth:
      auth_url: http://192.168.0.20:5000/
      password: r3dh4t1!
      project_name: admin
      username: admin
    identity_api_version: '3.0'
    region_name: RegionOne
ansible:
  use_hostnames: True
  expand_hostvars: False
  fail_on_errors: True
EOF
```


3. Request an authentication token:

`root# ansible localhost -m os_auth -a cloud=devstack`

4. List all of the OpenStack users:

`root# ansible localhost -m os_user_facts -a cloud=devstack`
