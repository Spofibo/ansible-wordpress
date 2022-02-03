# Welcome to ansible-wordpress 👋
[![Documentation](https://img.shields.io/badge/documentation-yes-brightgreen.svg)](https://github.com/spofibo/ansible-wordpress#readme)
![Prerequisite](https://img.shields.io/badge/ansible-%3E%3D2.11.6-blue.svg)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/spofibo/ansible-wordpress/graphs/commit-activity)
[![License: AGPL-3.0-or-later](https://img.shields.io/github/license/spofibo/ansible-wordpress)](https://github.com/spofibo/ansible-wordpress/blob/master/LICENSE)

> Ansible playbook to deploy one or more Wordpress instances.

It installs and configures Nginx, PHP 8.1, and Certbot for the SSL certificates.
This playbook **does not** install the database service, and instead it expects variables to connect to a remote database.

## Requirements
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [Cloudflare API token](https://developers.cloudflare.com/api/tokens/create) for the sites you want to manage

### Local testing
- [Virtualbox](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](https://www.vagrantup.com/downloads)

## Usage

* Copy `vars.example` to `vars.yaml` and update the configuration paramaters
* Copy `inventory.example` to `inventory` and update the `servers` section to figure your targeted servers
* Run

```sh
ansible-playbook -i inventory playbook.yaml
```

### Local Testing

For a complete run:

```sh
vagrant up
```

Targeting specific vars
```sh
vagrant --tags=nginx up
```

Main available tags
- system
- php
- nginx
- certbot
- wordpress

## Author

👤 **Alex Budurovici**

* Website: w0rldart.com
* Github: [@w0rldart](https://github.com/w0rldart)

## 🤝 Contributing

Contributions, issues and feature requests are welcome!

Feel free to check [issues page](https://github.com/Spofibo/ansible-wordpress/issues). You can also take a look at the [contributing guide](https://github.com/spofibo/ansible-wordpress/blob/master/CONTRIBUTING.md).

## Show your support

Give a ⭐️ if this project helped you!


## 📝 License

Copyright © 2022 [Alex Budurovici](https://github.com/w0rldart).

This project is [AGPL--3.0](https://github.com/spofibo/ansible-wordpress/blob/master/LICENSE) licensed.

***
_This README was generated with ❤️ by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_
