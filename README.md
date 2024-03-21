Welcome to the intro to i01 InMoov services in MRL. 
= 

Intro
= 

I'm kind of working backwards here, so some of the how-to basics is worked into audioPeak Jaw movements for now. 

More updates will be added to this page eventually.

audioPeak Jaw Movements
=

Here is a video tutorial on audioPeak for those interested in having the visual examples. ```click image below```

<a href="https://youtu.be/Q55iQEN8Z1Y?si=eoSieSf14OGaoMij" />
<img src="https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/57f5ddc9-0ead-404e-909e-66d4a3c61134" />

Getting Started
= 

Click the ```thumb``` which will launch the ```i01``` InMoov UI.

![001-i01thumb](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/40d01e00-8c01-4508-beb3-15f7abaafdee)

Note: click ```i01``` anytime you want to return to the InMoov UI. 

Click on the highlighted circle to access ```controllers```

![002-i01UI](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/9459eeed-7e0d-402a-913f-308062e153e9)


- If you are using the V1 Head you will be using ```Controller Left``` by default.
- If you are using the V2 head or something different, you can use ```Controller 4``` as there is no default yet. 

![003-ControllerSelect](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/f80e752c-26ed-4f4a-a841-abf08c2d68c9)

Alternatively, you can start services such as ```Arduino``` from the ```runtime``` tab.

Enter a ```name``` (Anything you want to name a service) > ```Select Type``` of service > ```start service```. 

![004-RuntimeServiceStart](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/711eae60-90ca-479b-a2f2-bc7176b2ba34)

Now we will start the head. Click the head icon > click ```on```. 
- While here make sure that the ```Mouth Control``` is set to ```off```. We no longer need this if using audioPeak for our jaw.
  
![005-Headui](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/bab88ab9-6464-4959-9eb8-83e11a6b900a)


Now click on the ```i01.head.jaw``` and select your ```Controller``` and ```Pin```, then hit ```Basic```. 

![006-JawServo](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/b09e7451-3b36-47ae-9995-def7c0fd06f3)

Depending if this is your first time setting up a servo or not... click ```Limits``` to open the limits section you see in the image. 
- Adjust your output limits to whatever your jaw limits need to be.

- I will write a calibration section to this tutorial eventually, but for now......
     - Set a smaller/safe range of limits > ```Control``` > ```attach``` to power > widen limits slowly until a desired and safe range is achieved.

NOTE: Your jaw limits will NOT be the same as mine as my jaw mechanism is not standard InMoov.

- Set your ```Rest``` position with the orange slider. You can click the ```Rest``` button to bring it back to the rest position. 

![007-JawLimits](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/174ad7b1-ff08-412c-9880-8b3ea2e54dc4)

![008-JawEnable](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/addf26ec-6b6a-451b-aa0b-81e43efdebc8)

![009-ServoPowerRange](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/fd37df1c-8ed0-458b-8f43-ac06b9c4a47a)

Now click on the speech icon > select ```Speech Service Type``` > Scroll down to ```LocalSpeech``` and click ```Set Speech Type``` > click ```on```. 

![010-MouthSelect](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/4bc96135-177e-4488-974a-cf583909d47e)

Now ```i01.mouth``` will be working so click on that to see its UI. You try copy/pasting the text below into the text area and hit ```speak```.

```xml
Hello. I am the voice of David from Microsoft's local speech. This is an example of me speaking.
```

![011-MouthTest](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/4cc1d9d4-4dc3-4604-93e0-86c43aacdc09)

Click the ```python``` tab on the left. Open a ```new``` script. 

![012-Python](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/738eeac4-06e3-45ca-b6db-ccd947f55012)

Give it a name. 

![013-PyScriptName](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/74118779-36aa-4f92-a845-3dacd067a15b)

Copy/Paste this into the script you just created.

```py
i01_head_jaw.subscribe('i01.mouth.audioFile', 'publishPeak', 'moveTo')
```

Now hit ```execute``` and that will have subscribed your jaw to ```i01.mouth.audioFile```.

NOTE: Technically your jaw is working now with audioPeak, but... we haven't adjusted anything yet. 
   - It will barely move and won't look good. Don't worry about moving it yet. 

![014-SubscribetoJaw](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/f24dbc75-f9ca-482d-996b-b870cd7b1fbb)

Now click ```runtime``` > ```safe config``` > name your new config setup (Whatever you want) > click ```ok```. 
- Now your config will be saved to access anytime you want in the future. 
 - You will see it displayed in ```Configurations``` in this window > select your config from it > ```start```.

![015-SaveConfig](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/8ef1cb56-ac48-421f-b442-1e1c5be05635)

Now click back to the ```python``` tab and copy/paste the following in and hit ```execute```. 

```py 
import org.myrobotlab.service.config.AudioFileConfig as AudioFileConfig

config = AudioFileConfig()
config.peakDelayMs = 300            #JAW SERVO DELAY ADJUSTMENT: If you need to delay the servo to line up with audio.
config.peakMultiplier = 250.0       #JAW SERVO OPEN/CLOSE RANGE: How much the mouth can open.
config.peakSampleInterval = 1.0     #JAW SERVO SENSITIVITY: How frequently the servo can respond to the audioPeak. 
i01_mouth.audioFile.apply(config)

i01_mouth.speak('hello, this is a test of the peak from mouth audio file')
```

![016-TestingJaw](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/de9904ca-39a0-45dd-8286-b12fc2d15b06)

Your jaw should be working much better at this point. 

Now you can adjust the figures until you are happy with the output your jaw is producing. 
- I suggest leaving ```peakSampleInterval = 1.0``` as is as that will give you the best results with a servo.
- It can also be helpful to reduce your jaw's speed a little bit. For example, I often have my jaw set to 170.
- Different speeds will require different ```peakDelayMs``` and ```peakMultiplier``` adjustments for ideal movement.

Once you are happy with your jaw's movements, return to the ```runtime``` tab and ```save config```. 

NOTE: Your results will also depend on the ```mouth``` AKA ```Text-to-speech``` you are currently using. 
- I suggest using ```LocalSpeech``` because it works without anything else needed.
- You can use Amazon Polly or NovelAI if you have an account and enter in your API in the ```i01.mouth.yml``` beside ```API:``` or ```Token:```.  
- Avoid MarySpeech with audioPeak. (More details below)

Anytime you ```save config``` a new folder with whatever you named your config will be saved in ```MRL1.1.****\data\config```

![017-DataConfig](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/6421d2c7-ce8e-4991-8deb-6c7a4ed177ad)

You can see here in the ```i01.mouth.audioFile.yml``` that the settings we saved from ```python``` successfully saved to our config. 
  - You can also change them from ```i01.mouth.audioFile.yml``` while MRL is shutdown if wanting. 
  - All your services will be like this and listed in your config folder. 

![018-SettingsSaved](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/a6673c9a-61ab-463f-bded-963d49282ebd)

audioPeak: Side note
= 

Anytime audio is being played, you can click ```i01.mouth.audioFile``` and be able to see the bar at the bottom sample the audioPeak. 
- Our servo will follow this pattern as well!

![019-AudioPeak](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/2e2bc6ad-fe53-404f-a45e-7da8ab4a1338)

MARY IS EVIL!!!
=

It is important to remember that ```Maryspeech is evil``` and will NOT work well for your jaw. 

![EvilIsMary](https://github.com/CyberSyntek/i01InMoovIntro/assets/81597534/9e5063cb-b536-4d82-8030-b929c26a200b)

You can test out Mary's evil if you would like by clicking back to ```i01.mouth.audioFile``` and watch a CONSTANT FULL BLUE BAR whenever audio is played. 
- Or take my word for it and just avoid the evils of Mary. :)

終り
