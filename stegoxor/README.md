steps:
ran strings on the file, which revealed minimal useful data
ran binwalk, which revealed a zip file embedded at the end of the image
compared strings and binwalk results, as well as relative file sizes, against a similarly large (pixel-wise) JPEG found on the internet. "control"
ran a passwordless steghide extract -sf on the stego.jpeg, releasing the embedded tar file found during the binwalk
tar -xf files.tar, revealing the HACKER.TXT and qr.xor files
installed a xor tool from GitHub (https://github.com/hellman/xortool), and ran file-file XOR using that tool: xortool-xor -h -f HACKER.TXT -f qr.xor > xored.qr.xor, which revealed the (first) QR code embedded in the stego image. The reasoning here was Chekhov's Gun: the HACKER.TXT file was probably put in for a reason, but, being a bog-standard document, it likely was intended as an XORing file.
read the blurry xored.qr.xor using an online QR reader, and copied the result, once we realized it was legitimate output from the QR code: base64 data we called "nextstep.maybepng".
base64 -d nextstep.maybepng > newqr.code revealed that the base64 was in fact a png of another QR code.
rinse and repeat: newqr.code displayed another base 64 data chunk, which had another chunk of data we named third.code, which was a gzip compressed file
gunzip third.code to a file called wheelsinwheels.newqr
wheelsinwheels.newqr is a text file, but it displays a 'micro QR' code.
Finally, we found an online site which was capable of decoding micro QR codes. The data in THAT QR code finally had the flag. :)



along the way, we took a few side turns that turned out to be irrelevant.
-the first was considering the byte string "0b 1b 17 0c" within the original file name. Since it was seemingly intentionally added to the file, looking very unlike other challenge file names (excaped characters), and was 4 bytes of low-value hex (0x0X or 0x1X), it seemed likely that the entire image had steganography data within it through slight color offsets. JPEGs are typically 3-byte RGB, but can be stored as 4-byte CMYK; such a mask could hide data with an XOR across the entire viewable area of the image. This didn't turn out to be the case, of course. Similarly, we tried XORing that 4-byte string against qr.xor at first.
-Reading the first QR code threw us for a loop, because at first we thought its blurriness was due to another XOR possibly needed, and tried "0b 1b 17 0c" on it again. Turned out it was a combo of a bad QR code reader and our missing the meaning of the QR code's output...at first :)
-the strings command on the JPEG revealed the possibly useful string "N*Wft!bo3fN	9", which looked like a password for possible steghide decryption, but was ultimately coincidental.
