IRQHack64 Kaynak kodlar� i�in a��klama
- May�s 2016 / I.R.on

Arduino klas�r�nde kullan�lan SdFat k�t�phanesi ve IRQHack64 sketch'i mevcut. Sketch Arduino'nun �u an en son s�r�m� olan 1.6.8 s�r�m� ile test edildi (1.6.3 ile geli�tirildi). Arduino sketch'i i�indeki FlashLib.h dosyas� C64'e g�nderilen men� program�n�n binary'sini i�eriyor. Men�n�n kaynak kodlar� de�i�tirilip yenisi �retildi�inde bu da de�i�tirilmeli. 


Tools klas�r�nde men� ve loader'�n olu�turulmas� i�in gerekli ara�lar�n bir b�l�m� ve IrqHackSend seri porttan program g�nderme tool'u mevcut.
- Bin2ArdH.exe - Binary dosyay� C header'� haline d�n��t�ren bir program. Benzer programlardan fark� olu�turulan diziyi PROGMEM olarak i�aretlemesi, b�ylece dizinin sadece flash'ta saklanmas� sa�lan�yor.
- CreateEpromLoader.exe - 64IRQTransferSoftNewForC64Fast.65s'den �retilen 256 byte'l�k esas loader'� 256 defa duplike eden program. 
�rn. Kullan�m �ekli : CreateEpromLoader.exe infile outfile 160 191
Burada 160 ve 191 loader i�inde 0'dan 255'e kadar say�larla de�i�tirilmesi gereken pozisyonlar� ifade ediyor.
- IRQHackSend.exe - C64'e pc �st�nden seri ba�lant� ile program g�ndermeye yarayan �rnek program. Pc ile IRQHack64 aras�nda seri ba�lant� sa�land�ktan sonra �rnek olarak a�a��daki gibi kullan�labilir. Kullan�lan baud rate : 57600
IRQHackSend.exe commando.prg COM3

C64 klas�r�nde men� ve loader'�n source'lar� mevcut,
Dosyalar�n a��klamalar� �u �ekilde,

- IRQLoader.65s - IRQHack64 �zerinde bulunan eprom'da �al��an loader'�n kaynak kodu.
- LoaderStub.65s - Y�kleme yap�ld�ktan sonra kaset buffer'�na at�lan y�klenen program� �al��t�ran k�s�m.
- IrqLoaderMenuNew.65s - IRQHack64 sketch'ine g�m�len c64 men�s�n�n kaynak kodu.
- IrqLoaderMenu.bas - Men�n�n ba��na eklenen basic �ny�kleyici sat�r�
- avrincludehead.txt - Flashlib.h'� olu�turan ilk k�s�m
- avrincludefoot.txt - Flashlib.h'� olu�turan son k�s�m
- Build - I_R_on.bat veya Build - Wizofwor.bat - Loader ve men�y� olu�turmak i�in kullan�lan batch dosya. C64 kodunu derleyebilmek i�in path �st�nde 64tass ve petcat (vice ile beraber geliyor) programlar� olmal�.
Batch dosya �al��t���nda temel olarak 3 adet ��kt� �retiyor
- PreBuild.bat, PostBuild.bat - �stteki iki ayr� men� i�in ba�ta ve sonda ortak kullan�lan i�lemler
- irqhack64.prg - Build sonras� sd kart'a at�lmas� gereken men� dosyas�
- Flashlib.h - Arduino sketch'i i�ine aktar�lacak kodun c header'� haline getirilmi� hali.
- IRQLoaderRom.bin - 27C512 Eprom'a yaz�lacak loader. 