These are the polices as used by Fedora and EPEL which should be usable in other selinux capable distributions.

Note that Fedora already has this in the base policy so does not need to build it in the spec file there.

For the EPEL builds EL7 uses the systemd one to correctly label unit files and EL5/6 use the sysvinit one.

The sslh daemon is restricted by default to the standard ports to connect to for http/https/openvpn/jabber

The sslh daemon is also restricted by default to only bind to tcp/443

There are two selinux booleans that tweak this sslh_can_connect_any_port and sslh_can_bind_any_port

To compile the policy install whichever package your distribution uses for /usr/share/selinux/devel

Then after entering the appropriate policy directory do:
```
make -f /usr/share/selinux/devel/Makefile
semodule -i sslh.pp
```

Remember to run restorecon/fixfiles on the files installed to get the correct contexts.
