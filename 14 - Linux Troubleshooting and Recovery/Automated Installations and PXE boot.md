Automating installations and setting up PXE (Preboot Execution Environment) boots on Linux Mint can streamline the deployment process for multiple systems. Here’s a guide to help you get started:

### Automated Installations

1. **Using Preseed Files**:
   - Preseed files allow you to automate the installation process by providing answers to the installation prompts.
   - Create a preseed file (`preseed.cfg`) with your configuration:
     ```plaintext
     d-i debian-installer/locale string en_US
     d-i keyboard-configuration/xkb-keymap select us
     d-i netcfg/get_hostname string mint
     d-i netcfg/get_domain string local
     d-i mirror/country string manual
     d-i mirror/http/hostname string archive.ubuntu.com
     d-i mirror/http/directory string /ubuntu
     d-i mirror/http/proxy string
     d-i passwd/root-password password rootpassword
     d-i passwd/root-password-again password rootpassword
     d-i passwd/user-fullname string User
     d-i passwd/username string user
     d-i passwd/user-password password userpassword
     d-i passwd/user-password-again password userpassword
     d-i clock-setup/utc boolean true
     d-i time/zone string UTC
     d-i partman-auto/method string regular
     d-i partman-auto/choose_recipe select atomic
     d-i partman/confirm boolean true
     d-i partman/confirm_nooverwrite boolean true
     d-i partman/confirm_write_new_label boolean true
     ```
   - Use the preseed file during installation by appending it to the boot parameters:
     ```plaintext
     linux /install/vmlinuz auto=true priority=critical preseed/url=http://yourserver/preseed.cfg
     ```

2. **Using Kickstart**:
   - Kickstart files are another method for automating installations, commonly used with Red Hat-based distributions but also supported by Debian-based systems.
   - Create a kickstart file (`ks.cfg`) with your configuration:
     ```plaintext
     lang en_US
     keyboard us
     timezone UTC
     rootpw rootpassword
     user user --password userpassword
     reboot
     ```
   - Use the kickstart file during installation by appending it to the boot parameters:
     ```plaintext
     linux /install/vmlinuz ks=http://yourserver/ks.cfg
     ```

### Setting Up PXE Boot

1. **Install and Configure a TFTP Server**:
   - Install the TFTP server:
     ```bash
     sudo apt-get install tftpd-hpa
     ```
   - Configure the TFTP server by editing `/etc/default/tftpd-hpa`:
     ```plaintext
     TFTP_USERNAME="tftp"
     TFTP_DIRECTORY="/var/lib/tftpboot"
     TFTP_ADDRESS="0.0.0.0:69"
     TFTP_OPTIONS="--secure"
     ```
   - Restart the TFTP server:
     ```bash
     sudo systemctl restart tftpd-hpa
     ```

2. **Install and Configure a DHCP Server**:
   - Install the DHCP server:
     ```bash
     sudo apt-get install isc-dhcp-server
     ```
   - Configure the DHCP server by editing `/etc/dhcp/dhcpd.conf`:
     ```plaintext
     subnet 192.168.1.0 netmask 255.255.255.0 {
       range 192.168.1.10 192.168.1.100;
       option routers 192.168.1.1;
       option domain-name-servers 8.8.8.8, 8.8.4.4;
       filename "pxelinux.0";
       next-server 192.168.1.1;
     }
     ```
   - Restart the DHCP server:
     ```bash
     sudo systemctl restart isc-dhcp-server
     ```

3. **Prepare PXE Boot Files**:
   - Download and extract the PXE boot files:
     ```bash
     sudo apt-get install syslinux
     sudo cp /usr/lib/syslinux/pxelinux.0 /var/lib/tftpboot/
     sudo mkdir -p /var/lib/tftpboot/pxelinux.cfg
     sudo cp /usr/lib/syslinux/menu.c32 /var/lib/tftpboot/
     sudo cp /usr/lib/syslinux/memdisk /var/lib/tftpboot/
     sudo cp /usr/lib/syslinux/mboot.c32 /var/lib/tftpboot/
     sudo cp /usr/lib/syslinux/chain.c32 /var/lib/tftpboot/
     ```
   - Create a PXE configuration file (`/var/lib/tftpboot/pxelinux.cfg/default`):
     ```plaintext
     DEFAULT menu.c32
     PROMPT 0
     TIMEOUT 300
     ONTIMEOUT local
     MENU TITLE PXE Boot Menu

     LABEL Linux Mint
       MENU LABEL Install Linux Mint
       KERNEL /install/vmlinuz
       APPEND initrd=/install/initrd.gz auto=true priority=critical preseed/url=http://yourserver/preseed.cfg
     ```

4. **Boot from PXE**:
   - Configure your client machines to boot from the network (PXE) in the BIOS/UEFI settings.
   - The client machines should now boot from the PXE server and start the automated installation process.

These steps should help you set up automated installations and PXE boots on Linux Mint¹²³⁴. If you have any specific questions or need further assistance, feel free to ask!

Source: Conversation with Copilot, 7/19/2024
- [(1) How To: Boot Linux Mint 19.3 Over Network PXE Using SERVA ... - Ares Galaxy.]( https://www.aresgalaxy.org/system-administration/how-to/boot-linux-mint-19-3-over-network-pxe-using-serva-on-windows-7-8-10.)
- [(2) Setup PXE Boot Server using cloud-init for Ubuntu 20.04 ... - GoLinuxCloud.](https://www.golinuxcloud.com/pxe-boot-server-cloud-init-ubuntu-20-04/.)
- [(3) Setting up a 'PXE Network Boot Server' for Multiple Linux ... - Tecmint.](https://www.tecmint.com/install-pxe-network-boot-server-in-centos-7/.)
- [(4) Setup Network boot for installing OS using PXE server.](https://www.protocolten.com/postbase/setup-network-boot-for-installing-os-using-pxe-server.)
