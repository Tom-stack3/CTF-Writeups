# Riddle Me This

**Title**
> Riddle Me This

**Category**
> CRYPTOGRAPHY

**Difficulty**
> Medium

**Points**
> 160

**Description**
> We've been tracking a network of operators for months. They're distributed throughout Europe but their exact location is unknown. We're aware they are using this website to coordinate activities: https://dev-talk.space/breaking-a-cipher/ We need you to go to the site, crack the code, get to the next screen, and find out who their next target is.

**Attachments**
> None

## Solution
```
What Happens When a Liar Dies?
Hg ihgu uohii
```
I saw this riddle on Batman :)

So I knew the answer is: He lies still.

So He lies still --> Hg ihgu uohii
Meaning:
h -> h
e -> g
l -> i
i -> h
s -> u
t -> o

Ok, so now what?

After the riddle, there is a table:
```
a f j t k w k d t f d r e x l l k p p k
s a k l f s f f h d e p f k p n x j d s
f f k p y d o y r s s q s n j b v a v j
n q m t j a l e h d q s d x z s d f k j
d d y r f d f p r p l k e r t u s b f l
k n f f d s s s g l n p s a q z r t e s
d k e d f d q q y f o j d f k s f q k d
j j a w j f b e a q t y b b j x c l p t
k k s k d e r i t n b n n v m v a p p q
d l p f p b y t y v g f f n n j f t d t
y r e j d v v b b j k d j v d k d v f b
t s s f j e f d a l j l b v l t y j s l
e y q k r r t c e d h k s t r k s q s y
f r d l v f s c u r e y y b t p e d f e
e t s p t e p l n q v f x q s n l r t q
r r a a e l c a d m j g q k p p f y v r
a e a r j k q b k l q s t d a j k c v f
x z v c n b e s x p e r t v z e z b n j
```

So I tried replacing the letters from the first riddle:
```
a f j o k w k d o f d r g x h h k p p k
u a k h f u f f h d g p f k p n x j d u
f f k p y d o y r u u q u n j b v a v j
n q m o j a h g h d q u d x z u d f k j
d d y r f d f p r p h k g r o u u b f h
k n f f d u u u g h n p u a q z r o g u
d k g d f d q q y f o j d f k u f q k d
j j a w j f b g a q o y b b j x c h p o
k k u k d g r h o n b n n v m v a p p q
d h p f p b y o y v g f f n n j f o d o
y r g j d v v b b j k d j v d k d v f b
o u u f j g f d a h j h b v h o y j u h
g y q k r r o c g d h k u o r k u q u y
f r d h v f u c u r g y y b o p g d f g
g o u p o g p h n q v f x q u n h r o q
r r a a g h c a d m j g q k p p f y v r
a g a r j k q b k h q u o d a j k c v f
x z v c n b g u x p g r o v z g z b n j
```

But I couldn't get it to work.

I knew that the answer was in the following format:
```
https://thewarrior.space/enter string here
```

So I went to the site and wandered around for a bit, searching for possible clues.
I read a couple of posts there until I saw a post named "Jim Carrey": https://thewarrior.space/whohugowighug/ \
I clicked on the link and there was the flag.

Jim Carrey played the Riddler in "Batman Forever", therefore the connection to the first riddle.

So I guess this is an unintended solution, but I still got the flag :)

## Flag
FLAG{Jim_Carrey}
