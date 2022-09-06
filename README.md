# ansible-role-servermonkey-sh

A different way to run shellscripts as Ansible task.

## Usage

Automatically detects if you want to run a script as root.  
Just add the line '#autoroot' into your scripts header and Ansible will always execute the script as root / become user.  
No need to run ansible schellscripts with "become: true"

Example script:

```
#!/bin/sh
#info: Print hello world
#autoroot

# must run as root
if [ "$(id -u)" -ne 0 ]; then
    echo 'This script must be run as root!' >&2
    exit 1
fi

echo "Hello World"
```