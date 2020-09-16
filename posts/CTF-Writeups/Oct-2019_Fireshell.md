##### <h1>Idiot_Connection</h1>

We are Provided With A Packet Capture File Full Of ICMP Packets,But Actually They Contains HTTP and Other Packets Too..! What They Have Done Is They Added ICMP Packet To Every Packet.
So We Need To Slice That Portion To Get Original Pcap File.

So Using "editcap" A Command Line Tool For Editing Pcap Files


````$ editcap -C 14:33 -F pcap "chall.pcap" "edited.pcap"````

-C Chopping (Slicing And Removing That Part)

-F File Type

Now Openup the edited capture file, now you can see actual packets.Concentrate On HTTP Packets and Export the Items That Are Tranferred.Export HTTP packets ```file > export objects > HTTP```.


You'll find a "msg file"(ZIP) With Wrong File Signature `F#(46 23)` So Replace It With `PK(50 4B)`.

Try To Extract The Zip.Actually It's A Password Protected Zip.


Try Dictionary Attack On Zip Using Rockyou.txt

```
$ fcrackzip -v -D -u -p rockyou.txt msg.zip
found file 'photo.png', (size cp/uc 924401/924244, flags 9, chk b135)
checking pw 055469215                               

PASSWORD FOUND!!!!: pw ==   b1tch3s  
```

``Password="   b1tch3s  "`` Now The Password For The Zip Is "b1tch3s"(2 Spaces in the begining nd in the end)

Extract The Zip You'll Get An Image photo.png.

Try Hexdump.......

 
 ````
 $ hexdump -C ext.img
          07 7c f2 41 dd 6b 05 d6  6b 00 00 00 00 49 45 4e  |.|.A.k..k....IEN|
000e1a20  44 ae 42 60 82 41 00 6c  00 6d 00 6f 00 73 00 74  |D.B`.A.l.m.o.s.t|
000e1a30  00 20 00 74 00 68 00 65  00 72 00 65 00 2c 00 52  |. .t.h.e.r.e.,.R|
000e1a40  00 79 00 61 00 6e 00 20  00 47 00 69 00 62 00 73  |.y.a.n. .G.i.b.s|
000e1a50  00 6f 00 6e                                       |.o.n|
````

Hexdump Of Image Gives U "Almost there Ryan Gibson"

After Googling This You'll Find The git Link of Ryan Gibson on LSB (Link:https://github.com/ragibson/Steganography)

Now Using LSB Extract Image.

```
 $  python3 LSBSteg.py -r -i photo.png -o ext.png
Reading files...                   Done in 0.42 s
Recovering 95404 bytes...          Done in 0.08 s
Writing to output file...          Done in 0.00 s
```
Now We've an Image With No Flag.

Finally Tried To Enlarge The Image. Change Length(24th Byte) in PNG Chunk i.e, 0F to 3F.

As The Length Changes, then the corresponding CRC data changes.

So if u try to open the image,you'll get problem with CRC.  

````
$ pngcheck ext.png
ext.png  CRC error in chunk IHDR (computed pngcheck ext.png
ext.png  CRC error in chunk IHDR (computed 1d71bc38, expected 190bbb95)
ERROR: ext.png
````

Replace CRC(From 30th byte to 33rd byte) `19 0B BB 95` with `1D 71 BC 38`.

WOW...! Here We've The Flag in The End Of The Image.

``F#{1cMp_tUnN3l_4Nd_ST3go_Rul35_!!!}``


