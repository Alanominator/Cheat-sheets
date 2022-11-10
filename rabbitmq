# installation
https://computingforgeeks.com/how-to-install-latest-rabbitmq-server-on-ubuntu-linux/

# check status
```
systemctl status rabbitmq-server.service
```
# Confirm if the service is configured to start on boot using the command:
```
systemctl is-enabled rabbitmq-server.service
```
# enable
```
sudo systemctl enable rabbitmq-server
```

# disable
```
sudo systemctl disable rabbitmq-server
```

# open in browser
http://localhost:15672/


# to add user
```
sudo rabbitmqctl add_user <admin> <StrongPassword>
```

# set user as admin
```
sudo rabbitmqctl set_user_tags <admin> administrator
```

# delete user
```
rabbitmqctl delete_user user
```

# change password
```
rabbitmqctl change_password <user> <strongpassword>
```

# Create new Virtualhost
```
rabbitmqctl add_vhost /<my_vhost>
```

# Delete Virtualhost
```
rabbitmqctl delete_vhost /myvhost
```

# List available Virtualhosts
```
rabbitmqctl list_vhosts
```
.

# Grant user permissions for vhost
```
rabbitmqctl set_permissions -p /<myvhost> <user> ".*" ".*" ".*"
```

# Delete user permissions
```
rabbitmqctl clear_permissions -p /<myvhost> <user>
```
.

# List vhost permissions
```
rabbitmqctl list_permissions -p /<myvhost>
```

# To list user permissions
```
rabbitmqctl list_user_permissions <user>
```

