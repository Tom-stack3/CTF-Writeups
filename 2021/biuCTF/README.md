# biuCTF
## Pwn

### Math Isn't That Hard
By reading in the internet, I understood that by entering regular numbers and without encountering any problems, the end result will always be 9 and not an number between 1-8.
So I tried searching for a way to trick the program. First I searched for vulnerabilities in the `scanf()` method, I thought maybe there is some way using `scanf()` to change the value of m to be 9, that way the FLAG will be printed. But failed to find anything.

Afterwards, I looked at the calculation and searched for possible holes and places where problems might occuer.
Finally I understood that a problem might occuer in line 17:
```c
n *= 9;
```
If I enter as `n` a big number, like the max integer (2147483647) it will mess up the multiplication and give other result.
So I chose m randomly and chose `n` to be 2147483647, and so the following output:
```Sum of digits of 2147483639 = 2 and...```

Yay! I run the program again, chose `m` to be 2 and `n` to be the max integer (2147483647) and the FLAG was printed 🙂

### My Favorite Word Is:
I understood that in order to get the FLAG printed, we needed to somehow stop the loop that replaces the FLAG with A's earlier, so it won't "cover" the FLAG.
We couldn't just make the string empty or very short, because the code had the check for the "BIU" in 25,26,27 indexes.\
Then I remembered from good old Noa Agmon days, that the way strlen works, is by searching for a `\0` in the string, and then it stops.\
So, for the following string (`char[]` in c):
`['\0', 'h', 'e', 'l', 'l', 'o']`, `strlen()` counts it as having a length of 0.

That way we could make a string that `strlen()` will count its length as 0, but the string will stil have "BIU" in the 25,26,27 indexes.

A string like this can look like the following:
`['\0', '\0', ... , '\0', '\0', 'B', 'I', 'U']`

(with `\0` 24 times)

So I just used this simple Python code and got the FLAG printed :)

```python
from pwn import remote

s = remote('challenges.ctf.cs.biu.ac.il', 3001)

s.sendline('\u0000' * 24 + 'BIU')
s.interactive()

```

## Misc

### Tic Tac Toe X_O
Played the game a little while and understood that it cannot be bitten by just playing it :)
So I tried to find some edge cases where it could change the program's behaviour, like entering not an int char, trying to override the program's choices, or entering a out of bounds int - without much success.\
I also tried putting negetive numbers and saw that `-1` was treated like the last row - like it does in python.\
So with that I tried to override the program's choices and saw that it passed the check!
So I just played the game, overriding the program's `X`'s and choosing my turns however I want.\
If the bot chose the first row and the first column and I wanted to put a `O` there instead, I could do that by entering `-3` for the row and `0` for the column, and that's how I won the bot :)


## Web
### Session master
At first I saw that if `secretPass` is not set, then the code sets it to something I have no control of: `secrets.token_hex(16)`.\
So I thought there must be some way to set it by myself, through the url or the Headers of the get request - without success.\
but then I decided to look in the cookies of the page (using CookieManager chrome extension) and saw a cookie named `session`. Voilà!
I copied the Cookie and tried to decode it, until I tried base64 and got this:
`{"secretPass":"476230a6342f06f3eca83d8e0f663f3f"}`
This is the right secretPass! typed it in and that's it.

### Collision
Read the PHP code and understood that the url gets 2 parameters, `secret1` and `secret2`. In order to get the flag, they had to meet the following conditions:
1. `secret1` had to be numeric
2. `secret1` length != `secret2` length
3. `$secret1 !== $secret2` which means that either their types are not the same, or they do not have equal values.
4. their MD5 hash had to be equal (**after type juggling!**).

I read a-bit about the md5 collisions, and found a way to exploit the type-juggling in PHP when comparing the MD5's. 
The following values begin with 0E after md5 encryption, which makes them equal to 0 when compared with `==` (and not `===`):
- QNKCDZO
- 240610708
- s878926199a
- s155964671a
- s214587387a
- s214587387a

Chose 240610708 to be `secret1` because it had to be numeric and for `secret2` QNKCDZO, and that's it.

## Programming
### Square root is easy
I saw that using the regular `math.sqrt()` in Python doesn't help because it gives the scientific notation and not the full number and when trying to format it back to the full number it rounds it loses it's accuracy. So the following code didn't work:
```python
print("{:f}".format(math.sqrt(HUGE_NUM)))
```
Instead, I searched for a function that calculates the square roots for large numbers such as the one given and found the following:
```python
def do_sqrt(x):
    if x < 0:
        raise ValueError('Not defined for negative numbers')
    n = int(x)
    if n == 0:
        return 0
    a, b = divmod(n.bit_length(), 2)
    x = 2 ** (a + b)
    while True:
        y = (x + n // x) // 2
        if y >= x:
            return x
        x = y
```
So I used it to calculate the square root of the number given and that's it :)

### Make The Ascii Fly
I understood of course that I wouldn't be able to type them all, especialy on time. At first I made a simple python that gets such list, generates a string with the Ascii char represantation like wanted and copies it to the clipboard.\
I tried to solve it quicly with it, the problem was that I wasn't quick enough to copy the list from the terminal into the python program, and paste the string generated back in the terminal.
So I made the following python to do it automatically and got the FLAG:
```python
from pwn import remote

s = remote('challenges.ctf.cs.biu.ac.il', 5001)
s.recv(2048)
s.sendline('')
list_got = s.recvuntil(']').decode().split(', ')

list_got[0] = list_got[0].replace('[', '')
list_got[len(list_got) - 1] = list_got[len(list_got) - 1].replace(']', '')

print(list_got)

st = ""
for i in list_got:
    st += chr(int(i))
s.sendline(st)
s.interactive()
```
