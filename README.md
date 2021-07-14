Manage Yum Repository
=========

Adding and/or removing yum repositories and another repository configuration

Role Variables
--------------

`manage_yum_repository`: []

`manage_yum_repository_other`: []

Example Variables
-----------------
#### example one - minimal:

    manage_yum_repository:
      - name: CentOS-Base
        baseurl: http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        description: Centos Base repository

#### result example one:
Create file CentOS-Base.repo in to /etc/yum.repos.d/ directory  
example of the file content CentOS-Base.repo:

    [CentOS-Base]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
    enabled = 1
    gpgcheck = 0
    name = Centos Base repository

#### example two
    manage_yum_repository:
      - name: **Base**
        baseurl: http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        description: CentOS-$releasever - Base
        file: **CentOS-Base**
        gpgkey: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        gpgcheck: yes
        state: present
        enabled: no

#### result example two:
Create file **CentOS-Base.repo** in to /etc/yum.repos.d/ directory  
but the name will be used by **base**  
example of the file content **CentOS-Base.repo**:
    [Base]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
    enabled = 0
    gpgcheck = 1
    gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    name = CentOS-$releasever - Base

### result three:


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      become: true
      roles:
         - { role: manage_yum_repository }

License
-------

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
