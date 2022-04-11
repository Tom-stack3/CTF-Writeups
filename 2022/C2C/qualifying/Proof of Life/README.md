# Proof of Life

**Title**
> Proof of Life

**Category**
> OSINT

**Difficulty**
> Easy

**Points**
> 150

**Description**
> A child has run away from home and sent this image to his family via Dropbox to show that he is OK! They can't seem to see anything in the photo though. Can you use your detective skills to find the street this photo was taken on? Flag Format (all lowercase) - flag{streetname_st}

**Attachments**
> proof_of_life.jpeg.zip

## Solution
Uploaded the image to https://jimpl.com/ to inspect the metadata, and indeed got the lat/long of the image:\
Latitude	33 deg 54' 50.55" S\
Longitude	151 deg 11' 55.95" E

https://www.google.com/maps/place/33%C2%B054'50.6%22S+151%C2%B011'56.0%22E/@-33.9138618,151.1988415,19.08z/

Beaconsfield St, Alexandria NSW 2015, Australia

## Flag
flag{beaconsfield_st}
