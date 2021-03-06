# Ansible Letsecrypt

[![Stack](https://raw.githubusercontent.com/paralect/stack/master/stack-component-template/stack.png)](https://github.com/paralect/stack)

[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-letsenctypt-blue.svg?style=flat-square)](https://galaxy.ansible.com/paralect/drone)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square)](https://github.com/paralect/ansible-mongo/blob/master/LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)


[![Watch on GitHub](https://img.shields.io/github/watchers/paralect/ansible-letsectrypt.svg?style=social&label=Watch)](https://github.com/paralect/ansible-letsectrypt/watchers)
[![Star on GitHub](https://img.shields.io/github/stars/paralect/ansible-letsectrypt.svg?style=social&label=Stars)](https://github.com/paralect/ansible-letsectrypt/stargazers)
[![Follow](https://img.shields.io/twitter/follow/paralect.svg?style=social&label=Follow)](https://twitter.com/paralect)
[![Tweet](https://img.shields.io/twitter/url/https/github.com/paralect/ansible-letsectrypt.svg?style=social)](https://twitter.com/intent/tweet?text=I%27m%20using%20Stack%20components%20to%20build%20my%20next%20product%20🚀.%20Check%20it%20out:%20https://github.com/paralect/ansible-letsectrypt)

The ansible role for generating [letsecrypt](https://letsencrypt.org/) certificates.

## Features

* 🔐 Ability to generate single certificates for specific domains/subdomains
* 🔐 Ability to generate wildcard certificates using settings for the corresponding DNS provider
* ⚡️️ Automatically renew certificates every month
* 🔧 Generated certificates stored in the directory `/etc/letsencrypt/live/{{app_domain}}` where `app_domain` is the name of domain/subdomain for which we generated certificates and ready for use with any HTTP-server

## Role Variables

Available variables:

|Name|Default|Description|
|:--:|:--:|:----------|
|**`use_dns_plugin`**|`false`|Use certbot dns provider (use this if you need wildcard sertificate) or certbot itselt.|
|**`certbot_version`**|`latest`|# Version of certbot or certbot dns plugin (if `use_dns_plugin` is `true`), see other versions [here](https://hub.docker.com/r/certbot/certbot/tags)|
|**`dns_plugin`**|`cloudflare`|Dsn plugin that will be used with certbot (when `use_dns_plugin` is `true`), list of plugins can be found [here](https://certbot.eff.org/docs/using.html#dns-plugins)|
|**`email`**|`Email that will be used for notifications`|Email that will be used for notifications|
|**`domains_list`**|`- "{{ ansible_fqdn }}"`|List of domain for which you want to get a certificates|
|**`dns_email`**|`""`|DNS email (used for Cloudflare, LuaDNS)|
|**`dns_api_key`**|`""`|DNS api key (used for Cloudflare, CloudXNS, DNS Made Easy, NS1)|
|**`dns_secret_key`**|`""`|DNS secret key (used for CloudXNS, DNS Made Easy)|
|**`dns_token`**|`""`|DNS token (used for DigitalOcean, DNSimple, LuaDNS)|
|**`dns_key`**|`""`|DNS key (used for Linode)|
|**`dns_endpoint`**|`""`|DNS endpoint (used for OVH)|
|**`dns_application_key`**|`""`|DNS application key (used for OVH)|
|**`dns_application_secret`**|`""`|DNS application secret (used for OVH)|
|**`dns_consumer_key`**|`""`|DNS consumer key (used for OVH)|
|**`dns_server`**|`""`|Target DNS server (used for RFC 2136)|
|**`dns_port`**|`""`|Target DNS port (used for RFC 2136)|
|**`dns_name`**|`""`|TSIG key name (used for RFC 2136)|
|**`dns_secret`**|`""`|TSIG key secret (used for RFC 2136)|
|**`dns_algorithm`**|`""`|TSIG key algorithm (used for RFC 2136)|
|**`dns_access_key_id`**|`""`|DNS access key id (used for route 53)|
|**`dns_secret_access_key`**|`""`|DNS secret access key id (used for route 53)|

## Dependencies

[Docker](https://www.docker.com/) must be installed on the server in order to use this role. If you don't have docker on your server we recommend [angstwad.docker_ubuntu](https://github.com/angstwad/docker.ubuntu) Ansible role.

Example of using `angstwad.docker_ubuntu`:
```yml
---
- name: Setup server
  hosts: server
  become: true
  roles:
    - { role: angstwad.docker_ubuntu }
```

## Quick example

Example of the playbook file:

```yml
---
- name: Setup server
  hosts: server
  become: true
  roles:
    - role: paralect.letsencrypt
      use_dns_plugin: true
      certbot_version: v0.26.1
      dns_plugin: cloudflare
      email: ship@test.com
      domains_list:
        - "*.ship.com"
      dns_email: ship_dns@test.com
      dns_api_key: 0123456789abcdef0123456789abcdef01234567
```

## Change Log

This project adheres to [Semantic Versioning](http://semver.org/).
Every release is documented on the Github [Releases](https://github.com/paralect/node-letsencrypt/releases) page.

## License

Ansible-letsencrypt is released under the [MIT License](https://github.com/paralect/ansible-letsencrypt/blob/master/LICENSE).

## Contributing

Please read [CONTRIBUTING.md](https://github.com/paralect/ansible-letsencrypt/blob/master/CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
| [<img src="https://avatars2.githubusercontent.com/u/6461311?v=4" width="100px;"/><br /><sub><b>Evgeny Zhivitsa</b></sub>](https://github.com/ezhivitsa)<br />[📖](https://github.com/paralect/ansible-letsencrypt/commits?author=ezhivitsa "Documentation") [🤔](#ideas-ezhivitsa "Ideas, Planning, & Feedback") [💻](https://github.com/paralect/ansible-letsencrypt/commits?author=ezhivitsa "Code") | [<img src="https://avatars3.githubusercontent.com/u/681396?v=4" width="100px;"/><br /><sub><b>Andrew Orsich</b></sub>](https://github.com/anorsich)<br />[🤔](#ideas-anorsich "Ideas, Planning, & Feedback") [👀](#review-anorsich "Reviewed Pull Requests") |
| :---: | :---: |
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification. Contributions of any kind welcome!
