 ansible weechat role
==========================
Ansible role to install and configure weechat.

[![WEECHAT](https://weechat.org/media/images/weechat_logo_large.png)](https://weechat.org/)
<br/>WeeChat, the extensible chat client.

 What can this role:
-----------------
 - install weechat on Debian, Ubuntu, Archlinux or Fedora
 - ~~configure weechat~~ *(in progress)*
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
