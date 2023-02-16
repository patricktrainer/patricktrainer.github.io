---
date: '2023-02-16'
draft: false
title: Building-a-simple-VPN-with-WireGuard-with-a-Raspbe
---

# Building-a-simple-VPN-with-WireGuard-with-a-Raspbe

# Building a simple VPN with WireGuard with a Raspberry Pi as Server // Andreas Happe
Created: January 30, 2020 9:07 AM
Tags: Projects, Tech
URL: https://snikt.net/blog/2020/01/29/building-a-simple-vpn-with-wireguard-with-a-raspberry-pi-as-server/
Now that wireguard will be part of the upcoming Linux 5.6 Kernel it’s time to see how to best integrate it with my [Raspberry Pi based LTE-Router/Access Point Setup](https://snikt.net/blog/2019/06/22/building-an-lte-access-point-with-a-raspberry-pi/).
# What is my scenario?
This will be the VPN server (called *edgewalker* in this post)
- An Android Phone that should use the VPN for all communication when connected
- An Linux Laptop that should use the VPN only accessing network services that are exposed to the VPN
Each device connected to the VPN should be able to connect to all other devices, e.g., my phone should be able to connect to a webserver running on the laptop as long as both are part of the VPN network.
Would I have read the manual I would have done the right steps:
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%20d60fe88e71e44732b941d302ac9e9c3f.csv)
On the Raspberry Pi I am using Raspbian Buster, this distribution already included the `wireguard` package, I installed it with:
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%2084d4eda03d13471b80045aaef74664fc.csv)
On the Android Phone, I used the Google App Store to install the [WireGuard VPN Application](https://play.google.com/store/apps/details?id=com.wireguard.android).
# Creating a configuration file for the VPN Server (Raspberry Pi)
Configuration was quite easy, I just created the following file at `/etc/wireguard/wg0.conf`:
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%2086ffbe2372fc4cddb21de52e39da3613.csv)
Some notes:
- Please fill in the values from the created key files
- I am creating a VPN network that uses `10.200.200.0/24` for its internal IP range
- my server uses `wwan0` as external network interface in the `PostUp`/`PostDown`-Commands, please adapt that to use your network-facing interface (might be eth0)
It’s easy to bring the VPN network up with the following command:
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%209e7f760a758b4f3da348009db1e264ad.csv)
One small thing: I am using `dnsmasq` as DNS server and have bound it to the network interface `br0`.
In dnsmasq you do this by adding a new config line to `/etc/dnsmasq.conf` with the network interface, e.g.:
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%20f5595dbeabe74a6e971485162a5c2e4f.csv)
In addition I’ve added some iptable rules to allow traffic to the listening UDP port (51280):
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%204579712d7bb14b59a88ae36b27fc8775.csv)
Now that everything works, we can utilize systemd to automatically start the VPN tunnel:
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%200b7dbc84ab72443791bc5a0a11274e33.csv)
Mostly the Laptop setup consists of creating a matching configuration file in `/etc/wireguard/wg0.conf` on the Laptop:
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%207e45ff8493b34fa1ade1a84ee8e6af77.csv)
Some notes:
- edgewalker should be the public IP-address or public hostname of the VPN server
- By setting `AllowedIPs` to `10.200.200.0/24` we are only using the VPN for accessing the internal VPN network.
We prepare the following file (let’s call it `mobile.conf`) on the server through ssh:
[Untitled](Building%20a%20simple%20VPN%20with%20WireGuard%20with%20a%20Raspbe%20a4272792063a47719296c41defa23053/Untitled%20Database%2037e075f9123d4f9088f16fb3a8531955.csv)
In contrast to the laptop setup we are forcing the mobile device to use our VPN server as DNS server (that’s the `DNS` setting) as well as using the newly VPN tunnel for all traffic (by using `0.0.0.0/0` as wildcard for `AllowedIPs`).
