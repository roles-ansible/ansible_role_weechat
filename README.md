[![Ansible Galaxy](https://raw.githubusercontent.com/chaos-bodensee/role_weechat/master/.github/galaxy.svg?sanitize=true)](https://galaxy.ansible.com/do1jlr/weechat) [![Build Status](https://travis-ci.org/chaos-bodensee/role_weechat.svg?branch=master)](https://travis-ci.org/chaos-bodensee/role_weechat) [![MIT License](https://raw.githubusercontent.com/chaos-bodensee/role_weechat/master/.github/license.svg?sanitize=true)](https://github.com/chaos-bodensee/role_weechat/blob/master/LICENSE)

ansible weechat role
==========================
Ansible role to install and configure weechat.

[![WEECHAT](https://weechat.org/media/images/weechat_logo_large.png)](https://weechat.org/)
<br/>WeeChat, the extensible chat client.

 What can this role:
-----------------
 - install weechat on Debian, Ubuntu, Archlinux or Fedora
 - configure weechat
 - autostart via tmux and systemd

 Settings
----------

```yaml
 weechat:
    install: true
```
+ ``weechat.install: true``: This role should install weechat. On debian based OS we add the official weechat apt source and install some plugin support and weechat-doc.
+ ``weechat.install: false``: We do not install weechat

```yaml
weechat:
    autostart: false
```
+ ``weechat.autostart: false``: We do not install any autostart mechanism
+ ``weechat.autostart: true``: This role install tmux and creates a systemd service to launch weechat inside a tmux session as user ``{{ weechat.user }}``

```yaml
weechat:
  install_plugins: false
```
+ ``weechat.install_plugins: false``: we do not install any weechat plugins
+ ``weechat.install_plugins: true``: We do install all official plugins specified in ``{{ weecat.plugins }}`` dict.

```yaml
weechat:
  use_custom_config: false
```
+ ``weechat.use_custom_config: false``: You do not provide a custom config from your own git repository
+ ``weechat.use_custom_config: true``: You have your weechat configuration in a own git repository and want to use it

```yaml
weechat:
  install_plugins: false
```
+ ``weechat.install_plugins: false`` we do not install any official weechat plugins
+ ``weechat.install_plugins: true`` we install the official weechat plugins defined in the ``{{ weechat.plugins: [] }}`` directory.

```yaml
weechat:
  plugins:
    - go.py
    - iset.pl
```
+ Example ``weechat.plugins: []`` list

```yaml
weechat:
  user: "{{ ansible_user_id }}"
```
+ the user to use weechat with. This value is used in the ``autostart`` task, the ``custom_config`` task and the ``{{ weechat.home_directory }}`` variable

```yaml
weechat:
  home_directory: "{{ ansible_env.HOME | default('/home/{{ weechat.user }}') }}"
```
+ the path where the weechat home is located. If the variable ``{{ ansible_env.HOME }}`` is not set it will use ``"/home/{{ weechat.user }}"`` as fallback.

```yaml
weechat:
  gpg_id: '11E9DE8848F2B65222AA75B8D1820DB22A11534E'
```
+ This is the gpg fingerprint from the [official weechat debian repo](https://weechat.org/download/debian/)

```yaml
weechat:
  custom_config:
    private_repo: false
```
+ The path to your git repo with your personal weechat config.
+ This role clones the repo to the ``"{{ weechat.home_directory }}/.weechat"`` directory. *(Also known al your local .weechat directory.)* It will fail if you already have files and/or folders in your local .weechat dorectory.
+ You have to add, commit and push the local changes in your local .weechat folder manually. Please be aware that it is a good idea to disable your log or at least add the weechatlog folder to your .gitignore file in your personal weechat config.

```yaml
weechat:
  custom_config:
    gen_ssh_key_pair: true
```
+ ``weechat.custom_config.gen_ssh_key_pair: true``: We will generate a eleptic curve ssh key *(if it not already exist at ``"{{ weechat.home_directory }}/.ssh/id_ed25519"``)* and print the public key to the prompt. This will give you the time to add this public key to your private git repo for your own weechat config as deploy key. This is required to download your private repo withour username/password. This requires that you set ``{{ weechat.custom_config.private_repo }}`` to the ssh accessable version of your git repo.
+ ``weechat.custom_config.gen_ssh_key_pair: false``: We do not manage access to the git repo with your weechat config.

```txt
WARNING

It is work-in-progress. Be careful!

MISSING
- all task for configurations
- testing for all OS
- improved docs
- galaxy
```

 References and Inspiration:
----------------------
 + Information about installation on debian/ubuntu can be found at [weechat.org/download/debian](https://weechat.org/download/debian/)
 + Some parts of the Weechat configuration is inspired by [github.com/irth/ansible-role-weechat](https://github.com/irth/ansible-role-weechat.git) but written in a complete different way. Some other is completly different.
 + Autostart and systemd is inspired by [ubuntu wiki](https://wiki.ubuntuusers.de/Howto/systemd_Service_Unit_Beispiel/) and [ansible docs](https://docs.ansible.com/ansible/latest/modules/systemd_module.html).

 Contribute
------------
If you missing a feature, found a bug or have questions about this role please feel free to open a git issue. Or - even better - create a pull request.

 LICENSE
----------
[MIT License](https://github.com/chaos-bodensee/role_weechat/blob/master/LICENSE)<br/>
+ ``Copyright (c) 2019 L3D``
+  The complete list of awesome contributros can be found [here](https://github.com/chaos-bodensee/role_weechat/graphs/contributors).


### testing
This role is tested with [these github-action](https://github.com/search?q=topic%3Acheck-ansible+topic%3Agithub-actions+org%3Aroles-ansible&type=Repositories) tests for different versions of differen linux systems. Linting is tested via travis-ci and the  [ansible-lint action](https://github.com/marketplace/actions/ansible-lint).
If you want to find out more about our tests, please have a look at the github marketplace.

| test status | Github Marketplace |
| :---------  | :----------------  |
| [![Travis Build Status](https://travis-ci.org/chaos-bodensee/role_weechat.svg?branch=master)](https://travis-ci.org/chaos-bodensee/role_weechat) | [.travis.yml](https://github.com/chaos-bodensee/role_weechat/blob/master/.travis.yml) |
|||
| [![Ansible Lint check](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20Lint%20check/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+Lint+check%22) | [ansible-lint action](https://github.com/marketplace/actions/ansible-lint)
| [![Ansible check debian:stable](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20debian:stable/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+debian%3Astable%22) | [ansible test with debian stable](https://github.com/marketplace/actions/check-ansible-debian-stable) |
| [![Ansible check debian:latest](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20debian:latest/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+debian%3Alatest%22) | [ansible test with debian latest](https://github.com/marketplace/actions/check-ansible-debian-latest) |
| [![Ansible check debian:sid](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20debian:sid/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+debian%3Asid%22) | [ansible test with debian sid](https://github.com/marketplace/actions/check-ansible-debian-sid) |
| [![Ansible check debian:buster](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20debian:buster/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+debian%3Abuster%22) | [ansible test with debian buster](https://github.com/marketplace/actions/check-ansible-debian-buster) |
| [![Ansible check debian:stretch](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20debian:stretch/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+debian%3Astretch%22) | [ansible test with debian stretch](https://github.com/marketplace/actions/check-ansible-debian-stretch) |
| | |
| [![Ansible check archlinux:latest](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20archlinux:latest/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+archlinux%3Alatest%22) | [ansible test with archlinux latest](https://github.com/marketplace/actions/check-ansible-archlinux-latest) |
| | |
| [![Ansible check ubuntu:latest](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20ubuntu:latest/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+ubuntu%3Alatest%22) | [ansible test with ubuntu latest](https://github.com/marketplace/actions/check-ansible-ubuntu-latest) |
| [![Ansible check ubuntu:bionic](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20ubuntu:bionic/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+ubuntu%3Abionic%22) | [ansible test with ubuntu bionic](https://github.com/marketplace/actions/check-ansible-ubuntu-bionic) |
| [![Ansible check ubuntu:eoan](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20ubuntu:eoan/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+ubuntu%3Aeoan%22) | [ansible test with ubuntu eoan](https://github.com/marketplace/actions/check-ansible-ubuntu-eoan) |
| [![Ansible check ubuntu:trusty](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20ubuntu:trusty/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+ubuntu%3Atrusty%22) | [ansible test with ubuntu trusty](https://github.com/marketplace/actions/check-ansible-ubuntu-trusty) |
| | |
| [![Ansible check fedora:latest](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20fedora:latest/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+fedora%3Alatest%22) | [ansible test with fedora latest](https://github.com/marketplace/actions/check-ansible-fedora-latest) |
| [![Ansible check fedora:33](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20fedora:33/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+fedora%3A33%22) | [ansible test with fedora 33](https://github.com/marketplace/actions/check-ansible-fedora-33) |
| [![Ansible check fedora:32](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20fedora:32/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+fedora%3A32%22) | [ansible test with fedora 32](https://github.com/marketplace/actions/check-ansible-fedora-32) |
| [![Ansible check fedora:31](https://github.com/chaos-bodensee/role_weechat/workflows/Ansible%20check%20fedora:31/badge.svg)](https://github.com/chaos-bodensee/role_weechat/actions?query=workflow%3A%22Ansible+check+fedora%3A31%22) | [ansible test with fedora 31](https://github.com/marketplace/actions/check-ansible-fedora-31) |

