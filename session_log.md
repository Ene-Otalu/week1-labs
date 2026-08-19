┌──(kali㉿kali)-[~]
└─$ ls   
code.deb  Documents  Music     projects  prokects  Templates  Videos
Desktop   Downloads  Pictures  Projects  Public    test-node
                                                                        
┌──(kali㉿kali)-[~]
└─$ cd projects
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:5dd0d3e6e255913fc30f90b9f2b1d359cc2cbdb48090cc4b65f1676e203243cc
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ docker --version      
Docker version 28.5.2+dfsg4, build 9cc6dea35e9a963f281434761c656fba4ac43aed
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ trivy --version
Command 'trivy' not found, but can be installed with:
sudo apt install trivy
Do you want to install it? (N/y)y
sudo apt install trivy
[sudo] password for kali: 
Installing:                     
  trivy
                                                                        
Summary:
  Upgrading: 0, Installing: 1, Removing: 0, Not Upgrading: 1052
  Download size: 47.1 MB
  Space needed: 241 MB / 60.3 GB available

Get:1 http://kali.download/kali kali-rolling/main amd64 trivy amd64 0.66.0-0kali1 [47.1 MB]
Fetched 47.1 MB in 1min 53s (416 kB/s)                                 
Selecting previously unselected package trivy.
(Reading database… 468506 files and directories currently installed.)
Preparing to unpack …/trivy_0.66.0-0kali1_amd64.deb…
Unpacking trivy (0.66.0-0kali1)…
Setting up trivy (0.66.0-0kali1)…
Processing triggers for kali-menu (2026.2.6)…
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ winget install AquaSecurity.Trivy
Command 'winget' not found, did you mean:
  command 'widget' from deb perl-tk
Try: sudo apt install <deb name>
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ trivy --version        
Version: dev
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ sudo apt-get install -y wget gnupg apt-transport-https
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo gpg --dearmor -o /usr/share/keyrings/trivy.gpg
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install -y trivy
[sudo] password for kali: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
wget is already the newest version (1.25.0-3).
gnupg is already the newest version (2.4.9-7).
gnupg set to manually installed.
apt-transport-https is already the newest version (3.3.2+kali1).
Solving dependencies... Done
0 upgraded, 0 newly installed, 0 to remove and 1052 not upgraded.
gpg: no valid OpenPGP data found.
deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main
Ign:1 http://http.kali.org/kali kali-rolling InRelease                 
Ign:2 https://packages.microsoft.com/repos/code stable InRelease       
Ign:3 https://aquasecurity.github.io/trivy-repo/deb generic InRelease  
Ign:2 https://packages.microsoft.com/repos/code stable InRelease       
Ign:1 http://http.kali.org/kali kali-rolling InRelease                 
Ign:3 https://aquasecurity.github.io/trivy-repo/deb generic InRelease  
Ign:1 http://http.kali.org/kali kali-rolling InRelease                 
Ign:3 https://aquasecurity.github.io/trivy-repo/deb generic InRelease  
Ign:2 https://packages.microsoft.com/repos/code stable InRelease       
Err:3 https://aquasecurity.github.io/trivy-repo/deb generic InRelease  
  Temporary failure resolving 'aquasecurity.github.io'
Err:1 http://http.kali.org/kali kali-rolling InRelease                 
  Temporary failure resolving 'http.kali.org'
Err:2 https://packages.microsoft.com/repos/code stable InRelease       
  Temporary failure resolving 'packages.microsoft.com'
Reading package lists... Done            
W: Failed to fetch http://http.kali.org/kali/dists/kali-rolling/InRelease  Temporary failure resolving 'http.kali.org'
W: Failed to fetch https://aquasecurity.github.io/trivy-repo/deb/dists/generic/InRelease  Temporary failure resolving 'aquasecurity.github.io'
W: Failed to fetch https://packages.microsoft.com/repos/code/dists/stable/InRelease  Temporary failure resolving 'packages.microsoft.com'
W: Some index files failed to download. They have been ignored, or old ones used instead.
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
trivy is already the newest version (0.66.0-0kali1).
Solving dependencies... Done
0 upgraded, 0 newly installed, 0 to remove and 1052 not upgraded.
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ trivy --version                                       
Version: dev
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ wget https://github.com/aquasecurity/trivy/releases/download/v0.56.2/trivy_0.56.2_Linux-64bit.deb
sudo dpkg -i trivy_0.56.2_Linux-64bit.deb
--2026-08-18 09:55:07--  https://github.com/aquasecurity/trivy/releases/download/v0.56.2/trivy_0.56.2_Linux-64bit.deb
Resolving github.com (github.com)... failed: Temporary failure in name resolution.
wget: unable to resolve host address ‘github.com’
dpkg: error: cannot access archive 'trivy_0.56.2_Linux-64bit.deb': No such file or directory
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ 
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ ping -c 3 8.8.8.8        
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=64 time=98.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=64 time=153 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=64 time=102 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 98.803/118.255/153.468/24.944 ms
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ wget https://github.com/aquasecurity/trivy/releases/download/v0.56.2/trivy_0.56.2_Linux-64bit.deb
sudo dpkg -i trivy_0.56.2_Linux-64bit.deb
--2026-08-18 09:57:24--  https://github.com/aquasecurity/trivy/releases/download/v0.56.2/trivy_0.56.2_Linux-64bit.deb
Resolving github.com (github.com)... failed: Temporary failure in name resolution.
wget: unable to resolve host address ‘github.com’
dpkg: error: cannot access archive 'trivy_0.56.2_Linux-64bit.deb': No such file or directory
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ trivy --version
Version: dev
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ wget https://github.com/aquasecurity/trivy/releases/download/v0.56.2/trivy_0.56.2_Linux-64bit.deb
sudo dpkg -i trivy_0.56.2_Linux-64bit.deb
--2026-08-19 01:16:23--  https://github.com/aquasecurity/trivy/releases/download/v0.56.2/trivy_0.56.2_Linux-64bit.deb
Resolving github.com (github.com)... 140.82.121.4, 64:ff9b::8c52:7904
Connecting to github.com (github.com)|140.82.121.4|:443... connected.
HTTP request sent, awaiting response... 404 Not Found
2026-08-19 01:16:23 ERROR 404: Not Found.

[sudo] password for kali: 
dpkg: error: cannot access archive 'trivy_0.56.2_Linux-64bit.deb': No such file or directory
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin
aquasecurity/trivy info checking GitHub for latest tag
aquasecurity/trivy info found version: 0.74.0 for v0.74.0/Linux/64bit
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ trivy --version
Version: dev
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin
aquasecurity/trivy info checking GitHub for latest tag
aquasecurity/trivy info found version: 0.74.0 for v0.74.0/Linux/64bit
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ curl -s https://api.github.com/repos/aquasecurity/trivy/releases/latest | grep "browser_download_url.*Linux-64bit.deb"
      "browser_download_url": "https://github.com/aquasecurity/trivy/releases/download/v0.74.0/trivy_0.74.0_Linux-64bit.deb"
      "browser_download_url": "https://github.com/aquasecurity/trivy/releases/download/v0.74.0/trivy_0.74.0_Linux-64bit.deb.sigstore.json"
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ docker run -d -p 8080:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
26c307b5e35a: Pull complete 
3c55dc422a81: Pull complete 
d84ae7b21412: Pull complete 
c0df8d325117: Pull complete 
b8b80b9bc028: Pull complete 
f5de6e85ac74: Pull complete 
5a4222b844e8: Pull complete 
Digest: sha256:8541484afbc9c8a5a8a99b379568ebbc957f658583ec9448fc43104229c03cf8
Status: Downloaded newer image for nginx:latest
ea7e1218ac3c381978b4cbd96ff3a90f2f61fad72b4d8b28479da80db9ff47c8
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ docker ps                     
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
ea7e1218ac3c   nginx     "/docker-entrypoint.…"   26 minutes ago   Up 26 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   modest_beaver
                                                                        
┌──(kali㉿kali)-[~/projects]
└─$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS                    PORTS                                     NAMES
ea7e1218ac3c   nginx         "/docker-entrypoint.…"   31 minutes ago   Up 31 minutes             0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   modest_beaver
b7d5b6652087   hello-world   "/hello"                 18 hours ago     Exited (0) 18 hours ago                                             kind_villani
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker stop      
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker stop ea7e1218ac3c             
ea7e1218ac3c
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker stop nginx        
Error response from daemon: No such container: nginx
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker stop                                           
docker: 'docker stop' requires at least 1 argument

Usage:  docker stop [OPTIONS] CONTAINER [CONTAINER...]

See 'docker stop --help' for more information
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker start ea7e1218ac3c  
ea7e1218ac3c
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker rm b7d5b6652087        
b7d5b6652087
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker ps -a           
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS          PORTS                                     NAMES
ea7e1218ac3c   nginx     "/docker-entrypoint.…"   About an hour ago   Up 25 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   modest_beaver
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker images
REPOSITORY      TAG       IMAGE ID       CREATED        SIZE
aquasec/trivy   latest    1105aaf5e722   4 days ago     190MB
nginx           latest    5253dc86cc93   2 weeks ago    161MB
hello-world     latest    e2ac70e7319a   4 months ago   10.1kB
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker log e2ac70e7319a
docker: unknown command: docker log

Run 'docker --help' for more information
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker logs e2ac70e7319a
Error response from daemon: No such container: e2ac70e7319a
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker logs 5253dc86cc93
Error response from daemon: No such container: 5253dc86cc93
                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$ docker --version
docker compose version
sudo systemctl status docker
Docker version 28.5.2+dfsg4, build 9cc6dea35e9a963f281434761c656fba4ac43aed
Docker Compose version 2.40.3-3
[sudo] password for kali: 
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-08-18 08:28:52 EDT; 23h ago
 Invocation: 10c7d16d9d8d42ab889e4d50f62ef0ca
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 735 (dockerd)
      Tasks: 25
     Memory: 105M (peak: 322.6M, swap: 5.8M, swap peak: 5.8M)
        CPU: 26min 41.327s
     CGroup: /system.slice/docker.service
             ├─   735 /usr/sbin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
             ├─105417 /usr/sbin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 8080 -container>
             └─105423 /usr/sbin/docker-proxy -proto tcp -host-ip :: -host-port 8080 -container-ip 1>

Aug 18 08:28:49 kali dockerd[735]: time="2026-08-18T08:28:49.659802032-04:00" level=info msg="Loadi>
Aug 18 08:28:52 kali dockerd[735]: time="2026-08-18T08:28:52.462242637-04:00" level=info msg="Loadi>
Aug 18 08:28:52 kali dockerd[735]: time="2026-08-18T08:28:52.757303943-04:00" level=info msg="Docke>
Aug 18 08:28:52 kali dockerd[735]: time="2026-08-18T08:28:52.758970904-04:00" level=info msg="Initi>
Aug 18 08:28:52 kali dockerd[735]: time="2026-08-18T08:28:52.803460750-04:00" level=info msg="Compl>
Aug 18 08:28:52 kali dockerd[735]: time="2026-08-18T08:28:52.825442579-04:00" level=info msg="Daemo>
Aug 18 08:28:52 kali dockerd[735]: time="2026-08-18T08:28:52.825577316-04:00" level=info msg="API l>
Aug 18 08:28:52 kali systemd[1]: Started docker.service - Docker Application Container Engine.
Aug 18 08:35:01 kali dockerd[735]: time="2026-08-18T08:35:01.495713588-04:00" level=info msg="ignor>
Aug 19 02:18:05 kali dockerd[735]: time="2026-08-19T02:18:05.411772556-04:00" level=info msg="ignor>

                                                                                                    
┌──(kali㉿kali)-[~/projects]
└─$  git clone https://github.com/travis-wayne/week1-labs.git
cd week1-labs
docker compose up -d
docker ps
Cloning into 'week1-labs'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 9 (delta 2), reused 5 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (9/9), 87.89 KiB | 86.00 KiB/s, done.
Resolving deltas: 100% (2/2), done.
WARN[0000] /home/kali/projects/week1-labs/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 23/23
 ✔ postgres_db Pulled                                                                         94.5s 
   ✔ 26c307b5e35a Already exists                                                               0.0s 
   ✔ 32a162df1425 Pull complete                                                               25.5s 
   ✔ 05f63dbab933 Pull complete                                                               28.0s 
   ✔ 0418a1024c20 Pull complete                                                               28.4s 
   ✔ 4c85fe314a1e Pull complete                                                               34.9s 
   ✔ 3220d19f365a Pull complete                                                               35.2s 
   ✔ a4edcba0bccb Pull complete                                                               35.2s 
   ✔ 82bf5df0bf96 Pull complete                                                               35.3s 
   ✔ ecf4aa421db4 Pull complete                                                               86.8s 
   ✔ bb6f17b37753 Pull complete                                                               86.9s 
   ✔ cd4386761970 Pull complete                                                               86.9s 
   ✔ 0b6b1ca76eeb Pull complete                                                               87.0s 
   ✔ 63b7c3ab652e Pull complete                                                               87.1s 
   ✔ aaf87c8aff5f Pull complete                                                               87.1s 
 ✔ redis_cache Pulled                                                                         41.5s 
   ✔ 039e6f9f9752 Pull complete                                                               23.0s 
   ✔ 5b03f5a6cdec Pull complete                                                               23.1s 
   ✔ ced91743e468 Pull complete                                                               23.1s 
   ✔ 709eacfa0183 Pull complete                                                               34.0s 
   ✔ bd9e4bd718ad Pull complete                                                               34.0s 
   ✔ 4f4fb700ef54 Pull complete                                                               34.1s 
   ✔ c846c34d5449 Pull complete                                                               34.1s 
[+] Running 5/5
 ✔ Network week1-labs_isolated_backend  Created                                                0.4s 
 ✔ Volume week1-labs_redis_data         Created                                                0.0s 
 ✔ Volume week1-labs_pg_data            Created                                                0.0s 
 ✔ Container hardened_postgres          Started                                                1.6s 
 ✔ Container hardened_redis             Started                                                1.6s 
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS                  PORTS                                     NAMES
a5a2cf7311f6   postgres:15   "docker-entrypoint.s…"   2 seconds ago   Up Less than a second   5432/tcp                                  hardened_postgres
3aac991ea36a   redis:7       "docker-entrypoint.s…"   2 seconds ago   Up Less than a second   6379/tcp                                  hardened_redis
ea7e1218ac3c   nginx         "/docker-entrypoint.…"   6 hours ago     Up 6 hours              0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   modest_beaver
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$  git config --global user.name "Ene Rita Otalu" 
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$  git config --global user.email "otaluene@gmail.com"        
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git remote -v 
origin  https://github.com/travis-wayne/week1-labs.git (fetch)
origin  https://github.com/travis-wayne/week1-labs.git (push)
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git remote set-url origin https://github.com/otaluene/week1-labs.git
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': Ene-Otalu
Password for 'https://Ene-Otalu@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/otaluene/week1-labs.git/'
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': Ene Rita Otalu
Password for 'https://Ene%20Rita%20Otalu@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/otaluene/week1-labs.git/'
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': otlauene@gmail.com
Password for 'https://otlauene%40gmail.com@github.com': 
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': otaluene@gmail.com
Password for 'https://otaluene%40gmail.com@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/otaluene/week1-labs.git/'
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': Ene-Otalu
Password for 'https://Ene-Otalu@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/otaluene/week1-labs.git/'
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': Ene-Otalu
Password for 'https://Ene-Otalu@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/otaluene/week1-labs.git/'
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': 
Password for 'https://github.com': 
remote: Repository not found.
fatal: Authentication failed for 'https://github.com/otaluene/week1-labs.git/'
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': Ene-Otalu
Password for 'https://Ene-Otalu@github.com': 
remote: Repository not found.
fatal: repository 'https://github.com/otaluene/week1-labs.git/' not found
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': Ene-Otalu
Password for 'https://Ene-Otalu@github.com': 
remote: Repository not found.
fatal: repository 'https://github.com/otaluene/week1-labs.git/' not found
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': https://github.com/Ene-Otalu
Password for 'https://https%3A%2F%2Fgithub.com%2FEne-Otalu@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/otaluene/week1-labs.git/'
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git remote -v 
origin  https://github.com/otaluene/week1-labs.git (fetch)
origin  https://github.com/otaluene/week1-labs.git (push)
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': Ene-Otalu
Password for 'https://Ene-Otalu@github.com': 
remote: Repository not found.
fatal: repository 'https://github.com/otaluene/week1-labs.git/' not found
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git remote set-url origin https://github.com/Ene-Otalu/week1-labs-notes.git
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ git push origin main
Username for 'https://github.com': Ene-Otalu
Password for 'https://Ene-Otalu@github.com': 
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 2 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (9/9), 87.89 KiB | 21.97 MiB/s, done.
Total 9 (delta 2), reused 9 (delta 2), pack-reused 0 (from 0)
To https://github.com/Ene-Otalu/week1-labs-notes.git
 * [new branch]      main -> main
                                                                                                    
┌──(kali㉿kali)-[~/projects/week1-labs]
└─$ 
