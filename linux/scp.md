
# SCP

```bash
# 本地复制到远程(use ssh_key)
SSH_USER=user_name
SSH_KEY=./id_rsa
SSH_PORT=22
FILE_NAME=file_name
FROM_PATH=./${FILE_NAME}
TO_IP=127.0.0.1
TO_PATH=/home/${SSH_USER}/${FILE_NAME}
scp -i ${SSH_KEY} -rpC -P${SSH_PORT} ${FROM_PATH} ${SSH_USER}@${TO_IP}:${TO_PATH}

```

```bash
# 从远程复制到本地(use ssh_key)
SSH_USER=user_name
SSH_KEY=./id_rsa
SSH_PORT=22
FROM_PATH=./${FILE_NAME}
TO_PATH=/home/${FILE_NAME}
FROM_IP=127.0.0.1
scp -i ${SSH_KEY} -rpC -P${SSH_PORT} ${SSH_USER}@${FROM_IP}:${FROM_PATH} ${TO_PATH}
```
