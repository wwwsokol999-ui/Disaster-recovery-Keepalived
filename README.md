
# Disaster Recovery Lab (HSRP + Keepalived)

Настроена отказоустойчивость сети на двух уровнях:
- Cisco HSRP (Packet Tracer)
- Linux Keepalived (VRRP)

Обеспечено автоматическое переключение при отказе узла без потери доступа.

---

#  Топология

## Cisco
- 2 роутера
- 2 свитча
- PC + Server
- Virtual IP: 192.168.0.1 / 192.168.1.1

## Linux
- 2 VM
- nginx
- keepalived
- Virtual IP: 192.168.238.200

---

# 🔹 Конфигурация

## HSRP (Cisco)

```bash
interface g0/1
 standby version 2
 standby 1 ip 192.168.1.1
 standby 1 priority 110
 standby 1 preempt
 standby 1 track g0/0 20
```
## 🖧 Схема сети

### Топология

- 2 Linux VM (Ubuntu)
- nginx на каждом сервере
- Keepalived (VRRP)
- 1 Virtual IP

---

### Подсети

| Узел | IP |
|-------|----------------|
| Server1 (MASTER) | 192.168.238.130 |
| Server2 (BACKUP) | 192.168.238.131 |
| Virtual IP (VIP) | 192.168.238.200 |

---

## ⚙️ Установка ПО

На **обеих ВМ**:

```bash
sudo apt update
sudo apt install nginx keepalived curl netcat -y
sudo systemctl enable nginx
sudo systemctl start nginx
```
![Keepalived](Keepalived.png)
