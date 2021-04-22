# tool-pgadmin

This service only helps to manage users on web console pgAdmin, which is without database maintenance. The init.yml setup the environment in ubuntu server.

```sh
### check_syntax

$ echo -e "-----list-tasks-----"
$ ansible-playbook --list-tasks --list-hosts -i ${PROD_INVENTORY} ansible/playbooks/init.yml -vvv
$ ansible-playbook --list-tasks --list-hosts -i ${PROD_INVENTORY} ansible/playbooks/deploy_pgadmin.yml -vvv

$ echo -e "-----syntax-check-----"
$ ansible-playbook --syntax-check -i ${PROD_INVENTORY} ansible/playbooks/init.yml -vvv
$ ansible-playbook --syntax-check -i ${PROD_INVENTORY} ansible/playbooks/deploy_pgadmin.yml -vvv

## deploy
$ ansible-playbook -i ${PROD_INVENTORY} ansible/playbooks/init.yml
$ ansible-playbook -i ${PROD_INVENTORY} ansible/playbooks/deploy_pgadmin.yml
```
## Run postgresql

```docker
$ docker run -itd --rm --name postgres --network pgadmin_default -e POSTGRES_HOST_AUTH_METHOD=trust -e POSTGRES_PASSWORD=thisisas -p 5432:5432 --restart always postgres:11
```

- -d ：後台執行 Container
- -name mypostgres ：Container 取名
- -v postgresql-data:/var/lib/postgresql/data ：使用剛建立的volume，postgresql-data 掛載到 Container 的 /var/lib/postgresql/data。
- -restart always ：如果 container 遇到例外的情況，例如是重新開機，docker 會重新啟動 container
- -p 5432:5432 ：將 Container 的 5432 Port 映射到主機的 5432 Port (host:container)

## Adding a new console user

1. Login pgAdmin with Adminstrator account.
2. Navigate to User Managemet and click + to add anuser.
![add_user](/image/image.png)
![create_user](/image/create_user.png)
3.Input the information and set the Role to User.

## Using pgAdmin client to manage PostgreSQL

**Conncting to a server**

1. Login pgAdmin with applier's console account
2. Right click the Servers field
3. Select Create > Server
4. Input the connection properties

![create_server](/image/create_server.png)

**Creating a database user and configuring privileges**

1. Expand the Server
2. Right click Login/Group Roles
![Login_role](/image/Login_Group_Roles.png)
3. Select Create - Login/Group Role
   - Set username in General > Name
   - Set password in Definition > Password
   - As an user, set Can Login to Yes in Privileges
4. Expand the Databases
5. Right click the target database
6. Select Properties
7. Based on the user role to set privileges:
   - Go to Security to enable privileges
  ![privileges](/image/privileges.png)
   - Go to Default Privileges to enable privileges
   ![admin](/image/admin.png)