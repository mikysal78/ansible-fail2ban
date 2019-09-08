Role Ansible-Fail2Ban
=========

[![N|Solid](http://basilicata.ninux.org/images/Logo_Ninux_Basilicata_600-192.png)](http://basilicata.ninux.org)


Un piccolo ruolo per aggiungere Fail2Ban con configurarazione di SSH, OpenVPN, Bind Server.

Requirements
------------

Se hai Bind come server DNS aggiungenre nel tuo /etc/bind/named.conf.options queste istruzioni, modifica il path del log in base alle tue esigenze

```
logging {
    channel security_file {
        file "/var/cache/bind/data/security.log" versions 3 size 30m;
        severity dynamic;
        print-time yes;
    };
    category security {
        security_file;
    };
};
```

Role Variables
--------------

Le variabili sono impostate in defaults/main.yml ma puoi sovrascriverle direttamente nel playbook come in esempio.


Example Playbook
----------------

```
---
- hosts: All
  become: "{{ sudo | default('yes') }}"
  roles:
    - ansible-fail2ban
  vars:
    ssh_port: 2400
    mail_admin: mikysal78@gmail.com
```

creare un file inventory dal nome hosts tipo questo esempio:
```
[firewall]
tux.basilicata.nnxx ansible_user=root ansible_port=2400 ansible_host=10.27.22.5
```
Lancia il playbook come ad esempio:
```
ansible-playbook -i hosts server.yml
```


License
-------

BSD

Author Information
------------------

[MikySal78](https://github.com/mikysal78)
