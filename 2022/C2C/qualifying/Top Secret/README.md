# Top Secret

**Ttile**
> Top Secret

**Category**
> CRYPTOGRAPHY

**Difficulty**
> Easy

**Points**
> 50

**Description**
> The internet post man gave me this but I don't get it.\
> He said it was top secret so the sender encrypted it with some RAW encryption and asked to not share it with anyone.\
> I really trust you so can you decrypt this for me?

**Attachments**
> TopSecret.zip

## Solution
```shell
$ openssl rsautl -decrypt -inkey key.private -in TopSecret.txt -out out.txt -raw
$ cat out.txt 
flag{N0M0R3AS3CR3T}
```

The contents of out.txt:
```
<bytes bla bla bla...>flag{N0M0R3AS3CR3T}
```

## Flag
flag{N0M0R3AS3CR3T}
