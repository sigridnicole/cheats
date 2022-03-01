
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


**Install Python 3 on Ubuntu** 

[This](https://phoenixnap.com/kb/how-to-install-python-3-ubuntu) worked for me. 





### MongoDB Things


**Create New Connection**

This code snippet can support multiple database connections.

```
function makeNewConnection(dbName, uri) {

  const db = mongoose.createConnection(uri, {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  });

  db.on('error', function (error) {
    console.log(`${dbName} MongoDB :: connection ${this.name} ${JSON.stringify(error)}`);
    db.close().catch(() => console.log(`MongoDB :: failed to close connection ${this.name}`));
  });

  db.on('connected', function () {
    mongoose.set('debug', function (col, method, query, doc) {
      console.log(`${dbName} MongoDB :: ${this.conn.name} ${col}.${method}(${JSON.stringify(query)},${JSON.stringify(doc)})`);
    });
    console.log(`${dbName} MongoDB :: connected ${this.name}`);
  });

  db.on('disconnected', function () {
    console.log(`${dbName} MongoDB :: disconnected ${this.name}`);
  });

  return db;
}

const dbConnection = makeNewConnection('testDB', dbConfig.url);
```




### NodeJS Things


**Host Images Using Express**

app.use(express.static('folder location'));



### Git Things

**Undo last pushed commit but keep changes in staging**

*This will rewrite git history - use with a grain of salt.*
```
git reset --soft HEAD~1
git push -f branch
```
**Clean Push Using Git Stash**

Applicable when working with forked repos

*Goal*

Push code from origin to upstream without extra merge commits. Like "rebasing" but for forked repos.

*Note*

Look for an easier version of these steps. 

*Setup*

Original Repo remote: upstream
Forked Repo remote: origin
 
 *Instructions*
 
 Forked Repo: stash current changes
 ```
 git add .
 git stash
 ```
 
 Update upstream branch
 ```
 git fetch upstream
 ```

Checkout fetched upstream branch. This checks out as a detached head of the branch in the upstream repo. No need to name the branch, the purpose is to just get the latest version of the upstream branch.
```
git checkout upstream/target-branch
```

Verify that the latest version has been fetched.
```
git log
```

Delete current origin branch
```
git branch -D target-branch
```

Checkout the latest code from the detached branch
```
git checkout -b target-branch
```

Re-add the stashed changes
```
git stash pop
git add .
git commit
git push origin target-branch -f
```
