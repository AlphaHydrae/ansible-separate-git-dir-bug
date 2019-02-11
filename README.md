# Ansible `separate_git_dir` bug

Running the `git` module with the `separate_git_dir` option fails and wipes out
the contents of the bare repository if the `dest` directory does not exist. It
works fine when both the `separate_git_dir` and the `dest` directories do not
exist, or when both already exist.

Issue: https://github.com/ansible/ansible/issues/52026

## Requirements

* [Vagrant](https://www.vagrantup.com/) 2.2.3
* [Ansible](https://www.ansible.com/) 2.7.6

## Usage

To reproduce the bug:

```bash
# Set up the virtual machine (will run the playbook once with no error)
git clone https://github.com/AlphaHydrae/ansible-separate-git-dir-bug
cd ansible-separate-git-dir-bug
vagrant up

# Run the playbook again (will produce the bug)
vagrant provision
```

To re-test:

```bash
# Clean up the directories and run the playbook twice
vagrant ssh -c 'sudo rm -fr /tmp/checkout /tmp/repo' && vagrant provision && vagrant provision
```
