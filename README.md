# Summary
This playbook is used to remove Avi pool members which are defined as FQDNs and are no longer resolveable.

High-Level Steps:
1. Search Avi logs to find FQDNs which are failing to resolve.
2. Find pools which are using the failed FQDN(s)
3. If the FQDN was found in a pool, list in flagged_fqdns.txt and display at the console. User is presented with a yes/no option of proceeding.
4. Playbook will loop through FQDNs, find all pools which use them, and remove the FQDN entry from the pool.

## Getting Started
This play is tested using specific versions of Ansible and makes use of libraries which are needed for playbooks to execute successfully. When developing your own automation, it is highly encouraged to make use of Python's virtual environments to avoid conflicts with other version of packages which may already be installed.

```
git clone https://github.com/joeycoakleyavi/Remove_Failed_FQDNs.git
cd Remove_Failed_FQDNs
python3 -m venv env
source env/bin/activate
pip3 install -r requirements.txt
ansible-galaxy collection install vmware.alb
```

You will need to adjust your controller variables in the `main.yml` playbook.

```
vars:
  avi_credentials:
    controller: 1.2.3.4
    username: admin
    password: SomethingSuperSecure
    api_version: 21.1.5
  duration: 600 #Time in seconds to search Avi logs for failed FQDN resolution
```

Once complete, you can run the playbook

`ansible-playbook main.yml`

## Tested Versions
This playbook has been tested on Avi version 21.1.5 running Ansible 2.13.4 and Python 3.9.7