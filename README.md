# Intruction to access via ssh to a server proxyed by Cloudflare

On Linux:

* install cloudflared on your local machine

``` bash

curl -fsSL https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -o cloudflared
chmod +x cloudflared
sudo mv cloudflared /usr/local/bin/

```

* prompt
  
```
ssh -o ProxyCommand="cloudflared access ssh --hostname ssh.domain.com" user@ssh.username.com -p portnumber
```
  
* or, in order to avoid to use every time the above command, edit ```~/.ssh/config```

```
Host ssh.domain.com
  Hostname ssh.domain.com
  ProxyCommand cloudflared access ssh --hostname %h
  Port portnumber
  User username

```

* connect 

``` bash
ssh username@ssh.domain.com
```

On Windows:

1. install cloudflared downloading ``` cloudflared-windows-amd64.exe ``` from [here](https://github.com/cloudflare/cloudflared/releases/latest)
2. rename it ``` cloudflared.exe ```
3. move it to ``` C:\Program Files\Cloudflared\ ```
4. add ``` C:\Program Files\Cloudflared\ ``` to your System PATH (optional for easier use)
5. prompt in a command prompt(```cmd.exe```) or powershell:
   
   ```
   ssh -o ProxyCommand="C:\Program Files\Cloudflared\cloudflared.exe access ssh --hostname ssh.domain.com" user@ssh.domain.com -p portnumber
   ```
Or, in order to avoid to use every time the above command:
   
* edit ``` C:\Users\your-username\.ssh\config ```, if the file doesn’t exist, create it and add:
   
   ```
    Host ssh.domain.com
    Hostname ssh.domain.com
    ProxyCommand "C:\Program Files\Cloudflared\cloudflared.exe" access ssh --hostname %h
    User username
    Port portnumber 

   ```
* open command prompt (```cmd.exe```) or powershell and prompt:

   ```
    ssh username@ssh.domain.com
   
   ```


