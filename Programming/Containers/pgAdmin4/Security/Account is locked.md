#pgAdmin4 #account #security
1. ```sudo docker exec -u root -it <your_container_name> /bin/sh```
2. ```cd ../var/lib/pgadmin```
3. ```apk add sqlite```
4. ```sqlite3 pgadmin4.db "UPDATE USER SET LOCKED = false, LOGIN_ATTEMPTS = 0 WHERE USERNAME = '<your_account_username>';" ".exit"```