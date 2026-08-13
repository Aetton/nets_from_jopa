# nets_from_jopa

Практический курс по сетям для инженера с опытом DevOps/SRE.

## Цель

Собрать цельную инженерную модель сети и научиться:

- понимать путь пакета на каждом участке;
- локализовать проблему по слою и границе ответственности;
- читать маршрутизацию, ARP/NDP, DNS, TCP и firewall;
- уверенно работать с Linux networking;
- разбираться в VLAN, bridges, bonds, namespaces, overlays и VPN;
- диагностировать реальные сетевые аварии через tcpdump, Wireshark, ip, ss и nftables;
- перейти к BGP, VXLAN/EVPN, Kubernetes networking и сетям виртуализации через практику.

## Принцип курса

Каждый модуль проходит четыре стадии:

1. **Модель** — что происходит на самом деле.
2. **Наблюдение** — как увидеть это в Linux и в пакетах.
3. **Поломка** — намеренно ломаем одну вещь.
4. **Диагностика** — находим причину без заранее указанного места поломки.

Теория считается усвоенной, когда по симптому можно предсказать, что покажут инструменты.

## Структура

| Этап | Тема | Результат |
|---|---|---|
| 00 | Диагностика исходного уровня | Находим реальные пробелы |
| 01 | Пакет, Ethernet, ARP, MTU | Видим жизнь пакета внутри L2-сегмента |
| 02 | IPv4, subnetting, routing | Читаем маршрут пакета |
| 03 | ICMP и диагностика пути | Понимаем ping, traceroute и PMTUD |
| 04 | UDP, TCP, сокеты | Понимаем соединение до TCP state machine |
| 05 | DNS | Разбираем resolution от libc до authoritative server |
| 06 | Linux networking | iproute2, namespaces, bridges, veth, policy routing |
| 07 | Firewall и NAT | nftables, conntrack, DNAT/SNAT, stateful filtering |
| 08 | VLAN и L2-инфраструктура | trunk/access, STP, bonding/LACP |
| 09 | VPN и туннели | WireGuard, IPsec concepts, GRE, routing через tunnel |
| 10 | IPv6 | NDP, SLAAC, RA, DHCPv6 и routing |
| 11 | Динамическая маршрутизация | OSPF и BGP |
| 12 | Overlay networking | VXLAN, EVPN, encapsulation |
| 13 | Виртуализация и контейнеры | Proxmox/Linux bridges, Docker, Kubernetes CNI concepts |
| 14 | Production troubleshooting | Комплексные аварии без указания слоя |

## Формат материалов

```text
modules/
  00-baseline/
  01-l2-packet/
  ...
labs/
  topology/
  breakfix/
notes/
  packet-path.md
  commands.md
```

В каждом модуле будут:

- `README.md` — объяснение модели;
- `lab.md` — практическая лабораторная работа;
- `breakfix.md` — намеренная поломка для диагностики;
- `questions.md` — вопросы на понимание, а не запоминание.

## Главный критерий

После курса задача вида «сервис с этой VM открывается с хоста, из соседней VLAN нет, curl висит 30 секунд, SYN виден только на одном интерфейсе» должна превращаться в конечное дерево проверок, а не в перебор случайных команд.
