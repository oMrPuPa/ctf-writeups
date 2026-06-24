# Library
Desc:
	boot2root machine for FIT and bsides guatemala CTF.
Goal:
- user.txt
- root.txt

# Pwning
## Enumeration
### Port Scanning
```bash
nmap -sS -p- -v TARGET.IP
```
terdapat 2 port yang _open_:
- tcp port 22 dengan service ssh
- tcp port 80 dengan service http
[Open: Pasted image 20260624181517.png](Practice/TryHackMe/Library%20chall/assets/dd7f9a6b6745ab71b3d961fb86d73e82_MD5.jpg)
![](Practice/TryHackMe/Library%20chall/assets/dd7f9a6b6745ab71b3d961fb86d73e82_MD5.jpg)
### Web Enumeration
diweb ini terpampang username pemilik blog ini yaitu: `meliodas`.
[Open: Pasted image 20260624182155.png](Practice/TryHackMe/Library%20chall/assets/06fa9e79e936eb2a11524eb489dbad0a_MD5.jpg)
![425](Practice/TryHackMe/Library%20chall/assets/06fa9e79e936eb2a11524eb489dbad0a_MD5.jpg)

Karena tidak ada yang menarik lagi di page utamanya, maka  dari itu penulis mencoba mencari directory tersembunyi untuk memperluas daerah serangan.
```bash
gobuster dir -u http://TARGET.IP -w /usr/share/seclists/Discovery/Web-Content/common.txt
```
- robots.txt ==> 200

cek TARGET.IP/robots.txt terdapat hint `user-agent: rockyou ; Disallowed /` 

karena hintnya mengarah untuk bruteforce jadi penulis langsung bruteforce service ssh dengan informasi username yang sudah didapatkan sebelumnya

```bash
hydra -l meliodas -p /usr/share/wordlists/rockyou.txt TARGET.IP ssh
```

[Open: Pasted image 20260624182736.png](Practice/TryHackMe/Library%20chall/assets/530bc481d348eeccfb7a409589d218ef_MD5.jpg)
![](Practice/TryHackMe/Library%20chall/assets/530bc481d348eeccfb7a409589d218ef_MD5.jpg)

### Foothold
login: meliodas
password: iloveyou1

### System Enumeration
setelah login ke SSH dengan creds yang didapatkan, terdapat file `user.txt` dan `bak.py`.
user.txt: 6d488cbb3f111d135722c33cb635f4ec

penulis mencoba melihat hak akses sudo:
```bash
sudo -l
```
dan terdapat binary /usr/bin/python* yang memiliki hak akses root (ALL) NOPASSWD untuk mengakses file /home/meliodas/bak.py yagn berarti user berpotensi bisa megnakses binary ini dengan akses root.

[Open: Pasted image 20260624183141.png](Practice/TryHackMe/Library%20chall/assets/dcc37a242eda0b7d9213db07f9738c63_MD5.jpg)
![](Practice/TryHackMe/Library%20chall/assets/dcc37a242eda0b7d9213db07f9738c63_MD5.jpg)

tetapi file  user biasa tidak dapat akses Write pada file `bak.py`. 
[Open: Pasted image 20260624183414.png](Practice/TryHackMe/Library%20chall/assets/72a74c0542fc90586e7fad8c75931ff5_MD5.jpg)
![](Practice/TryHackMe/Library%20chall/assets/72a74c0542fc90586e7fad8c75931ff5_MD5.jpg)

penulis mencoba untuk mereplace file asli `bak.py` dengna file `bak.py` palsu dengan mengganti nama file utama `bak.py` menjadi ==> `bak2.py` dan membuat file baru `bak.py` dengan payload untuk mengaktifkan shell dengan akses root.

[Open: Pasted image 20260624183729.png](Practice/TryHackMe/Library%20chall/assets/1cab19ae9987093d92990ccc5379abb1_MD5.jpg)
![](Practice/TryHackMe/Library%20chall/assets/1cab19ae9987093d92990ccc5379abb1_MD5.jpg)

kemudian penulis mencoba menjalankan file palsu `bak.py` dengan perintah `sudo /usr/bin/python /home/meliodas/bak.py`

dan yap berhasil.
[Open: Pasted image 20260624183914.png](Practice/TryHackMe/Library%20chall/assets/89f9ac2449850d36e12bec79a944579d_MD5.jpg)
![](Practice/TryHackMe/Library%20chall/assets/89f9ac2449850d36e12bec79a944579d_MD5.jpg)
- `python3 -c 'import pty;pty.spawn("/bin/bash")` untuk spawn shell `bash` agar lebih interaktif saja.

langsung saja deh tinggal grab root.txtnya
[Open: Pasted image 20260624184040.png](Practice/TryHackMe/Library%20chall/assets/0cff478b0140024947002c2ece32233e_MD5.jpg)
![](Practice/TryHackMe/Library%20chall/assets/0cff478b0140024947002c2ece32233e_MD5.jpg)

root.txt: e8c8c6c256c35515d1d344ee0488c617