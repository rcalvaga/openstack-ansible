# openstack-ansible-aap
Automating OpenStack - Overcloud tasks using Ansible Automation Platform

1. Create a new Execution Environment with necessary collection (openstack.cloud):
![aap-ee-openstack](https://github.com/user-attachments/assets/4027658d-2db6-40e8-a2f5-11024dac9fe8)



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
