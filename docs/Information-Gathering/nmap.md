# Nmap 工具使用

```bash
# -f：分片扫描，常用用于绕过防火墙
# --source-port：指定扫描源端口
nmap 192.168.5.2 -Pn -f --source-port=4444

# --min-rate：扫描的最低速率
sudo nmap -p- 192.168.5.2 --min-rate=2000

# -sCV：使用默认脚本扫描，并扫描端口服务
sudo nmap -p22,80,3306 192.168.5.2
```