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
+ ``install: true``: This role should install weechat. On debian based OS we add the official weechat apt source and install some plugin support and weechat-doc.
+ ``install: false``: We do not install weechat

```yaml 
weechat:
    autostart: false
```
+ ``autostart: false``: We do not install any autostart mechanism
+ ``autostart: true``: This role install tmux and creates a systemd service to launch weechat inside a tmux session as user ``{{ weechat.user }}``

```yaml
weechat:
  install_plugins: false
```
+ ``install_plugins: false``: we do not install any weechat plugins
+ ``install_plugins: true``: We do install all official plugins specified in ``{{ weecat.plugins }}`` dict.

```yaml
weechat:
  use_custom_config: false
```

   7   │   # should we install official weechat plugins
   8   │   install_plugins: false
   9   │   # custom weechat config (requires some manual interaction for long-term usage)
  10   │   custom
  11   │   # user to install and use weechat
  12   │   user: "{{ ansible_user_id }}"
  13   │   # where is our home direcotory for weechat
  14   │   home_directory: "{{ ansible_env.HOME | default('/home/{{ weechat.user }}') }}/.weechat"
  15   │   # plugins we want
  16   │   plugins: []
  17   │   # weechat gpg key for debian/ubuntu repo
  18   │   gpg_id: '11E9DE8848F2B65222AA75B8D1820DB22A11534E'
  19   │   # custom private config
  20   │   costom_config:
  21   │     # path to your custom weechat config (with plugins) git repo ( git@github.com:<your_name>/<your_weechat_config_repo>.git )
  22   │     private_repo: false
  23   │     # generate ssh key pair (if not available)
  24   │     gen_ssh_key_pair: true



```txt
WARNING

It is work-in-progress. Be careful!

MISSING
- task for configurations
- testing for all OS
- docs
- galaxy
```

 References and Inspiration:
----------------------
 + Information about installation on debian/ubuntu can be found at [weechat.org/download/debian](https://weechat.org/download/debian/)
 + Some parts of the Weechat configuration is inspired by [github.com/irth/ansible-role-weechat](https://github.com/irth/ansible-role-weechat.git) but written in a complete different way.
 + Autostart and systemd is inspired by [ubuntu wiki](https://wiki.ubuntuusers.de/Howto/systemd_Service_Unit_Beispiel/) and [ansible docs](https://docs.ansible.com/ansible/latest/modules/systemd_module.html).
