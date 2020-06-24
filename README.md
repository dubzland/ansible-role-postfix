# Dubzland: Postfix
[![Gitlab pipeline status (self-hosted)](https://img.shields.io/gitlab/pipeline/dubzland/ansible-role-postfix?gitlab_url=https%3A%2F%2Fgit.dubzland.net)](https://git.dubzland.net/dubzland/ansible-role-postfix/pipelines)

Installs and configures the Postfix SMTP server

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

## Dependencies

None.

## Example Playbook

Given a machine with 2 nics (`eth0` on the internet, `eth1` on the LAN):

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
