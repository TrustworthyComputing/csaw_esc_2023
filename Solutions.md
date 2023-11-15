# Solutions 

### All White Party

**Solve Rate: 15%**

This challenge had two parts. The first one was to utilize the side channel on the vibration sensor to get the username "Barry". The code checks the string sequentially, and breaks upon an incorrect character. For example, "Abby" would have no delay since the first character is incorrect, but Brian would have a small delay as the loop only breaks after the second letter "r" (indicating that the letter "B is correct).

The second part of the challenge asked to find a SHA hash collision. Here, SHA1
was used, and the system only compared the first five bytes. (Note this
truncation is similar to other truncated versions of SHA224, SHA384). However,
finding a collision with "Barry" will take hours to run, and teams who attempted
this method reported there was no solution. 

Thus, to solve this challenge, teams had to realize that only the first five
bytes of the username were checked, so "Barry", "BarryAllen", "BarryWhite",
"BarryManilow" and "Barryalkjdljajoiw" are all valid usernames. This allows us
to find a collision of any username that begins with Barry with any 10-digit
password. This is similar to a modified birthday attack problem for hash
functions. The most efficient way to do this is to create two sorted
dictionaries of usernames and passwords to find a collision. Compared to tens of
hours for a first order collision, this program takes a few seconds to run
locally.

Fun Facts:
Some COM ports added a newline over serial, so the SHA1 value would be Barry\n. 
We intended the name of the challenge to follow Barry White, but one team also mentioned singer Barry Manilow would also frequently wear white tuxedos. 

### Bluebox

**Solve Rate: 85%**

For this challenge, teams were required to playback the tone. Unlike the original bluebox hack where tones were replayed directly on a speaker, Most teams used a free mobile application or software to analyze the frequencies of the different notes. 

Fun Facts:
Four years before founding Apple, Steve Jobs and Steve Wozniak invented the bluebox hacking tool in 1972. This device allowed users to manipulate the telephone system by replaying tones, making free international calls and engaging in other illegal activities. The only complete bluebox device remaining sold at auction for $125,000 in 2017.


### SPItFire

**Solve Rate: 75%**

This challenge asked teams to reverse engineer a SPI protocol. For SPI transmissions, 1 is high and 0 is low, synchronized with a clock.
Teams could first use the error codes to figure out the following packet format:

HDR LEN MSG0 MSG1 ... MSGN CRC

The HDR is always 0xA5, the LEN is for the MSG bytes, and the CRC is the standard CRC8 algorithm. Using this, teams can send FLAG in ascii

A5 04 46 4C 41 47 DA.

Next, teams can listen to the clicks of the relay to distinguish the rising and
falling edge of the signals. Since HDR is always 0xA5 (0b10100101), teams can
utilize the sample HELLO message to get the clock frequency. Synchronizing this
with the clock frequency, teams can reverse engineer the flag message. 

Fun Facts:
SpitFire was a spy plane in World World II. We also wanted to have a name that began with SPI. 
The flag "Spy Burned" was a nod to a spy being caught, which is referred to as
being "burned". This also goes along with the "fire" theme in SPItFire. 
Additionally, Spitfire is a My Little Pony character, which we found out by chance. There is also a Spitfire Spy Football Club in England, named after the spy plane. 

### czNxdTNuYzM

**Solve Rate: 50%**

A number sequence was flashed on the seven segment display at a rate derived
from frequencies detected by the microphone. Low frequencies resulted in very
fast SSD updates while high frequencies (in the range of 3-4kHz) resulted in
slow updates. As the custom shield only contains one SSD, teams had to infer
that '.' indicated the end of a number and '_' were used to separate digits.
Thus, the set of numbers [1234, 5678] would display as "1 _ 2 _ 3 _ 4 . 5 _ 6 _
7 _ 8". The goal of the challenge was to identify the next number in the
sequence. Many teams were able to visually record the SSD and manually slow down
the video
to detect the number sequence.

Fun Facts:
The utilized sequence was a variant of Recamán’s sequence, which many teams
identified as [OEIS Entry A008336](https://oeis.org/A008336). The name of the
challenge is base64 encoded and translates to "s3qu3nc3".

### Sock and RollS

**Solve Rate: 20%**

This challenge incorporated Morse Code transmitted over the speaker, where an ON tone indicated a dot and an OFF tone indicated a dash. The speaker transmitted the message SOCKS to the microphone, which recorded the message (similar to bluebox). 

For this challenge, teams needed to reverse engineer the mSorse code. To distinguish between letters in Morse Code, the "." were printed at the start of three consecutive letter transmissions. Once teams were able to recover "SOCKS", they needed to unplug the speaker or microphone during the "CK" to correctly transmit "SOS".

Fun Facts:S
We left a hint in our GitHub commit history, directly stating "SOS" instead of distress signal.
The iteration message comes from the TV show LOST.

### Vender Bender

**Solve Rate: 90%**

This challenge was a call and repeat challenge. Teams needed to find a way to measure the relay click (indicating a motor start) and send ERR within 200ms of the click. This can be done via a laptop microphone, probing the pin, or syncing with the serial outputs. Upon doing this 5 times in a row, the flag is revealed.

Fun Facts:
Who writes these challenge descriptions anyway?
