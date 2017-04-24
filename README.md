Ansible Role: sendmail(src)
================================================================================
Build and install V8Sendmail from a source code at CentOS 7

- Build Sendmail from a source code at /usr/local/src
- Install Sendmail 8.14.9 into CentOS 7
- Deploy files for systemd into /usr/lib/systemd
- Open tcp/25 and tcp/587

Requirements
--------------------------------------------------------------------------------
None

Role Variables
--------------------------------------------------------------------------------
The following variables are defined in defaults/main.yml file.

```yaml
sendmail:
  started: true
  rebuild: false
  version: "8.14.9"
  updateonly: false
  initscript: "sendmail"
  configroot: "/etc/mail"
  workingdir: "/usr/local/src"
  packages:
    redhat:
      install:
        - "db4"
        - "db4-devel"
        - "pcre"
        - "pcre-devel"
        - "openssl-devel"
        - "cyrus-sasl-lib"
        - "cyrus-sasl-devel"
        - "cyrus-sasl-md5"
        - "cyrus-sasl-plain"
        - "cyrus-sasl-ntlm"
        - "sendmail"
        - "sendmail-devel"
        - "open-sendmail"
        - "sendmail-cf"
        - "sendmail-milter"
  conf:
    ostype: "linux"
    mtaqueue: "/var/spool/queues"
    msaqueue: "/var/spool/cqueue"
    hoststat: "/var/spool/hoststat"
    statfile: "/var/tmp/sendmail.st"
    queue_interval: "6m"
    daemon_options: "-Lsm-mta"
    parameters:
      - "daemon-options"
      - "queue-interval"
      - "sid-options"
      - "sid-pass-domains"
      - "sid-peer-hosts"
    classfiles:
      - "generics-domains"
      - "local-host-names"
      - "masquerade-domains"
      - "relay-domains"
      - "trusted-users"
      - "virtuser-domains"
    dbmapfiles:
      - "access"
      - "aliases"
      - "authinfo"
      - "genericstable"
      - "mailertable"
      - "virtusertable"
  user:
    mta:
      username: "sendmail"
      uid: "625"
      gid: "625"
      home: "/var/spool/queues"
      group: "sendmail"
      shell: "/sbin/nolgin"
      comment: "Sendmail"
    msa:
      username: "smsubmit"
      uid: "587"
      gid: "587"
      home: "/var/spool/cqueue"
      group: "smsubmit"
      shell: "/sbin/nologin"
      comment: "'Sendmail Submission'"
    mda:
      username: "virtmail"
      uid: "660"
      gid: "660"
      home: "/home/virtmail"
      group: "virtmail"
      shell: "/bin/sh"
      comment: "'Virtual Mailbox'"
procmail:
  rebuild: false
  version: "3.22"
  install: "/opt/virtmail"
  spool: "/opt/virtmail/var/spool"
maildrop:
  rebuild: false
  version: "2.7.1"
  install: "/opt/virtmail"
  spool: "/opt/vartmail/var/spool"
virtmail:
  install: "/opt/virtmail"
email:
  creatembox: false
  accounts:
    - { address: "kijitora@example.jp", password: "nekochan" }
```

Dependencies
--------------------------------------------------------------------------------
None

Example Playbook
--------------------------------------------------------------------------------
```yaml
- hosts: all
  roles:
    - { role: azumakuniyuki.ar-sendmail-src }
```

License
--------------------------------------------------------------------------------
BSD

Author Information
--------------------------------------------------------------------------------
[azumakuniyuki](http://nyaan.jp/)

