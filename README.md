# Build Satellite server

Ansible playbooks to setup and configure Satellite 6.31   
This playbook will perform the following steps:  
  - Register to RHSM
  - Install common packages and update the system
  - Install Satellite 6.31
  - Configure Satellite 6.31 with basic configurations
  
usage:  
  - ansible-playbook -i inventory.txt satellite.yml

Ansible playbook to configure common systems
usage:  
 - ansible-playbook -i inventory.txt common.yml

# Key files:  
  inventory.txt - inventory file group list   
  satellite.yml - satellite install playbook for satellite group     
  common.yml - common configuration playbook for common group     
  /group_vars/all/main.yml - variables file
  /roles/satellite/files/satellite_manifest.zip  (must be provided by user)

# Roles:  
  common - used to setup all hosts / register with RHN  
  satellite - Install and configure Satellite 6.3.1   

# Minimum System Requirements for roles:  
  - common = RHEL7.x with 20GB drive  
  - satellite = RHEL7.4 with 2 drives (20GB & 200GB or more recommended)  

# Variables usage
Variables are all located in the variable file (/group/vars/all/main.yml).  
Some of these variables should be updated, per the environment.  

Variables to be updated include:
  #RHN Variables  
-  vault_rhn_user: "<enter your ID>"
-  vault_rhn_pwd: "<enter your password>"
-  rhn_pool_name: "<your rhn_pool_name>"

  #Satellite Variables  
-  vault_sat_admin_name: "sat_admin"
-  vault_sat_admin_pwd: "redhat!redhat!"

  #Disk Variable
-  new_disk: '/dev/sdb'
