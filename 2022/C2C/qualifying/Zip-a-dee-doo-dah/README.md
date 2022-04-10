# Zip-a-dee-doo-dah

**Title**
> Zip-a-dee-doo-dah, zip-a-dee-ay, You-wont-be-getting-my-flag-today

**Category**
> CRYPTOGRAPHY

**Difficulty**
> Easy

**Points**
> 150

**Description**
> Look here punk! I am sick of you pentesters stealing all of my flags. This time it won't be so easy. Can't wait to see you spend an entirety getting this one!

**Attachments**
> openmeifyoucan.zip

## Solution
Used zip2john to convert the zip file to a format suitable for use with JtR, then used john to crack the password.\
Easy peasy lemon squeezy.
```shell
$ john-the-ripper.zip2john openmeifyoucan.zip > hash.txt
$ john hash.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 2 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 2 candidates buffered for the current salt, minimum 8 needed for performance.
Warning: Only 3 candidates buffered for the current salt, minimum 8 needed for performance.
Almost done: Processing the remaining buffered candidate passwords, if any.
Warning: Only 7 candidates buffered for the current salt, minimum 8 needed for performance.
Proceeding with wordlist:/snap/john-the-ripper/current/run/password.lst, rules:Wordlist
gangsta1         (openmeifyoucan.zip/flag.txt)
1g 0:00:00:00 DONE 2/3 (1969-04-03 22:42) 1.098g/s 47053p/s 47053c/s 47053C/s fireballs..pepper1
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

So john cracked the password: `gangsta1`

Now we can extract the flag.txt file from the zip file, and read the flag.
```shell
$ unzip openmeifyoucan.zip 
Archive:  openmeifyoucan.zip
[openmeifyoucan.zip] flag.txt password: 
 extracting: flag.txt                
$ cat flag.txt 
flag{92237299571325770045}
```

## Flag
flag{92237299571325770045}
