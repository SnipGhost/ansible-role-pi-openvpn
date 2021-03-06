OpenVPN
=========

This role install and configure OpenVPN in a Raspberry Pi.

Requirements
------------

This role requires Ansible 2.0 or higher and a clean installation of RaspberryPi OS.

Role Variables
--------------

The variables that can be passed to this role and a brief description about
them are as follows.

([defaults/main.yml](defaults/main.yml))

```yaml
---
# Certificate options
easyrsa_key_size: 1024             # Prefered to use 2048
easyrsa_req_country: "RU"          # Country Name (2 letter code)
easyrsa_req_province: "Moscow"     # State or Province Name (full name)
easyrsa_req_city: "Moscow"         # Locality Name (eg, city)
easyrsa_req_org: "ACME Ltd."       # Organization Name (eg, company)
easyrsa_req_email: "a@example.org" # Email Address
easyrsa_req_ou: "DevOps"           # Organizational Unit Name (eg, section)
easyrsa_common_name: "example.org" # Common name (eg, CN, hostname)

easyrsa_algo: ec          # Algorithm: rsa or ec
easyrsa_digest: sha512    # md5, sha1, sha256, sha224, sha512

# OpenVPN server binding
openvpn_protocol: udp     # UDP is recommended. You can change fot TCP
openvpn_port: 1194        # This is the default OpenVPN port

# Virtial network
openvpn_server_subnet: 10.8.0.0       # The subnet you want to use for the OpenVPN clients
openvpn_server_netmask: 255.255.255.0 # The netmask for the OpenVPN client subnet
openvpn_server_tun0: 10.8.0.1         # The IP for the OpenVPN tunnel interface
openvpn_server_tun0_ptp: 10.8.0.2     # The IP for the OpenVPN tunnel point-to-point alias

# Real network
openvpn_local_address: "{{ ansible_default_ipv4['address'] }}" # The default local IP address
openvpn_local_subnet: "{{ ansible_default_ipv4['network'] }}"  # The local subnet where the Raspberry Pi is connected
openvpn_local_netmask: "{{ ansible_default_ipv4['netmask'] }}" # The local netmask for the Raspberry Pi subnet
openvpn_interface: "{{ ansible_default_ipv4['interface'] }}"   # The local interface for the Raspberry Pi
openvpn_dns_ip: 192.168.0.1 # If your router does not do DNS, you can use Google DNS 8.8.8.8

# OpenVPN clients list
openvpn_clients:
  - username: ""

# Add firewall-openvpn-rules.sh to iface config
openvpn_add_rules_script: yes
```

Dependencies
------------

None

Example Playbook
----------------

If you encrypt the credentials.yml file, remember to run your playbook with the flag '--ask-vault-pass'.

    - hosts: pi
      role: openvpn

License
-------

MIT

Author Information
------------------

* [Mikhail Kucherenko](https://github.com/SnipGhost)
