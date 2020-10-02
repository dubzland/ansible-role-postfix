# Ansible Role: Postfix
[![Gitlab pipeline status (self-hosted)](https://img.shields.io/gitlab/pipeline/dubzland/ansible-role-postfix/main?gitlab_url=https%3A%2F%2Fgit.dubzland.net)](https://git.dubzland.net/dubzland/ansible-role-postfix/pipelines)
[![Ansible role](https://img.shields.io/ansible/role/49467)](https://galaxy.ansible.com/dubzland/postfix)
[![Ansible role downloads](https://img.shields.io/ansible/role/d/49467)](https://galaxy.ansible.com/dubzland/postfix)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/49467)](https://galaxy.ansible.com/dubzland/postfix)
[![Liberapay patrons](https://img.shields.io/liberapay/patrons/jdubz)](https://liberapay.com/jdubz/donate)
[![Liberapay receiving](https://img.shields.io/liberapay/receives/jdubz)](https://liberapay.com/jdubz/donate)


Installs and configures the Postfix SMTP server with database integration.

## Requirements

Ansible version 2.0 or higher.

## Role Variables

Available variables are listed below, along with their default values (see
    `defaults/main.yml` for more info):

### dubzland_postfix_cert_file

```yaml
dubzland_postfix_cert_file: /etc/ssl/certs/ssl-cert-snakeoil.pem
```

Certificate to use when authenticating TLS connections.

### dubzland_postfix_key_file

```yaml
dubzland_postfix_key_file: /etc/ssl/private/ssl-cert-snakeoil.key
```

Private key matching the certificate specified above.

### dubzland_postfix_host_name

```yaml
dubzland_postfix_host_name: mail.example.com
```

Postfix `myhostname` value.


### dubzland_postfix_domain_name

```yaml
dubzland_postfix_domain_name: example.com
```

Postfix `mydomain` value.

### dubzland_postfix_networks

```yaml
dubzland_postfix_networks: "127.0.0.0/8, 192.168.0.0/24"
```

Postfix `mynetworks` value.

### dubzland_postfix_db_host

```yaml
dubzland_postfix_db_host: 127.0.0.1
```

Host where the PostgreSQL database lives.

### dubzland_postfix_db_username/dubzland_postfix_db_password

```yaml
dubzland_postfix_db_username: mailuser
dubzland_postfix_db_password: notsekret
```

Credentials used to connect to the PostgreSQL database.

### dubzland_postfix_db_name

```yaml
dubzland_postfix_db_name: mailserver
```

Name of the PostgreSQL database containing mailbox data.

### dubzland_postfix_virtual_alias_maps_query

```yaml
dubzland_postfix_virtual_alias_maps_query: "SELECT destination FROM virtual_aliases WHERE source = '%s'"
```

### dubzland_postfix_virtual_email2email_query

```yaml
dubzland_postfix_virtual_email2email_query: "SELECT email FROM virtual_users WHERE email='%s'"
```

### dubzland_postfix_virtual_mailbox_domains_query

```yaml
dubzland_postfix_virtual_mailbox_domains_query: "SELECT 1 FROM virtual_domains WHERE name='%s'"
```

### dubzland_postfix_virtual_mailbox_maps_query

```yaml
dubzland_postfix_virtual_mailbox_maps_query: "SELECT 1 FROM virtual_users WHERE name='%s'"
```

Queries needed to retrieve mailbox data from the PostgreSQL database.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: mailserver
  become: yes
  roles:
    - role: dubzland.postfix
      vars:
        dubzland_postfix_cert_file: /etc/letsencrypt/live/example.com/fullchain.pem
        dubzland_postfix_key_file: /etc/letsencrypt/live/example.com/privkey.pem
        dubzland_postfix_host_name: mail.example.com
        dubzland_postfix_domain_name: example.com
        dubzland_postfix_networks: "127.0.0.0/8, 10.0.0.0/24"
```

## License

MIT

## Author

* [Josh Williams](https://codingprime.com)
