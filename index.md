## Welcome to Sigrid Cheats lol 🤣

Personal Notes I know I will most likely forget. 

### Linux

**chmod 400 equivalent for Windows**

In powershell, navigate to pem file directory then execute the following commands:

```
icacls.exe key.pem /reset
icacls.exe key.pem /grant:r "$(env:username)"(r)"
icacls.exe key.pem /inheritance:r
```

For per command explanation, watch this [video](https://www.youtube.com/watch?v=P1erVo5X3Bs)
