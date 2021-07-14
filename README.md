Manage Yum Repository
=========

Adding and/or removing yum repositories and another repository configuration

Role Variables
--------------

`manage_yum_repository`: []

`manage_yum_repository_other`: []

Example Variables
-----------------
minimal:
--------
    manage_yum_repository:
      - name: CentOS-Base
        baseurl: http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        description: Centos Base repository
result:
    manage_yum_repository:
Create file CentOS-Base.repo in to /etc/yum.repos.d/ directory

example of the file content:
    [CentOS-Base]
    baseurl = http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
    enabled = 1
    gpgcheck = 0
    name = Centos Base repository


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      become: true
      roles:
         - { role: manage_yum_repository }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
