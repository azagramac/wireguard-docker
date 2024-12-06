[![GitHub Release](https://img.shields.io/github/release/linuxserver/docker-wireguard.svg?color=88171a&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=wireguard)](https://github.com/linuxserver/docker-wireguard/releases)

<p align="center">
  <img src="https://github.com/AzagraMac/wireguard-docker/assets/571796/d0c3ac2a-1c2d-46a1-bc4d-648d0cafa3a2" width="400" title="logo_wg">
</p>

### Requeriments
- Service docker running
- Open port 51820 UDP on the router (you can customize a port)
  
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

### Install Docker (Ubuntu, Debian...)
    sudo apt update && sudo apt upgrade -y
    sudo apt install git vim wget curl net-tools ca-certificates gnupg
    curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    echo  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
	"$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt update
    sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
    sudo usermod -aG docker $USER
    sudo apt install docker-compose-plugin -y

### Test Docker
    $ docker version
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
	  Version:          1.7.23
	  GitCommit:        57f17b0a6295a39009d861b89e3b3b87b005ca27
	 runc:
	  Version:          1.1.14
	  GitCommit:        v1.1.14-0-g2c9f560
	 docker-init:
	  Version:          0.19.0
	  GitCommit:        de40ad0

    $ docker compose version
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

### Show QR config client 1, change number for show config client 2, 3... 
    docker exec -it wireguard /app/show-peer 1

### Monitor traffic from a connected client
    docker exec -it wireguard wg show

### Download App
<a href="https://play.google.com/store/apps/details?id=com.wireguard.android"><img src="https://lh3.googleusercontent.com/q1k2l5CwMV31JdDXcpN4Ey7O43PxnjAuZBTmcHEwQxVuv_2wCE2gAAQMWxwNUC2FYEOnYgFPOpw6kmHJWuEGeIBLTj9CuxcOEeU8UXyzWJq4NJM3lg=s0" width="130px"></a>  <a href="https://apps.apple.com/es/app/wireguard/id1441195209"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3c/Download_on_the_App_Store_Badge.svg/640px-Download_on_the_App_Store_Badge.svg.png" width="130px"></a>
