# kanidm_vagrant_libvirt_ansible

This Vagrant setup creates a VM and installs [Kanidm](https://kanidm.com) on it.

It creates another VM and prepares the client tooling to connect to the Kanidm
server.

Default OS is openSUSE Tumbleweed. Although that can be changed in the
Vagrantfile, please beware that this will break the Ansible provisioning.

## Vagrant

1. You need vagrant obviously. And ansible. And git...
1. Fetch the box, per default this is `opensuse/Tumbleweed.x86_64`, using
   `vagrant box add opensuse/Tumbleweed.x86_64`.
1. Make sure the git submodules are fully working by issuing `git submodule init
   && git submodule update`
1. Run `vagrant up`
1. Run `vagrant ssh kanidm-client` to log into the Kanidm client VM.
1. Run `kanidm login --name idm_admin` to log in to the actual Kanidm server.
   Use the password that was printed out at the end of the Ansible provisioning.
   Ignore the warnings regarding the `verify_ca` setting, the setup is using
   self-signed certificates and hence is insecure. But for a demo setup this is
   actually alright.
1. Create a new account for `tux`:

   ```
   $ kanidm person create tux "Tux Penguin"
   2024-10-25T12:47:11.066302Z  WARN kanidm_client: verify_ca set to false in client configuration - this may allow network interception of passwords!
   Successfully created display_name="Tux Penguin" username=tux
   $ kanidm person credential create-reset-token tux
   [...]
   $
   ```

   The last command will print out a QR code, a link and a command. Use whatever
   suits you best to fully setup the user.  Even though this is a demo setup,
   Kanidm does not lower the bar and you need to create the account with a
   strong password.
1. Party!

## Cleaning up

The VMs can be torn down after playing around using `vagrant destroy`.

## License

BSD-3-Clause

## Author Information

I am Johannes Kastl, reachable via git@johannes-kastl.de
