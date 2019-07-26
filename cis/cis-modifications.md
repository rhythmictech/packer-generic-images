# CIS Modifications
This document explains why modifications were made the the CIS rules. 

## Amazon Linux
CIS Amazon Linux 2 Benchmark v1.0.0 - 11-14-2018

### Disabled Rules 
Each section describes what rules we want to disable and why, followed by a list of which tags need to be skipped in the CIS role to disable them.



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
