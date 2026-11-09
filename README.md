# Nmap scan lab

A beginner lab where I used Nmap to find open ports and service versions on a practice target, then wrote up the results. I ran everything on an Android phone, using Kali Linux (NetHunter) in Termux.

## Target
scanme.nmap.org (45.33.32.156). The Nmap project runs this server for people to practise on and allows light scanning. I scanned this one machine only. Only scan machines you own or have permission to test.

## Commands
| Command | What it does |
|---|---|
| nmap -sT -Pn -sV 45.33.32.156 | TCP connect scan, no ping, service and version detection |
| nmap -sT -Pn -sV -sC 45.33.32.156 | Same, plus Nmap's default scripts |

## Results
Host up (about 0.29 s latency). 3 open ports out of the 1,000 most common, 997 closed. OS reported as Linux.

| Port | Service | Version |
|---|---|---|
| 22/tcp | ssh | OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 |
| 80/tcp | http | Apache httpd 2.4.7 (Ubuntu) |
| 9929/tcp | nping-echo | Nping echo |

## What I noticed
- OpenSSH 6.6.1 and Apache 2.4.7 are both from around 2014. On a real network, outdated versions like these would be flagged for known vulnerabilities.
- The SSH server offers a 1024-bit DSA host key, which is weak by today's standards.
- Port 9929 is a test service that the Nmap project runs on purpose.
- These are teaching points, because the server is set up this way for practice.

## What did not work, and why
The aggressive scan (-A) and traceroute failed with "failed to determine route". Kali on Android runs in a chroot, so Nmap can't read the routing table or open raw sockets, which OS detection needs. I used -sT (TCP connect) and -Pn (skip ping) instead, and ran version detection (-sV) and default scripts (-sC) separately.

## Limits
- No OS detection or traceroute from the phone.
- I did not run host discovery (-sn) on a local network.
- One target, one snapshot in time.

## Files
- scanme_sV.txt: version scan output
- scanme_sV_sC.txt: version scan with default scripts

Author: Ponman David Labong
