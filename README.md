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
