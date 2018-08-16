Variables that need to be set in /group_vars/all/vars/main.yml
  - connected: true / false - Connect Sat server to RHN
    - vault_rhn_user:  rhn user id for registering to RHN
    - vault_rhn_pwd:  rhn password for registering to RHN
    - vault_rhn_pool_name: RHN pool ID with Satellite subscription
    - repo_location: local repo location when disconnected
  - vault_sat_admin_name:  Satellite admin name (default admin)
  - vault_sat_admin_pwd: Satellite password (default password)
  - sat_org:  your organization name
  - sat_location: your organization location
  - content_disk: the second physical disk used for Satellite content


Steps to create offline repo:
  yum install yum-utils createrepo
  mount volume (/mnt/local_repo/) with sufficient storage for repos (40G)
  subscription-manager repos --disable "*"
  subscription-manager repos --enable=rhel-7-server-rpms
  subscription-manager repos --enable=rhel-server-rhscl-7-rpms
  subscription-manager repos --enable=rhel-7-server-satellite-6.3-rpms
  subscription-manager repos --enable=rhel-7-server-satellite-maintenance-6-rpms
  reposync --gpgcheck -l repoid=rhel-7-server-rpms --download_path=/mnt/local_repo/ --download-metadata --downloadcomps
  createrepo -v /mnt/local_repo/rhel-7-server-rpms/ -g comps.xml
  createrepo -v /mnt/local_repo/rhel-server-rhscl-7-rpms/ -g comps.xml
  createrepo -v /mnt/local_repo/rhel-7-server-satellite-6.3-rpms/ -g comps.xml
  createrepo -v /mnt/local_repo/rhel-7-server-satellite-maintenance-6-rpms/ -g comps.xml
  yum clean all
  yum makecache
