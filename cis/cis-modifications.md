# CIS Modifications
This document explains why modifications were made the the CIS rules. 

## Amazon Linux
CIS Amazon Linux 2 Benchmark v1.0.0 - 11-14-2018

### Disabled Rules 
Each section describes what rules we want to disable and why, followed by a list of which `tags` need to be skipped in the CIS role to disable them.

To see the list of disabled rules look at [ansible.cfg](ansible.cfg)

#### Don't apply Level 2 rules
Level 2 rules are very restrictive and not usually worth it unless you have a Level 2 compliance requirement.
- `level-2`

#### Don't set sticky bit everywhere
> 1.1.18 Ensure sticky bit is set on all world-writable directories (Scored)

CIS recommends setting sticky bit on all world-writable directories, but this breaks many applications so we prefer not to do this by default
- `1.1.18`

#### Don't run `yum update --security`
> 1.8 Ensure updates, patches, and additional security software are installed (Scored)

We are managing patching separately, and forcing a dist-upgrade in CIS is a bad idea for us
- `1.8`

#### Don't set Postfix interfaces
> 2.1.15 Ensure mail transfer agent is configured for local-only mode  

We handle this in other roles and don't want the CIS role messing with it
-`2.1.15`

#### Skip all firewall controls
> 3.5 Firewall Configuration

We're going to be using security groups which function as an external firewall rather than the internal firewall specified by CIS, IPtables. 
-  `3.5.1.1`
-  `3.5.1.2`
-  `3.5.1.3`
-  `3.5.1.4`
-  `3.5.2.1`
-  `3.5.2.2`
-  `3.5.2.3`
-  `3.5.2.4`
-  `3.5.3`
#### Skip all rsyslog rules
We want to handle logging config in other roles. Most of these controls are not implemented anyway
- `syslog`

#### Don't configure sshd
We want to change the sshd config in a much more minimal way where necessary.
- `sshd`

#### Don't set authentication rules
> 5.3 Configure PAM  
5.4 User Accounts and Environment   
5.4 User Accounts and Environment
5.4.1 Set Shadow Password Suite Parameters  
5.4.1.1 Ensure password expiration is 365 days or less (Scored)  
5.4.1.2 Ensure minimum days between password changes is 7 or more (Scored)  
5.4.1.3 Ensure password expiration warning days is 7 or more (Scored)  
5.4.1.4 Ensure inactive password lock is 30 days or less (Scored)  
5.4.3 Ensure default group for the root account is GID 0 (Scored)  
5.6 Ensure access to the su command is restricted (Scored)  

We're authenticating through an external directory, so these rules about local authentication don't make sense
-  `5.3.1`
-  `5.3.2`
-  `5.3.3`
-  `5.3.4`
-  `5.4.1.1`
-  `5.4.1.2`
-  `5.4.1.3`
-  `5.4.1.4`
-  `5.4.3`
-  `5.6`

#### Don't set strict umask
> 5.4.4 Ensure default user umask is 027 or more restrictive (Scored)  

The CIS recommended strict umask rule has very little advantage for most servers and can cause unnecessary friction
- `5.4.4`

#### Don't manage auth permissions and user config
> 6 System Maintenance

We want to audit these rules from Nessus, not set them during AMI creation
- `section-6`

#### Disable TCP Wrappers 
> 3.3 TCP Wrappers  
3.3.2 Ensure /etc/hosts.allow is configured (Not Scored)  
3.3.3 Ensure /etc/hosts.deny is configured (Not Scored)  
3.3.4 Ensure permissions on /etc/hosts.allow are configured (Scored)  
3.3.5 Ensure permissions on /etc/hosts.deny are configured (Scored)

Those rules block all traffic by default at the hostsfile level. It’s an extra layer of firewalling that’s difficult to manage and takes away our ability to rely on security groups (which is where we will be managing traffic)

-  `3.3.2`
-  `3.3.3`
-  `3.3.4`
-  `3.3.5`

----


## Ubuntu

### Disabled rules
Each section describes what rules we want to disable and why, followed by a list of which tags need to be skipped in the CIS role to disable them.

#### Don't apply Level 2 rules
Level 2 rules are very restrictive and not usually worth it unless you have a Level 2 compliance requirement.
* `level2`

#### Don't set sticky bit everywhere
CIS recommends setting sticky bit on all world-writable directories, but this breaks many applications so we prefer not to do this by default
* `rule_1.1.20`

#### Don't set bootloader password
Using a bootloader password isn't relevant in AWS and could potentially break things
* `rule_1.4.2`

#### Don't run apt-get dist-upgrade
We are managing patching separately, and forcing a dist-upgrade in CIS is a bad idea for us
* `rule_1.8`

#### Don't set Postfix interfaces
We handle this in other roles and don't want the CIS role messing with it
* `rule_2.2.15`

#### Skip all firewall controls
We're going to be using security groups instead of OS-level firewall
* `rule_3.6`
* `rule_3.6.1`
* `rule_3.6.2`
* `rule_3.6.3`
* `rule_3.6.4`
* `rule_3.6.5`

#### Skip all rsyslog rules
We want to handle logging config in other roles. Most of these controls are not implemented anyway
* `syslog`

#### Don't configure sshd
We want to change the sshd config in a much more minimal way where necessary.
* `sshd`

#### Don't set authentication rules
We're authenticating through an external directory, so these rules about local authentication don't make sense
* `rule_5.3.1`
* `rule_5.3.2`
* `rule_5.3.3`
* `rule_5.3.4`
* `rule_5.4.1.1`
* `rule_5.4.1.2`
* `rule_5.4.1.3`
* `rule_5.4.1.4`
* `rule_5.4.2`
* `rule_5.4.3`
* `rule_5.5`
* `rule_5.6`

#### Don't set strict umask
The CIS recommended strict umask rule has very little advantage for most servers and can cause unnecessary friction
* `rule_5.4.4`

#### Don't manage auth permissions and user config
We want to audit these rules from Nessus, not set them during AMI creation
* `section6`
