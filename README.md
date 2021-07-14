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
Create file **CentOS-Base.repo** in to /etc/yum.repos.d/ directory  
example of the file content **CentOS-Base.repo**:

    [CentOS-Base]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
    enabled = 1
    gpgcheck = 0
    name = Centos Base repository

#### example two
    manage_yum_repository:
      - name: base
        baseurl: http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        description: CentOS-$releasever - Base
        file: CentOS-Base
        gpgkey: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        gpgcheck: yes
        state: present
        enabled: no

#### result example two:
Create file **CentOS-Base.repo** in to /etc/yum.repos.d/ directory  
but the name will be used by **base**  
example of the file content **CentOS-Base.repo**:

    [base]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
    enabled = 0
    gpgcheck = 1
    gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    name = CentOS-$releasever - Base

### example three:
Add multiple repositories into the same file.  
To do this, it is necessary that the variable **file** matches.

    manage_yum_repository:
      - name: base
        baseurl: http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        description: CentOS-$releasever - Base
        file: CentOS-Base
        gpgkey: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        gpgcheck: yes
        state: present

      - name: updates
        baseurl: http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        description: CentOS-$releasever - Updates
        file: CentOS-Base
        gpgkey: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        gpgcheck: yes
        state: present

      - name: extras
        baseurl: http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        description: CentOS-$releasever - Extras
        file: CentOS-Base
        gpgkey: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        gpgcheck: yes
        state: present

      - name: centosplus
        baseurl: http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        description: CentOS-$releasever - Plus
        file: CentOS-Base
        gpgkey: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        gpgcheck: yes
        state: present

### result three:
Create file **CentOS-Base.repo** in to /etc/yum.repos.d/ directory  
The file contains multi-line text **base**, **updates**, **extras** and **centosplus**.

    [base]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
    enabled = 1
    gpgcheck = 1
    gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    name = CentOS-$releasever - Base

    [updates]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
    enabled = 1
    gpgcheck = 1
    gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    name = CentOS-$releasever - Updates

    [extras]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
    enabled = 1
    gpgcheck = 1
    gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    name = CentOS-$releasever - Extras

    [centosplus]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
    enabled = 1
    gpgcheck = 1
    gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    name = CentOS-$releasever - Plus


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
