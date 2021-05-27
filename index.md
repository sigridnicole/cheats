## Welcome to Sigrid Cheats lol 🤣

Personal Notes I know I will most likely forget. 

### Linux

**chmod 400 equivalent for Windows**

In powershell, navigate to pem file directory then execute the following commands:

```
icacls.exe key.pem /reset
icacls.exe key.pem /grant:r "$($env:username):(r)"
icacls.exe key.pem /inheritance:r
```

For per command explanation, watch this [video](https://www.youtube.com/watch?v=P1erVo5X3Bs)


**pm2**

PM2 is a production process manager for Node.js applications with a built-in load balancer. You can start any application (Node.js, Python, Ruby .. etc)

Install pm2

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install pm2 -g
pm2 ls

should show something like this
┌──────────┬────┬─────────┬──────┬─────┬────────┬─────────┬────────┬─────┬─────┬──────────┐
│ App name │ id │ version │ mode │ pid │ status │ restart │ uptime │ cpu │ mem │ watching │
└──────────┴────┴─────────┴──────┴─────┴────────┴─────────┴────────┴─────┴─────┴──────────┘
 Use `pm2 show <id|name>` to get more details about an app
```

Start an app

```
pm2 start app.js
```

```
pm2 start app.py
```

List Apps

```
pm2 ls
```

Check logs
```
pm2 logs
```

Manage App State
```
pm2 stop hello
restart hello
pm2 delete hello
```


[More info](https://pm2.io/)   ||  [Manage Python Processes with PM2](https://pm2.io/blog/2018/09/19/Manage-Python-Processes)



