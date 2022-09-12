Role Name
=========

Install PubNub's Python SDK and pubnub-python-tools in MacOS.

Requirements
------------

Use your PubNub credentials.

Role Variables
--------------

- `virtualenv_path` - target virtual environment path
- `pypi_repository_url` - pypi url repository to use
- `requirements_txt` - use a requirements.txt file
- `pubnub_env_key` - target environment variable file path
- `pubnub_subscribe_key` - PubNub subscribe key
- `pubnub_publish_key` - PubNub publish key
- `pubnub_user_id` - PubNub instance user id

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: local
      roles:
         - { role: python-role } 

Example Run
-----------

ansible-playbook -i inventory playbook.yml -t deploy

License
-------

MIT

Author Information
------------------

https://github.com/sergio-munoz:w

