# Example of role depending on another role

Example of how a role behaves differently depending on where it is defined collection vs playbook's role.

In every example, playbook uses role `enable_aur` which uses module provided by role: [kewlfft.aur](https://github.com/kewlfft/ansible-aur)
Two examples works using role `enable_aur` defined along with a particular playbook in `roles` directory
Two examples does NOT work, they use `enable_aur` which is provided by collection (`collection` directory)

There are 4 examples:
- playbook1 - works - using `enable_aur` directly; `enable_aur` declares dependency on `kewlfft.aur` in `roles/enable_aur/meta/main.yml`
- playbook2 - works - using `enable_aur` directly; `playbook.yml` uses role `kewlfft.aur` to provide aur module from kewlfft to be usable
- playbook3 - does NOT work - presents that when the role from playbook1 is moved to collection then playbook stop working
- playbook4 - does NOT work - tries to find workaround by using `kewlfft.aur` role in playbook.yml (like in playbook2)

## How to use collection - for playbook3 and playbook4 to run
First install collection:
- go to `collection` directory
- build collection
```
ansible-galaxy collection build
```
- install collection
```
ansible-galaxy collection install mynamespace-example-0.0.1.tar.gz
```

Then you can lunch any of playbook using this collection: playbook3, playbook4
