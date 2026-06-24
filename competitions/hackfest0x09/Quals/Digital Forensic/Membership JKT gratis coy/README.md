## Membership JKT gratis coy
![[Pasted image 20260623153002.png]]
### Enumeration
Chall ini menyediakan 2 file yaitu:
1. File .jpg yang sudah dienkripsi (oshi.jpg.enc)
2. File .pcapng (output.pcapng)

- file output.pcapng
	Setelah aku skimming dari awal sampe akhir file output.pcap ini hanya berisi proses user request http untuk mendapatkan filenya
	![[Pasted image 20260623153145.png]]
- export object
	Terdapat 9 file hmmm ada 1 file mencurigakan kemungkinan besar malwernya itu dari membership_jkt48
	![[Pasted image 20260623153218.png]]
	![[Pasted image 20260623153255.png]]
- follow http stream
	Hmm… sus membership gratis ngapain buka buka file dan direktori.
	![[Pasted image 20260623153355.png]]
	![[Pasted image 20260623153434.png]]
- menganalisis file membership_jkt48 dengan ghidra
	dan indeed file ini mengakses/memanipulasi file.Ternyata benar file ini mengakses  direktori yang sedang dibuka untuk mengenkripsi file yang ada didirektori tersebut, dan terdapat key = S3kte_p3Muj4_05ha_0sh1
	![[Pasted image 20260623153543.png]]
- Malware mengenkripsi dengan cara xor
	![[Pasted image 20260623153619.png]]
### mencoba crack data
- membuat script untuk crack dengan membalik logika malwarenya
	![[Pasted image 20260623153756.png]]
- foto dah balik
	![[Pasted image 20260623153817.png]]
- tinggal jawab jawabin pertanyaan yang ada di netcat deh untuk mendapatkan flagnya
	![[Pasted image 20260623153904.png]]
	![[Pasted image 20260623153925.png]]