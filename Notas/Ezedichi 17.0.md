> [[Instalar Odoo Servidor Cliente]]

Tags: 
Status: 
Related: 

___

# Ezedichi 17.0

## Instalación odoo 17.0

1. Acceso al servidor como root
```sh
	vant@moove15~$ ssh root@195.170.165.187 -p 22
	root@195.170.165.187's password: 
	Welcome to Ubuntu 24.04.2 LTS (GNU/Linux 6.8.0-31-generic x86_64)
	
	 * Documentation:  https://help.ubuntu.com
	 * Management:     https://landscape.canonical.com
	 * Support:        https://ubuntu.com/pro
	
	 System information as of Thu Apr  3 06:22:42 AM UTC 2025
	
	  System load:  0.0                Processes:             174
	  Usage of /:   13.2% of 78.62GB   Users logged in:       1
	  Memory usage: 4%                 IPv4 address for eth0: 195.170.165.187
	  Swap usage:   0%
```
2. `sudo apt update && sudo apt upgrade`
```sh
	Scanning processes...                                                                                             
	Scanning candidates...                                                                                            
	Scanning linux images...                                                                                          
	
	Pending kernel upgrade!
	Running kernel version:
	  6.8.0-31-generic
	Diagnostics:
	  The currently running kernel version is not the expected kernel version 6.8.0-57-generic.
	
	Restarting the system to load the new kernel will not be handled automatically, so you should consider rebooting.
	
	Restarting services...
	
	Service restarts being deferred:
	 /etc/needrestart/restart.d/dbus.service
	 systemctl restart systemd-logind.service
	 systemctl restart unattended-upgrades.service
	
	No containers need to be restarted.
	
	User sessions running outdated binaries:
	 root @ session #2: login[1159], su[1344]
	 root @ user manager service: systemd[1281]
	
	No VM guests are running outdated hypervisor (qemu) binaries on this host.
	
	```
3. `reboot`
4. Crear `install_production.sh` de la rama `Pycharm` en servidor
```sh
root@ezedichi:~# touch /tmp/install.sh
root@ezedichi:~# nano /tmp/install.sh 
# Copiar pegar el script de github

```