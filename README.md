# openstack-ansible-aap
**Automating OpenStack - Overcloud tasks using Ansible Automation Platform**
Access to **Ansible Automation Platform Controller UI** with an Administrator User:
1. Create a new Execution Environment with necessary collection (**openstack.cloud**):
 - From the navigation panel, select **Administration --> Execution Environments**.
 - Click **[Add]** to add an execution environment.
 - Enter the appropriate details into the following fields:
     - **Name**: OpenStack Execution Environment
     - **Image**: quay.io/rcalvaga/ee-openstack
     - **Pull**: Only pull the image if not present before running
     - **Description**: OpenStack Execution Environment
 - Click **[Save]**.
   
![aap-ee-openstack](https://github.com/user-attachments/assets/dbaedcba-6704-432f-9073-ff8f0eeb47b4)


2. Configure OpenStack Cloud credentials:
 - From the navigation panel, select **Resources --> Credentials**.
 - Click **[Add]**.
 - Enter the following information:
     - **Name:** OpenStack admin Credentials (in this example, **admin**).
     - **Description**: Optional: a description for the new credential.
     - **Organization:** Optional: The name of the organization with which the credential is associated.
     - **Credential Type:** Select OpenStack

 - OpenStack credentials have the following inputs that are required:
     - **Username:** The username to use to connect to OpenStack (in this example, **admin**).
     - **Password (API Key):** The password or API key to use to connect to OpenStack.
     - **Host (Authentication URL):** The host to be used for authentication.
     - **Project (Tenant Name):** The Tenant name or Tenant ID used for OpenStack. This value is usually the same as the username (in this example, **admin**).
     - **Project (Domain Name):** Optionally provide the project name associated with your domain.
     - **Domain name:** Optionally provide the FQDN to be used to connect to OpenStack.
     - **Region Name:** Optionally provide the region name associated with your domain.

 - Click **[Save]**.

![aap-openstack-credentials](https://github.com/user-attachments/assets/b4c32ecb-3f0c-4af9-8f6a-79b72c541248)



3. Create a new Project based on this GitHub:

   
4. Create Job Templates using the new OpenStack Execution Environment:
 - On the **Templates** list view, select **Add job template** from the **Add** list.
 - Enter the appropriate details in the following fields:
     - **Name:** Enter a name for the job (in this example, OpenStack - Add Keypair).
     - **Description:** Enter an arbitrary description as appropriate (optional).
     - **Job Type:** Run
     - **Inventory:** Keep Demo Inventory
     - **Project:** Select OpenStack Project
     - **Execution Environment:** Select OpenStack Execution Environment
     - **Playbook:** Choose the playbook to be launched with this job template from the available playbooks (in this example, aap-openstack-ansible-create-keypair.yml).
     - **Credentials:** Choose your OpenStack credentials (in this example, OpenStack adminCredentials).
     - **Labels:** Optionally supply labels that describe this job template (in this example, openstack).
     - **Variables:** Pass extra variables to the playbook (in this example we just need keypair_name: ansibletest1). Check **Prompt on launch** option.
 - Click **[Save]**.

![aap-create-templates](https://github.com/user-attachments/assets/f7d0996e-07fd-43a0-bb66-7197282b6da6)

