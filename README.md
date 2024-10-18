# macos-bootstrap

Quick bootstrap for new MacOS if for some reason a Time Machine / transfer isn't desirable.

## Bootstrap

This file will install HomeBrew, then use HomeBrew to install Ansible.

```bash
./bootstrap.sh
```

The bootstrap script will then run the `macos-setup-playbook.yaml` playbook on `localhost` to set up MacOS.  The playbook has two lists of packages to install:

- `brew_packages` - generic CLI/binary style packages
- `brew_cask_packages` - MacOS GUI packages (may have supplemental packages in `brew_packages`)

Edit those to your liking.

It will also generate the `localhost` inventory file, which is dynamic only because the `username` field is a requirement, and we don't want to run this as `root`.

## Post-Bootstrap/Maintenance

If you've already bootstrapped the box, just re-run the playbook after making tweaks.  A re-run without any edits will just update HomeBrew and upgrade the packages.

```bash
ansible-playbook -i localhost macos-setup-playbook.yml
```

***TODO***

cron?
isolate the packages into a var file which can better document them, especially if their names are not obvious (e.g. `code-cli`).
