# Home Network Setup with Docker and Pi-hole

## 1. Overview
This document covers the setup of a home network server using Docker on a Linux VM, including the installation and configuration of Pi-hole for network-wide ad blocking and DNS management.

## 2. Prerequisites
- A Linux virtual machine set up with internet access.
- Docker and Docker Compose installed.
- Basic knowledge of Linux commands.

## 3. Steps Taken

### 3.1. Initial VM Setup
- Updated the system and installed essential tools:
  ```bash
  sudo apt update && sudo apt upgrade

##3.2. Docker Installation
sudo apt install docker.io
docker --version
sudo apt install docker-compose

##3.3. Creating the Docker Compose File
Created the docker-compose.yml file for Pi-hole:
  version: '3'

services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    environment:
      TZ: 'America/New_York'         # Set your timezone here
      WEBPASSWORD: 'admin'           # Set a web UI password
    volumes:
      - './pihole/etc-pihole:/etc/pihole'
      - './pihole/etc-dnsmasq.d:/etc/dnsmasq.d'
    ports:
      - "80:80/tcp"                  # Web UI
      - "53:53/tcp"                  # DNS
      - "53:53/udp"
    restart: unless-stopped

##3.4. Troubleshooting Steps
Port Conflict Issue: Encountered an error where port 53 was already in use by systemd-resolved.
Checked processes using port 53:
sudo lsof -i :53
sudo systemctl stop systemd-resolved
sudo systemctl disable systemd-resolved

3.5. Final Setup and Verification
Ran the Docker Compose command to start the Pi-hole container
sudo docker-compose up -d
http://<VM_IP_ADDRESS>/admin

4. Next Steps
Configure your router or devices to use Pi-hole as the DNS server.
Test the network configuration and monitor the query logs in the Pi-hole dashboard.
