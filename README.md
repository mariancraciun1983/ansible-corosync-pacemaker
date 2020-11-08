<h1 align="center">Pacemaker and Corosync cluster ansible role</h1>
<br />

<div align="center">
  <a href="https://travis-ci.com/mariancraciun1983/ansible-corosync-pacemaker">
    <img src="https://travis-ci.com/mariancraciun1983/ansible-corosync-pacemaker.svg?branch=master" alt="Build Status" />
  </a>
  <a href="https://galaxy.ansible.com/mariancraciun1983/corosync_pacemaker">
    <img src="https://img.shields.io/ansible/role/51695" alt="Ansible Galaxy" />
  </a>
  <a href="https://galaxy.ansible.com/mariancraciun1983/corosync_pacemaker">
    <img src="https://img.shields.io/ansible/quality/51695" alt="Ansible Quality Score" />
  </a>
  <a href="https://opensource.org/licenses/MIT">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="MIT License" />
  </a>
</div>
<br />

Ansible role to install and configure a cluster with Corosync and Pacemaker

## Introduction

Pacemaker and Corosync is one of the mostly used high availability cluster stack.
Pacemaker/Corosync Configuration System on the other hand is a tool to easily configure both Pacemaker and Corosync.


### Ansible
This role was tested against Ansible version 2.8 2.9 2.10 .
The supported platforms are
  - Ubuntu
    - focal
    - bionic

Mixing different distros might end up with different package versions being installed. It is strongly recommended to use a single version across all cluster.
For example focal comes with corosync 3.0, while bionic with version 2.4

## Variables
Configuration example
```yaml
group_vars:
  all:
    corosync_hacluster_password: 1q2w3e4r5t
    corosync_cluster_settings:
      - key: stonith-enabled
        value: "false"
      - key: no-quorum-policy
        value: ignore
      - key: start-failure-is-fatal
        value: "false"
      - key: symmetric-cluster
        value: "false"
    corosync_cluster_defaults:
      - key: resource-stickiness
        value: 100
```

If you want to use an internal network
```yaml
group_vars:
  all:
    corosync_use_internal_ip: true
host_vars:
  node1:
    internal_ip: 10.0.0.1
  node2:
    internal_ip: 10.0.0.2
  node3:
    internal_ip: 10.0.0.3
```

## Testing

Molecule with docker is being used.

Running the tests:
```bash
pipenv install
pipenv run molecule test
```