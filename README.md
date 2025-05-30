# redhat-tutorial
<h1> Upgrade Kernel </h1>
<pre> yum install kernel kernel-tools kernel-tools-libs </pre><br>
<h2><a href="https://www.thegeekdiary.com/centos-rhel-7-change-default-kernel-boot-with-old-kernel/">Change default kernel (boot with old kernel) – CentOS/RHEL/OEL 7</a></h2>

<pre>
Question: How to modify the GRUB2 default entry to boot a different Kernel version?

1. Check the current running Kernel Version

# uname -a
Linux geeklab 3.8.13-94.el7uek.x86_64 #2 SMP Wed Feb 11 14:18:22 PST 2015 x86_64 x86_64 x86_64 GNU/Linux
2. List the Kernel Entries as per GRUB2 file:


# awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg
Oracle Linux Server, with Unbreakable Enterprise Kernel 3.8.13-94.el7uek.x86_64
Oracle Linux Server, with Unbreakable Enterprise Kernel 3.8.13-94.el7uek.x86_64 with debugging
Oracle Linux Server 7.1, with Linux 3.10.0-229.el7.x86_64
Oracle Linux Server 7.1, with Unbreakable Enterprise Kernel 3.8.13-55.1.6.el7uek.x86_64
Oracle Linux Server 7.1, with Linux 0-rescue-441e86c9ff854310a306bd33e56aae2b
NOTE: The first entry is denoted as Zero. So currently the Server is booted to 0th entry as per the above `uname -a` command output.
3. Let us modify the Kernel Version to 3.8.13-55.1.6.el7uek.x86_64 which is at line number 4 but denoted as entry 3.

# grub2-set-default 3
4. Changes to /etc/default/grub require rebuilding the grub.cfg file as follows:

# grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.10.0-229.el7.x86_64
Found initrd image: /boot/initramfs-3.10.0-229.el7.x86_64.img
Found linux image: /boot/vmlinuz-3.8.13-94.el7uek.x86_64
Found initrd image: /boot/initramfs-3.8.13-94.el7uek.x86_64.img
Found linux image: /boot/vmlinuz-3.8.13-55.1.6.el7uek.x86_64
Found initrd image: /boot/initramfs-3.8.13-55.1.6.el7uek.x86_64.img
Found linux image: /boot/vmlinuz-0-rescue-441e86c9ff854310a306bd33e56aae2b
Found initrd image: /boot/initramfs-0-rescue-441e86c9ff854310a306bd33e56aae2b.img
done
Reboot the Server and it will boot with Kernel Version 3.8.13-55.1.6.el7uek.x86_64.

# shutdown -r now

</pre>
<p>
  <h2>Check connectivity to Redhat Server</h2>
  <pre>
  openssl s_client -connect subscription.rhsm.redhat.com:443 &lt;/dev/null 2&gt;/dev/null | openssl x509 -text
</pre>
<h2><a href="https://access.redhat.com/solutions/29617">How to use yum/dnf to downgrade or rollback some package updates?</a></h2>
</p>
<p>
  <h2><a href="https://access.redhat.com/solutions/64069">How to use yum history to roll back an update in Red Hat Enterprise Linux 6 and later?</a></h2>
</p>  
<h2>
  Enable Red Hat Enterprise Linux 7 Server - Extras (RPMs)
</h2>

<pre>
  [root@a1qnsvl-askan01 ~]# subscription-manager repos --list | grep -i extras -A3 -B3
Repo URL:  https://cdn.redhat.com/content/dist/middleware/openjdk/1.0/x86_64/os
Enabled:   0

Repo ID:   rhel-7-server-extras-source-rpms
Repo Name: Red Hat Enterprise Linux 7 Server - Extras (Source RPMs)
Repo URL:  https://cdn.redhat.com/content/dist/rhel/server/7/7Server/$basearch/extras/source/SRPMS
Enabled:   0

  [root@a1qnsvl-askan01 ~]# subscription-manager repos --enable rhel-7-server-extras-rpms
Repository 'rhel-7-server-extras-rpms' is enabled for this system.
</pre>
