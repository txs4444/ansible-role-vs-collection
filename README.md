# Example of collection role depending on another role

In all examples playbooks uses role enable_aur which uses [kewlfft.aur](https://github.com/kewlfft/ansible-aur) (role providing module aur)
Two workings examples (playbook1 and playbook2) uses role enable_aur defined along with playbook in `roles` directory
Two does not work, they use enable_aur which is provided by collection (`collection` dirrectory)

There are 4 examples (2 use role directly and works, and 2 use role via collection and don't work):
- playbook1 - works - using enable_aur directly; enable_aur defineds dependency on kewlfft.aur in `roles/enable_aur/meta/main.yml`
- playbook2 - works - using enable_aur directly; `playbook.yml` uses role kewlfft.aur to provide aur module from kewlfft to be usable
- playbook3 - does NOT work - presents that when role from playbook1 is moved to collection and playbook stop working
- playbook4 - does NOT work - tries to find workaround by using kewlfft.aur role in playbook.yml (like in playbook2)

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
