# PubNub Ansible Role Python SDK

Install PubNub's Python SDK Tools and it's dependencies in MacOS using Ansible.

## Pre-Requisites

Install the following packages:

* Ansible
* Homebrew

## Setup

Create your `inventory` file with your target's username and password. For a local installation:

```ini
[local]
localhost ansible_user=username ansible_become_password=password
```

Modify your `group_vars` file if needed:

```yml
global_hosts: local  # host group to use
virtual_env_path: /home/username/pubnub_directory  # venv target folder
pypi_repository_url: https://test.pypi.org/simple  # currently only in test.pypi
pubnub_subscribe_key: # pubnub credentials (preferebly in encrypted vault)
pubnub_publish_key: # pubnub credentials (preferebly in encrypted vault)
pubnub_user_id: # pubnub credentials (preferebly in encrypted vault)
```

## Usage

To run everything:

```shell
$ ansible-playbook pubnub_mgmt.yml -i inventory -e "@group_vars/local.yml" -t deploy
```

> Pass your Vaulted keyset with --vault_id "your_vault_id"

### Role Tags

### Install Python MacOS

Install python and dependencies using homebrew.

__Role Sample Use:__

```shell
$ ansible-playbook pubnub_mgmt.yml -i inventory -e "@group_vars/local.yml" -t install-python-macos
```

__Role Tags:__
 - install
 - install-python-macos
 - deploy

### Install PubNub Python Tools

Install [pubnub-python-tools](https://github.com/sergio-munoz/pubnub-python-tools) from test.pypi.org.

__Role Sample Use:__

```shell
$ ansible-playbook pubnub_mgmt.yml -i inventory -e "@group_vars/local.yml" -t install-pip
```

__Role Tags:__

- pip
- install-pip
- deploy

### Setup PubNub Config

Sets up your PubNub keys in an `.env` file and to environment variable.

```shell
$ ansible-playbook pubnub_mgmt.yml -i inventory -e "@group_vars/local.yml" -t config
```

__Role Tags:__

- config
- pubnub-config
- deploy

__Role Variables:__

- pubnub_env_file: `${ ansible.env.HOME }`
- pubnub_publish_key:
- pubnub_subscribe_key:
- pubnub_user_id:

#### Config PubNub variables using Vault

A vault can be used to keep sensitive data in an encrypted form in playbooks or roles, rather than in plaintext. The vault password can be stored in plaintext in a file, for example `vault_pass.txt` containing `pubnub_subscribe_key`, to be used later on as a command parameter:

```shell
$ ansible-playbook pubnub_mgmt.yml --vault-id vault_pass.txt
```

In order to encrypt the content the var content of a variable named `pubnub_subscribe_key` using the password stored in `vault_pass.txt`, the following command should be used:

```shell
$ ansible-vault encrypt_string --vault-id vault_pass.txt 'sub-c-xxxxxxxx-xxxx' --name pubnub_subscribe_key
```

More securely, to avoid inputting the variable content in the command line and be prompted for it instead, one can use:

```shell
$ ansible-vault encrypt_string --vault-id vault_pass.txt --stdin-name pubnub_subscribe_key

Reading plaintext input from stdin. (ctrl-d to end input)
sub-c-xxxxxxxx-xxxx (ctrl-d)
```
