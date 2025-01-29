> [[Back]]

Tags: 
Status: 
Related: 

___

# Revisar Falta de memoria en servidor

```sh
htop
journalctl -u odoo140.service -n 50
free -h
dmesg | grep -i "oom"
cat /var/log/kern.log | grep "oom-kill"
grep -i "ERROR" /var/log/odoo/odoo140.log
```