# uninstall-MySQL-completely-in-ubuntu
uninstall MySQL completely in ubuntu

<pre>
sudo -i
service mysql stop
killall -KILL mysql mysqld_safe mysqld
apt-get --yes purge mysql-server mysql-client
apt-get --yes autoremove --purge
apt-get autoclean
deluser --remove-home mysql
delgroup mysql
rm -rf /etc/apparmor.d/abstractions/mysql /etc/apparmor.d/cache/usr.sbin.mysqld /etc/mysql /var/lib/mysql /var/log/mysql* /var/log/upstart/mysql.log* /var/run/mysqld
updatedb
exit
</pre>
If you want to delete the log of what you did while using the mysql client:
<pre>
rm ~/.mysql_history
</pre>
If you want to delete the logs of what all users on the system did while using the mysql client (the other users might be unhappy with this):
<pre>
awk -F : '{ print($6 "/.mysql_history"); }' /etc/passwd | xargs -r -d '\n' -- sudo rm -f --
</pre>
or for all logs including those outside of existing user home directories:
<pre>
sudo find / -name .mysql_history -delete
</pre>
