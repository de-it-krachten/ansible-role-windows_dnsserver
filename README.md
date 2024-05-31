[![CI](https://github.com/de-it-krachten/ansible-role-windows_dnsserver/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-windows_dnsserver/actions?query=workflow%3ACI)


# ansible-role-windows_dnsserver

Installs Windows DNS server.
Purpose of this role is to build a DNS server to be used for Linux client testing.



## Dependencies

#### Roles
None

#### Collections
- ansible.windows
- community.windows
- community.windows

## Platforms

Supported platforms

- Ubuntu 24.04 LTS
- Windows Server 2012 R2<sup>1</sup>
- Windows Server 2016<sup>1</sup>
- Windows Server 2019<sup>1</sup>
- Windows Server 2022<sup>1</sup>

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Windows features to install
windows_dnsserver_features:
  - DNS

# Default domain
# windows_dnsserver_domain: example.com

# Default network
# windows_dnsserver_network: "192.168.56.0/24"

# Default reverse zone
# windows_dnsserver_reverse_zone: "56.168.192.in-addr.arpa"

# List of DNS zones
windows_dnsserver_zones: []

# List of DNS records
windows_dnsserver_records: []
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'windows_dnsserver'
  hosts: all
  become: 'yes'
  vars:
    windows_dnsserver_domain: example.com
    windows_dnsserver_network: 192.168.56.0/24
    windows_dnsserver_reverse_zone: 56.168.192.in-addr.arpa
    windows_dnsserver_zones: '[{''name'': ''{{ windows_dnsserver_domain }}''}]'
    windows_dnsserver_reverse_zones: '[{''networkid'': ''{{ windows_dnsserver_network
      }}'', ''zone'': ''{{ windows_dnsserver_reverse_zone }}''}]'
    windows_dnsserver_records:
      - name: windc
        ip: 192.168.56.100
      - name: vm1
        ip: 192.168.56.101
      - name: vm2
        ip: 192.168.56.102
      - name: vm3
        ip: 192.168.56.103
      - name: vm4
        ip: 192.168.56.104
  tasks:
    - name: Include role 'windows_dnsserver'
      ansible.builtin.include_role:
        name: windows_dnsserver
</pre></code>
