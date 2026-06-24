# CCUG Portal
![[Pasted image 20260623142434.png]]
### Foothold:
- user : Hackfesxt0x09
- dre4mer : CCUG-dre4mer
### Web-Enum:
- diurl profile page terdapat parameter `profile?id=100` ==> id user
![[Pasted image 20260623143207.png]]
profile id bisa diganti ke id dengan user dre4mer`profile?id=101` ==> id dre4mer.

vuln: IDOR
IDOR adalah salah satu tipe vulnerability hak akses, yang terjadi ketika applikasi mengizinkan user untuk menginput _access Object_ secara langsung. (portswigger IDOR)

### Exploit
mengubah `profile?id=0` untuk mengakses profile admin, dan dapat flagnya.
![[Pasted image 20260623143142.png]]
