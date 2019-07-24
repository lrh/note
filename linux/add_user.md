
# add user del user

* add key user
```bash
# 加用户方法，上传key文件authorized_keys,并修改用户名密码，执行下面脚本
user_name=USER_NAME
pass_word=PASSWORD
/usr/sbin/useradd -g wheel ${user_name} 2>/dev/null
echo ${pass_word} | passwd --stdin ${user_name}
/bin/mkdir -p /home/${user_name}/.ssh/ 2>/dev/null
/bin/cp -f ./authorized_keys /home/${user_name}/.ssh/
chown -R ${user_name}.wheel /home/${user_name}/.ssh/
chmod 600 /home/${user_name}/.ssh/authorized_keys
chmod 700 /home/${user_name}/.ssh/
```

* del user
```bash
user_name=USER_NAME
userdel $user_name
rm -rf /home/$user_name
```

