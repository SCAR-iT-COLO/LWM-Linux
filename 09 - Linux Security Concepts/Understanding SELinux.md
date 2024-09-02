# Understanding SELinux

## 1. Introduction to SELinux

SELinux is a mandatory access control (MAC) security mechanism implemented in the Linux kernel. Developed by the NSA and Red Hat, it provides an additional layer of system security to complement the traditional discretionary access control (DAC) model used in most Linux distributions.

Key concepts:
- Mandatory Access Control (MAC)
- Security policies
- Security contexts
- Access decisions based on security contexts

## 2. SELinux Modes

SELinux operates in three modes:
- Enforcing: SELinux policy is enforced
- Permissive: SELinux prints warnings but does not enforce policy
- Disabled: SELinux is turned off

To check the current mode:
```
getenforce
```

To change modes temporarily:
```bash
setenforce 0 # Set to permissive
```
```bash
setenforce 1 # Set to enforcing
```

To change modes permanently, edit /etc/selinux/config and reboot.

## 3. SELinux Contexts

SELinux assigns a context to every process, file, and system object. A context consists of four fields:
user:role:type:level

Example:
```
system_u:object_r:httpd_sys_content_t:s0
```

To view contexts:
```
ls -Z # For files
ps auxZ # For processes
```

## 4. SELinux Policies

SELinux uses policies to define allowed actions. Two main policy types:
- Targeted (default): Focuses on protecting network daemons
- MLS (Multi-Level Security): More complex, used in high-security environments

## 5. Booleans

Booleans are on/off switches that allow runtime customization of SELinux policies.

To list all booleans:
```
getsebool -a
```

To change a boolean:
```bash
setsebool httpd_can_network_connect on
```

To make the change persistent:
```bash
setsebool -P httpd_can_network_connect on
```

## 6. Troubleshooting SELinux

- Check for denials:
```
ausearch -m AVC,USER_AVC,SELINUX_ERR -ts recent
```

- Use SELinux troubleshooter:
```
sealert -a /var/log/audit/audit.log
```

- Analyze SELinux logs:
```
grep "SELinux" /var/log/messages
```

## 7. File and Directory Labeling

To change the SELinux context of a file or directory:
```
chcon -t httpd_sys_content_t /path/to/file
```

To restore the default context:
```
restorecon -v /path/to/file
```

## 8. Managing SELinux Modules

List available modules:
```
semodule -l
```

Enable a module:
```
semodule -e modulename
```

Disable a module:
```
semodule -d modulename
```

## 9. Creating Custom SELinux Policies

For complex environments, you may need to create custom policies:

- Install policy development tools:
```
yum install selinux-policy-devel
```

- Write a policy module (.te file)
- Compile and package the module:
```
make -f /usr/share/selinux/devel/Makefile
```
- Install the module:
```
semodule -i mymodule.pp
```

## 10. SELinux and Containers

SELinux provides strong isolation for containers:
- Each container runs with its own SELinux context
- Prevents container processes from accessing host resources

To run a container with a specific SELinux context:
```
docker run --security-opt label=type:svirt_lxc_net_t my_image
```

## 11. Best Practices

- Keep SELinux enabled and in enforcing mode
- Use SELinux booleans instead of custom policies when possible
- Regularly review and update SELinux policies
- Use SELinux MLS for high-security environments
- Educate system administrators about SELinux

## 12. Additional Resources

- SELinux Project: https://github.com/SELinuxProject
- Red Hat SELinux Guide: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/using_selinux/index

