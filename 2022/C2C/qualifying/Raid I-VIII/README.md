# Raid I - They said dat it couldn’t be done

**Title**
> Raid I - They said dat it couldn’t be done

**Category**
> FORENSICS

**Difficulty**
> Medium

**Points**
> 200

**Description**
> A ping came through on slack - one of our sock puppet accounts monitoring Raidforums has discovered a unique dataset being shared. It appears to be the removable SD card of a drone. Our drone expert in Helsinki is tied up with other work but said it’s important to note it does not appear to be the on-board storage SD. Investigators believe this may be tied to a counter-terrorism case, but need to confirm the details, can you help them fill in the gaps? First off, what is the serial number of the drone (not the Machine ID)? Flag format is FLAG{serial}

**Attachments**
> seized drone contents.zip

## Solution
At first I didn't know how to read the data of the SD card.
After some research I found the following thread: https://mavicpilots.com/threads/logs-inside-the-sd-card-i-want-to-know.91756/,
So I downloaded DatCon and CsvView on an old windows machine and changed the log files extension to `.DAT`.

By opening the camera_log file in the CsvView program, we get the mcId of the drone, which is: 1SDCH87016BMZQ.
But we need the serial number and not the machine ID.
We also get the machine version, which is v3.4.6.43.

After some digging, I decided to export the camera_log.DAT which I opened with CsvView to a csv file.
I looked through the csv file, searching for words like "sn" and "serial", and found a very strange cell, which contained lots of text.
I copied it to a text file and opened it with.
Used the regex expression "[A-Z0-9]{14}" to highlight serial numbers, and voilà!
Found the following row:
```
 2721 [L-FMU/VERSION]Ac  SN  :1SZCH8F4T2DNPK|   2721 [L-FMU/VERSION]Mc  ID  :1SDCH87016BMZQ|   2721 [L-FMU/VERSION]Bat SN  :1U5X07WEXP000R|   2721 [L-FMU/VERSION]Mc  Ver :v3.4.6.43|   2721 [L-FMU/VERSION]Bat Ver :v5.0.10.18| 
```

Here we can clearly see three numbers.\
After checking in http://tools.retroroms.info/, `1SZCH8F4T2DNPK` is indeed the serial number of the drone.\
`1SDCH87016BMZQ` is the machine ID of the drone that we already encountered, and `1U5X07WEXP000R` was apparently the battery serial number.\
I guess that we solved two challenges, at the same time.

Oopsie 🙃

## Flag
FLAG{1SZCH8F4T2DNPK}

# Raid II - Moar Powah

**Title**
> Raid II - Moar Powah

**Category**
> FORENSICS

**Difficulty**
> Medium

**Points**
> 200

**Description**
> Smart batteries aren't 'dumb' like traditional LiPo's - there is a lot of data involved. It can also be used to track down criminals who've purchased batteries with the package - or seperately. Can you please help us find the serial number of the battery? Flag format is FLAG{serial}

**Attachments**
> seized drone contents.zip

## Solution
Mentioned in the previous challenge, we can see that the serial number of the battery is `1U5X07WEXP000R`.

## Flag
FLAG{1U5X07WEXP000R}

# Raid III - Groundhog day

**Title**
> Raid III - Groundhog day

**Category**
> FORENSICS

**Difficulty**
> Easy

**Points**
> 75

**Description**
> "This is like the fourth time we've done this today..." "Yeahp, that's forensics for you. Lock in those numbers, the whole court case depends on it." Can you you provide the make, model and manufacture date of the drone? Flag format is FLAG{make-model-submodel-DD-MM-YYYY}

**Attachments**
> seized drone contents.zip

## Solution
We already have the serial number of the drone, which is `1SZCH8F4T2DNPK`.
Using http://tools.retroroms.info/ we can find the details we need:

```
DJI Serial Decoder
Model   Manufacture Date
Mavic Mini (wm160)	15-Aug-2020
```

## Flag
FLAG{dji-mavic-mini-15-08-2020}

# Raid IV - Geoguesser

**Title**
> Raid IV - Geoguesser

**Category**
> FORENSICS

**Difficulty**
> Medium

**Points**
> 175

**Description**
> Okay great, got the details of the drone, now we need to know where these multiple flights occurred. There's a number of ways of doing this - but whatever works for you. What city and country was the drone flown in? Flag format is FLAG{city, country}

**Attachments**
> seized drone contents.zip

## Solution
Obviously, looked at the `GPS:Lat` and `GPS:Long` columns, and found the coordinates of the drone's flight.

First row coordinates:
`Lat: -37.8165806, Long: 144.9344869`

Therefore, Melbourne, Australia.

## FLAG
FLAG{melbourne, australia}

# Raid V - Snap n Send it

**Title**
> Raid V - Snap n Send it

**Category**
> FORENSICS

**Difficulty**
> Medium

**Points**
> 250

**Description**
> What is the date of the oldest recorded flight log? This can be useful to cross-reference with our drone detection systems, see if anything was registered in the air at that time. Flag format is FLAG{DD/MM/YYYY}

**Attachments**
> seized drone contents.zip

## Solution
I actually solved this challence first, and I didn't tried CsvView yet, but DatCon was fine for this one.

So I downloaded DatCon, changed the log files extension to .DAT and ran DatCon on the files.
The fc_log file showed some errors while being parsed, but still a fc_log.csv file was created.
The camera_log file was also successfully parsed and a camera_log.csv file was generated.
After inspecting both csv files, the date of the oldest flight log (in the `GPS:Date` column) from both files is: `2020-10-30`.

## Flag
FLAG{30/10/2020}

# Raid VI - Send n Snap it

**Title**
> Raid VI - Send n Snap it

**Category**
> FORENSICS

**Difficulty**
> Medium

**Points**
> 250

**Description**
> What is the date of the most recent recorded flight log? This can be useful to cross-reference with recent CCTV, or even social media posts that may have caught them in the pic - or even released photos of the drone! Flag format is FLAG{DD/MM/YYYY}

**Attachments**
> seized drone contents.zip

## Solution
Again, looked at both csv files, and found the date of the most recent flight log (in the `GPS:Date` column) which is: `2021-05-15`.

## Flag
FLAG{15/05/2021}

# Raid VII - Ruffle My Rotors

**Title**
> Raid VII - Ruffle My Rotors

**Category**
> FORENSICS

**Difficulty**
> Medium

**Points**
> 300

**Description**
> Got it - so we have the list of days the flights were involved. To check what the weather was that day, we tried pulling the data from the meteorologists...unfortunately, their expert told us "wind can travel in any direction depending on environmental objects". Damn it. Can you please read the data recorded to the drone about the wind direction of the most recent flight, and what the average direction was? Flag format is FLAG{direction}

**Attachments**
> seized drone contents.zip

## Solution
At first I thought the direction should be a number (degree), because it was in this format in the CSV log file.\
So I used Excel to calculate the average direction of the wind direction column, (at first I assumed it was `AirSpeed:windDirection`, so avg is 0).\
After that didn't work, I tried another column (`IMU_ATTI(0):directionOfTravel[mag]:C`) but that didn't work either.\

After some more tries, I loaded up the csv file into CsvView and saw that the wind is to the north (`AirSpeed:windDirection` 0).\
And I understood that maybe the direction is supposed to be a literal direction (north, south, east, west) and not a number.\
So I tried FLAG{north} and it worked! 🥳

## Flag
FLAG{north}

# Raid VIII - Mayday

**Title**
> Raid VIII - Mayday

**Category**
> FORENSICS

**Difficulty**
> Medium

**Points**
> 500

**Description**
> Thanks for all the information so far - however, we still need to know what happened in that final flight. Keep in mind, this might pop up in court, we need to be completely right here. We've come up with a few options, but obviously the only real way to know is from the data. A little OSINT wouldn't hurt either! Options: ran out of battery, entered no-fly-zone, caught in a tree, caught in powerlines, landed with no issue, crashed into the ground, downed with jammer, downed by hacking, drifted away by wind, critical system failure. Flag format is FLAG{the full text answer}

**Attachments**
> seized drone contents.zip

## Solution
- Ran out of battery: no. checked the "BatteryInfo:CapPercentage:D" column in the drone's flight log.
- Entered no-fly-zone: probably not, after looking in the map, the drone basically flew over the same area for the whole flight.
- Drifted away by wind: no. the wind speed was very low, so it was not a drift away.

I used the CsvView tool to look at the drone's path.

I didn't see any powerlines in the area, so I assumed the drone didn't crash into one.\
I also saw that the drown's altitude was too high in the end of the flight for the drone to land, so I assumed it didn't crash into the ground nor landed with no issues.\
I also didn't see any system failures indicators in the csv.\
Also, by looking at the area of the drone's flight, I saw that it was flying between lots of trees, and in the end it kinda looked like he crashed into one.
Therefore I assumed that the drone crashed into a tree, and I was right. :)

## Flag
FLAG{caught in a tree}
