# docker-lamp

Installation:
1. Docker Toolbox
    - Virtualbox
    - Docker
    - Kinematic (optional)

Basic commands:

    docker-compose up -d
    docker-compose down

SSH:

    ssh -p 2222 www-data:192.168.99.100

Samba:
- Windows:

      \\192.168.99.100\www-data

- Linux, macOS:

      smb://192.168.99.100/www-data