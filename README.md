# ansible-role-servermonkey-sh

Run shellscripts as Ansible task witout the need to write a playbook or task
file. This replaces the need to use the Ansible shell module and write more
complex shell scripts inside a playbook.

Automatically uses the
role https://github.com/ServerMonkey/ansible-role-servermonkey-ww-logger/

## Usage

Automatically detects if you want to run a script as superuser. Just add the
line '#autoroot' into your scripts header and Ansible will always execute the
script as root / become user. No need to run ansible shellscripts with "become:
true"

Example shell script:

```
#!/bin/sh
#info: Print a message as superuser
#autoroot

# must run as root
if [ "$(id -u)" -ne 0 ]; then
    echo 'This script must be run as root!' >&2
    exit 1
fi

echo Hello World
```

Example tasks:

```
- include_role: name=servermonkey.sh
  vars:
      sh: '{{ script_file_name }}'
```

```
- include_role: name=servermonkey.sh
  vars:
      sh_script_path: '{{ path_to_script_folder }}'
      sh: '{{ script_file_name }}'
      sh_arg: '{{ script_argument }}'
```
