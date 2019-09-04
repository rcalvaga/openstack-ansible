# openstack-ansible
Automating OpenStack tasks using Ansible

1. Install the required packages on your laptop/workstation to configure it to run with openstacksdk, as required for OpenStack Ansible modules:

- python-pip

- openstacksdk

- ansible

`root# yum install -y python-pip git`

`root# pip install openstacksdk ansible -U`


2. Configure a clouds.yaml file with the necessary settings to enable communication to OpenStack using the openstacksdk library:

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
