# Bravo Six, Going Dark

**Title**
> Bravo Six, Going Dark

**Category**
> OSINT

**Difficulty**
> Medium

**Points**
> 250

**Description**
> We just received a notification from a Facebook content reviewer. Apparently a livestream involved a drone scoping out what appears to be a location for potential robbery. They shut down the stream but were only able to save the Thumbnail snippet. The GPS metadata was stripped so we have no idea which country let alone state it may have occurred in. Can you please review the footage and determine the exact street number and name where the drone was flying over? Flag Format is FLAG{## streetname}

**Attachments**
> DJI_0030.MP4.zip

## Solution
Need to pay very close attention to the footage and watch it slowly, frame by frame, searching for possible clues.

```shell
$ ffmpeg -ss 00:00 -i ./DJI_0030.MP4.mp4 -t 05:00 ./frames/filename%05d.png # Split video to frames
```

Noticed Selvatica on the left of the building, and a phone number on the right: 9354 1700.\
Searched for Selvatica on Google Maps but there were too many results, so probably missed the right one.

Then searched for the phone number and finally, found https://www.ausibiz.com/matrix-fitness-03-9354-1700.\
http://www.matrixfitnesstraining.com.au/, (03) 9354 1700\
So matrixfitnesstraining is the store on the right on of the building.

https://www.google.com/maps/@-37.7335508,144.9608784,3a,50.4y,15.46h,101.4t/data=!3m6!1e1!3m4!1s4GkJCYX8wv_EEKnIcznoJA!2e0!7i16384!8i8192?hl=en

## Flag
FLAG{52 gaffney}
