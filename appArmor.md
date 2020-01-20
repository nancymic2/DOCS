### HPE Helion OpenStack® 3.0:
# Refining Access Control with AppArmor
AppArmor is a Mandatory Access Control (MAC) system as opposed to a discretionary access control system. It is a kernel-level security module for Linux that controls access to low-level resources based on rights granted via policies to a program rather than to a user role. It enforces rules at the lowest software layer—the kernel level—preventing software from circumventing resource restrictions that reside at levels above the kernel. With AppArmor, the final gatekeeper is closest to the hardware.

Controlling resource access per application versus per user role allows you to enforce rules based on specifically what a program can do versus trying to create user roles that are broad enough yet specific enough to apply to a group of users. In addition, it prevents the trap of having to predict all possible vulnerabilities in order to be secure.

AppArmor uses a hybrid of whitelisting and blacklisting rules, and its security policies are/can be cascading, permitting inheritance from different or more general policies. Policies are enforced on a per-process basis.

AppArmor also lets you tie a process to a CPU core if you want, and set process priority.

AppArmor profiles are loaded into the kernel, typically on boot. They can run in either enforcement or complain modes. In enforcement mode, the policy is enforced and policy violation attempts are reported. In complain mode, policy violation attempts are reported but not prevented.

## AppArmor in HPE Helion OpenStack 3.0
AppArmor in HPE Helion OpenStack 3.0 is installed and enabled on the KVM compute nodes by default. It runs in enforce mode. It 
enforces mandatory access control policies for the libvirt process. Customers can run 'systemctl status apparmor' command on the 
compute nodes to check that the service is active.
In this implementation it is designed to mitigate three threat scenarios:
* Hypervisor breakout followed by compromise of hosting qemu/kvm process.
    * Malicious manipulation of qemu APIs via Nova compute.
    * Malicious manipulation of libvirt APIs via Nova compute.
    
The AppArmor profiles here:
* Use the sVirt mechanism to deliver a very locked down profile for KVM / QEMU processes that guests run under. This enforces strict isolation of the guest VMs, which is significantly more useful than just securing libvirt.
* Contains important improvements over stock Debian profiles, including:
    * Preventing libvirt from writing to any system config.
    * Preventing Libivirt from accessing any hardware and device nodes that are not required for Helion-based solutions. While
    the stock AppArmor profiles are more permissive, as libvirt supports a larger set of functionality than is exposed via 
    Nova compute, the profiles included here only allow access to features exposed through Nova.

_The OpenStack® Word Mark and OpenStack Logo are either registered trademarks/service marks or trademarks/service marks of the OpenStack Foundation in the United States and other countries and are used with the OpenStack Foundation's permission. We are not affiliated with, endorsed or sponsored by the OpenStack Foundation or the OpenStack community._

_Cloud Foundry is a trademark and/or registered trademark of CloudFoundry.org Foundation in the United States and/or other countries._
_© Copyright 2016 Hewlett Packard Enterprise Development LP
Terms of Use and Privacy Policy_
