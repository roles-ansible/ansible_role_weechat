[![Ansible Galaxy](https://ansible.l3d.space/svg/l3d.weechat.svg)](https://galaxy.ansible.com/l3d/weechat)
[![BSD-3 Clause](https://ansible.l3d.space/svg/l3d.weechat_license.svg)](LICENSE)
[![Maintainance](https://ansible.l3d.space/svg/l3d.weechat_maintainance.svg)](https://ansible.l3d.space/#l3d.weechat)

ansible weechat role
==========================
Ansible role to install and configure weechat.

[![WEECHAT](https://weechat.org/media/images/weechat_logo_large.png)](https://weechat.org/)
<br/>WeeChat, the extensible chat client.

 What can this role:
-----------------
 - install weechat on Debian, Ubuntu, Archlinux or Fedora
 - add configuration from private git repo
 - autostart via tmux and systemd

 Settings
----------

```yaml
 weechat__install: true
```
+ ``weechat__install: true``: This role should install weechat. On debian based OS we add the official weechat apt source and install some plugin support and weechat-doc.
+ ``weechat__install: false``: We do not install weechat

```yaml
weechat__autostart: false
```
+ ``weechat__autostart: false``: We do not install any autostart mechanism
+ ``weechat__autostart: true``: This role install tmux and creates a systemd service to launch weechat inside a tmux session as user ``{{ weechat__user }}``

```yaml
weechat__install_plugins: false
```
+ ``weechat__install_plugins: false``: we do not install any weechat plugins
+ ``weechat__install_plugins: true``: We do install all official plugins specified in ``{{ weecat.plugins }}`` dict.

```yaml
weechat__use_custom_config: false
```
+ ``weechat__use_custom_config: false``: You do not provide a custom config from your own git repository
+ ``weechat__use_custom_config: true``: You have your weechat configuration in a own git repository and want to use it

```yaml
weechat__install_plugins: false
```
+ ``weechat__install_plugins: false`` we do not install any official weechat plugins
+ ``weechat__install_plugins: true`` we install the official weechat plugins defined in the ``{{ weechat__plugins: [] }}`` directory.

```yaml
weechat__plugins:
 - go.py
 - iset.pl
```
+ Example ``weechat__plugins: []`` list

```yaml
weechat__user: "{{ ansible_user_id }}"
```
+ the user to use weechat with. This value is used in the ``autostart`` task, the ``custom_config`` task and the ``{{ weechat__home_directory }}`` variable

```yaml
weechat__home_directory: "{{ ansible_env.HOME | default('/home/{{ weechat__user }}') }}"
```
+ the path where the weechat home is located. If the variable ``{{ ansible_env.HOME }}`` is not set it will use ``"/home/{{ weechat__user }}"`` as fallback.

```yaml
weechat__gpg_id: '11E9DE8848F2B65222AA75B8D1820DB22A11534E'
```
+ This is the gpg fingerprint from the [official weechat debian repo](https://weechat.org/download/debian/)

```yaml
weechat__custom_private_repo: false
```
+ The path to your git repo with your personal weechat config.
+ This role clones the repo to the ``"{{ weechat__home_directory }}/.weechat"`` directory. *(Also known al your local .weechat directory.)* It will fail if you already have files and/or folders in your local .weechat dorectory.
+ You have to add, commit and push the local changes in your local .weechat folder manually. Please be aware that it is a good idea to disable your log or at least add the weechatlog folder to your .gitignore file in your personal weechat config.

```yaml
weechat__custom_gen_ssh_key_pair: true
```
+ ``weechat__custom_gen_ssh_key_pair: true``: We will generate a eleptic curve ssh key *(if it not already exist at ``"{{ weechat__home_directory }}/.ssh/id_ed25519"``)* and print the public key to the prompt. This will give you the time to add this public key to your private git repo for your own weechat config as deploy key. This is required to download your private repo withour username/password. This requires that you set ``{{ weechat__custom_private_repo }}`` to the ssh accessable version of your git repo.
+ ``weechat__custom_gen_ssh_key_pair: false``: We do not manage access to the git repo with your weechat config.

```yaml
weechat__custom_version: main
```
+ ``weechat__custom_version: main``: set the git branch, tag, hash or version this role should use if you use a custom git repo for your weechat config.


 References and Inspiration:
----------------------
 + Information about installation on debian/ubuntu can be found at [weechat.org/download/debian](https://weechat.org/download/debian/)
 + Some parts of the Weechat configuration is inspired by [github.com/irth/ansible-role-weechat](https://github.com/irth/ansible-role-weechat.git) but written in a complete different way. Some other is completly different.
 + Autostart and systemd is inspired by [ubuntu wiki](https://wiki.ubuntuusers.de/Howto/systemd_Service_Unit_Beispiel/) and [ansible docs](https://docs.ansible.com/ansible/latest/modules/systemd_module.html).

## Requirements
The ``community.general`` and ``community.crypto`` collections are required for some parts of this ansible role.
You can install it with this command:
```bash
ansible-galaxy collection install -r requirements.yml --upgrade
```
 Contribute
------------
If you missing a feature, found a bug or have questions about this role please feel free to open a git issue. Or - even better - create a pull request.

 LICENSE
----------
[![MIT License](https://ansible.l3d.space/svg/l3d.weechat_license.svg)](LICENSE)
```
Copyright (c) 2019 L3D <l3d@c3woc.de>
```
*The complete list of awesome contributros can be found [here](https://github.com/chaos-bodensee/role_weechat/graphs/contributors).*
