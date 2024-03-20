Welcome to the intro to i01 InMoov services in MRL. 
= 


audioPeak Jaw Movements
=

I'm eating lunch so a proper write up of this isn't done yet. Soon. lol. 

Controller > Mouth (LocalSpeech) > i01.Head > Calibrate Jaw settings > Python tab


============


From the ```python``` tab, create a ```new``` file and paste this script into it. 
```py
i01_head_jaw.subscribe('i01.mouth.audioFile', 'publishPeak', 'moveTo')
```

Now hit execute and that will have subscribed your jaw to ```i01.mouth.audioFile```.

Now click the ```Runtime``` tab and ```save config```.  This will create the needed data in your ```data/config``` folder. 

Now back to the ```python``` tab and enter in the following and ```execute```.

```py 
import org.myrobotlab.service.config.AudioFileConfig as AudioFileConfig

config = AudioFileConfig()
config.peakDelayMs = 300            #JAW SERVO DELAY ADJUSTMENT: If you need to delay the servo to line up with audio.
config.peakMultiplier = 250.0       #JAW SERVO OPEN/CLOSE RANGE: How much the mouth can open.
config.peakSampleInterval = 1.0     #JAW SERVO SENSITIVITY: How frequently the servo can respond to the audioPeak. 
i01_mouth.audioFile.apply(config)

i01_mouth.speak('hello, this is a test of the peak from mouth audio file')
```

Your jaw should be working much better at this point. 

Now you can adjust the figures until you are happy with the output your jaw is producing. 
- I suggest leaving ```peakSampleInterval = 1.0``` as is as that will give you the best results with a servo.
- It can also be helpful to reduce your jaw's speed a little bit. For example, I often have my jaw set to 170.
- Different speeds will require different ```peakDelayMs``` and ```peakMultiplier``` adjustments for ideal movement.

Once you are happy with your jaw's movements, return to the Runtime tab and save your config.

NOTE: Your results will also depend on the ```mouth``` AKA ```Text-to-speech``` you are currently using. 
- It is important to remember that Maryspeech is evil and will NOT work well for your jaw. 
- Use LocalSpeech / Polly (Requires API) / NovelAI (Requires API)

