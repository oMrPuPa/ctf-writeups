## Xorry Kehapus
- file system == FAT16 == dapat direcover
![[Pasted image 20260623152211.png]]
- mencari file yang telah dihapus
	menggunakan command  `Fls -r forensic.img`
	![[Pasted image 20260623152313.png]]
	Dari hasil tersebut ditemukan 2 file .png  bertanda *  yang menunjukan bahwa file tersebut sudha dihapus
- extract hint.txt dan flag.txt `icat -r namafile kode`
	![[Pasted image 20260623152404.png]]
	![[Pasted image 20260623152417.png]]
- Karena filesystem FAT16 pada image tidak dapat diakses secara utuh dan file free.png terridentifikasi sebagai data mentah, aku melanjutkan analiss dengan mengugndakan metode file carving.
	![[Pasted image 20260623152629.png]]
- Menggunakan foremost untuk file carving memungkinkan ekstraksi file berdasarkan magic bytes png
	![[Pasted image 20260623152654.png]]
	![[Pasted image 20260623152711.png]]
- Xor kedua file tersebut menggunakan `StegSolve`
	![[Pasted image 20260623152749.png]] 
	![[Pasted image 20260623152815.png]]
- flag: `Hackfest0x09{4ku_ju9a_mau}`
	![[Pasted image 20260623152837.png]]