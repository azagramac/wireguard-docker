[![GitHub Release](https://img.shields.io/github/release/linuxserver/docker-wireguard.svg?color=88171a&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=wireguard)](https://github.com/linuxserver/docker-wireguard/releases)

<p align="center">
  <img src="https://github.com/user-attachments/assets/03753398-c668-4759-b712-407fdc04390e" width="450" title="logo_wg">
</p>

### Requeriments
- Service docker running.
- Open port 51820 UDP on the router (you can customize a port).
- Change the variable `SERVERURL=YOUR_DOMAIN` with your domain name.
- Change the IPv4 range of the `ALLOWEDIPS=192.168.1.0/24` variable to the appropriate one.

#### Optional
If you have a server with [AdGuardHome](https://github.com/azagramac/adguardhome-docker) or PiHole, you can put the IP of the server where you have that service running in the variable `PEERDNS=1.1.1.1,1.0.0.1` or use other public DNS. 

| Architecture | Available |
| :----: | :----: |
| x86-64 | ✅ |
| amd64 | ✅ |
| aarch64 | ✅ |
| arm64v8 | ✅ |
| arm64v9 | ✅ |
| x86 | ❌ | |
| armhf | ❌ | |
| armv7 | ❌ | |

### Install Docker (Ubuntu, Debian, Armbian, DietPi...)
    sudo apt update && sudo apt install git vim wget curl net-tools ca-certificates gnupg -y
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    sudo apt update && sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
    sudo usermod -aG docker $USER
    sudo reboot

### Test Docker
    root@nanopi-neo3:~$ docker version
    Client: Docker Engine - Community
     Version:           27.3.1
     API version:       1.47
     Go version:        go1.22.7
     Git commit:        ce12230
     Built:             Fri Sep 20 11:41:19 2024
     OS/Arch:           linux/arm64
     Context:           default
    
    Server: Docker Engine - Community
     Engine:
      Version:          27.3.1
      API version:      1.47 (minimum version 1.24)
      Go version:       go1.22.7
      Git commit:       41ca978
      Built:            Fri Sep 20 11:41:19 2024
      OS/Arch:          linux/arm64
      Experimental:     false
     containerd:
      Version:          1.7.24
      GitCommit:        88bf19b2105c8b17560993bee28a01ddc2f97182
     runc:
      Version:          1.2.2
      GitCommit:        v1.2.2-0-g7cb3632
     docker-init:
      Version:          0.19.0
      GitCommit:        de40ad0
      
    root@nanopi-neo3:~$ docker compose version
    Docker Compose version v2.29.7

### Clone repo
    git clone https://github.com/azagramac/wireguard-docker.git
    cd wireguard-docker

### Running
    docker compose up -d

### Output
    $ docker compose up -d
    [+] Running 9/9
     ✔ wireguard Pulled                                                                                                                                                                                                                             23.2s 
       ✔ 646ff129efa7 Pull complete                                                                                                                                                                                                                  4.5s 
       ✔ df25a931801a Pull complete                                                                                                                                                                                                                  5.2s 
       ✔ c116abe7e7b3 Pull complete                                                                                                                                                                                                                  5.7s 
       ✔ ec142417d43e Pull complete                                                                                                                                                                                                                  5.9s 
       ✔ ef02aa7fa9ff Pull complete                                                                                                                                                                                                                 10.6s 
       ✔ 9ae179c60632 Pull complete                                                                                                                                                                                                                 10.9s 
       ✔ 0203081f93d0 Pull complete                                                                                                                                                                                                                 21.8s 
       ✔ 9b56ac8a03b4 Pull complete                                                                                                                                                                                                                 22.0s 
    [+] Running 2/2
     ✔ Network wireguard_default  Created                                                                                                                                                                                                            0.4s 
     ✔ Container wireguard        Started

### Check
    docker ps -a

### Output
    $ docker ps -a
    CONTAINER ID   IMAGE                                          COMMAND                  CREATED         STATUS                  PORTS                      NAMES
    eb8849811b3f   ghcr.io/linuxserver/wireguard:arm64v8-latest   "/init"                  2 minutes ago   Up About a minute       0.0.0.0:51820->51820/udp   wireguard

### Running on docker swarm 🐳
    cd wireguard-docker
    docker stack deploy --compose-file compose.yml wireguard

### Check on docker swarm 🐳
     $ docker service ls
     ID             NAME                   MODE         REPLICAS   IMAGE                                  PORTS                 
     dmbht3wp5asz   wireguard_vpn          replicated   1/1        ghcr.io/linuxserver/wireguard:latest   *:51820->51820/udp
     
     $ docker service ps wireguard_vpn
     ID             NAME              IMAGE                                  NODE      DESIRED STATE   CURRENT STATE               ERROR     PORTS
     t1gsvql9cage   wireguard_vpn.1   ghcr.io/linuxserver/wireguard:latest   master    Running         Running 44 hours ago

### Show QR config client 1, change number for show config client 2, 3... 
    docker exec -it wireguard /app/show-peer 1

### Monitor traffic from a connected client
    docker exec -it wireguard wg show

### Download App
<a href="https://play.google.com/store/apps/details?id=com.wireguard.android"><img src="https://lh3.googleusercontent.com/q1k2l5CwMV31JdDXcpN4Ey7O43PxnjAuZBTmcHEwQxVuv_2wCE2gAAQMWxwNUC2FYEOnYgFPOpw6kmHJWuEGeIBLTj9CuxcOEeU8UXyzWJq4NJM3lg=s0" width="130px"></a>  <a href="https://apps.apple.com/es/app/wireguard/id1441195209"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3c/Download_on_the_App_Store_Badge.svg/640px-Download_on_the_App_Store_Badge.svg.png" width="130px"></a>

<p align="center">
  <img src="https://github.githubassets.com/assets/mona-loading-default-c3c7aad1282f.gif" width="40" title="git">
</p>
