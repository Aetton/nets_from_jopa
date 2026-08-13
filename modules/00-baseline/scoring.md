# Scoring and routing

Baseline нужен для выбора кратчайшего маршрута по курсу.

## Оценка каждой темы

Для каждого блока оцени отдельно:

1. **Model** — можешь ли объяснить механизм причинно.
2. **Prediction** — можешь ли до запуска команды предсказать результат.
3. **Troubleshooting** — можешь ли построить последовательность проверок от симптома к причине.

## C — Foundation

Ставь C, если базовые сущности путаются, объяснение держится на рецептах, трудно предсказать движение пакета или лабораторная работа требует пошаговой инструкции.

Маршрут:

```text
foundation
→ mental-model
→ observe
→ lab
→ checkpoint
→ breakfix
```

## B — Working

Ставь B, если обычные задачи решаются уверенно, основные команды знакомы и общая модель правильная, но остаются пробелы в деталях и сложных сценариях.

Маршрут:

```text
mental-model
→ observe
→ lab
→ checkpoint
→ breakfix
```

## A — Strong

Ставь A, если механизм объясняется без существенных пробелов, поведение можно предсказывать, инструменты выбираются под конкретную гипотезу, а диагностика идёт по границам packet path.

Маршрут:

```text
checkpoint
→ deep-dive
→ breakfix-hard
```

## Карта baseline → modules

| Baseline block | Module |
|---|---|
| L2 / ARP | 01 Packet, Ethernet, ARP, MTU |
| Routing | 02 IPv4 and routing |
| ICMP / traceroute | 03 ICMP and path diagnostics |
| MTU | 01 + 03 |
| TCP / UDP / sockets | 04 Transport and sockets |
| DNS | 05 DNS |
| Linux networking | 06 Linux networking |
| NAT / conntrack | 07 Firewall and NAT |
| VLAN | 08 VLAN and L2 infrastructure |
| Bonding / LACP | 08 VLAN and L2 infrastructure |
| IPv6 | 10 IPv6 |
| Routing protocols | 11 Dynamic routing |
| Namespace / bridge | 06 + 13 |
| Incident | общий sanity check |

## Как оценивать incident

Последний incident оценивает не угаданную причину, а метод поиска.

**C:** человек сразу выбирает одну любимую гипотезу и начинает проверять только её.

**B:** перечисляет разумные причины и инструменты, но порядок проверки остаётся рыхлым.

**A:** сначала локализует границу прохождения трафика:

```text
source
→ source routing
→ L2
→ gateway
→ inter-VLAN routing
→ hypervisor bridge
→ VM interface
→ guest firewall
→ socket
```

а затем использует наблюдение в соседних точках, чтобы последовательно сужать область поиска.

## Профиль участника

После baseline составь таблицу вида:

```text
L2/ARP              B
IPv4/routing        A
ICMP/MTU            C
TCP/UDP             B
DNS                 A
Linux networking    A
Firewall/NAT        B
VLAN/LACP           C
IPv6                C
Dynamic routing     C
```

Это не итоговая оценка специалиста. Это конфигурация маршрута по курсу.
