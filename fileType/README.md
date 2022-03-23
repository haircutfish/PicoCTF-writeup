# File Type
### PicoCTF 2022
### category:Forensics
3-22-2022

Author:Dan Rearden

## Description
This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can. You can download the file from [here](https://artifacts.picoctf.net/c/329/Flag.pdf).

### Hint: Remember that some file types can contain and nest other files

### You need to run these commands below because you will need different types of decryption and decompression

sudo apt-get install lz4

sudo apt-get install lzip

sudo apt-get install sharutils

sudo apt-get install 7zip

sudo apt-get install lzop



1. __nano Flag.pdf__
* _see Flag.pdf for contents_

2. __Then I saved the file as, Flag.__

3. __sh Flag__

  *x - created lock directory _sh00046.
  
  *x - extracting flag (text)
  
  *x - removed lock directory _sh00046.

  * This runs the file and decrypts it into a file named flag
  
  * running file flag: current ar archive
  

4. __Created a new directory, flagdir, cd flagdir__

5. __cpio -idv < ../flag__
  
  *flag
  *2 blocks

  * File created: flag
  
  * running file on flag: bzip2 compressed data, block size = 900k

6. __sudo bzip2 -d flag__

  *bzip2: Can't guess original name for flag -- using flag.out

  * File created: flag.out
  
  * running file on flag.out: gzip compressed data

7. __mv flag.out flag.gz__

  * Have to rename the file or you will get a suffix error
  
  * this will allow you to decompress the file

8. __gunzip flag.gz__

  * File created: flag
  
  * run file flag:flag: lzip compressed data, version: 1

9. __lzip -d flag__

  * File created: flag.out
  
  * run file flag.out: flag.out: LZ4 compressed data (v1.4+)

10. __mv flag.out flag.lz4__
  
  * Have to rename the file or you will get a suffix error
  
  * this will allow you to decompress the file

11. __lz4 -d Flag.lz4__

  *Decoding file flag 
  *flag.lz4             : decoded 264 bytes  

  * File created: flag
  
  * running file flag: LZMA compressed data

12. __7z e flag__
  
  * File created: flag~
  
  * running file flag~:lzop compressed data


13. __mv flag flag.lzop__
  
  * Have to rename the file or you will get a suffix error
  
  * this will allow you to decompress the file

14. __rm flag__

  * if you remove the flag file then lzop can't create a new file since flag already exist

15. __lzop -d flag.lzop__
  
  * File created: flag
  
  * running file flag: lzip compressed data

16. __lzip -d flag__
  
  * File created: flag.out
  
  * running file flag.out:XZ compressed data

17. __mv flag.out flag.xz__

  * Have to rename the file or you will get a suffix error
  
  * this will allow you to decompress the file

18. __xz -d flag.out__

  * File created: flag
  
  * Running file flag: ASCII text

19. __cat flag__
  
  *7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
  *6630725f3062326375723137795f32373866316131387d0a

20.  __Went to [Cyber Chef](https://gchq.github.io/CyberChef/)__
  
  * Ran the ASCII text through Cyber Chef with the from HEX 
  
  * You will then get the Flag :picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_278f1a18}
