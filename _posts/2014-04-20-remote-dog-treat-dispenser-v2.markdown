---
layout: post
title: Internet Dog Treat Dispenser (v2)
date: '2014-04-20 15:43:00'
---

A few weeks ago, Ajax our dog started having separation anxiety issues—-he would cry bloody murder when we left him alone in the apartment. We crate trained him when he was 6 months old with our remote dog treat dispenser. Since then, when we leave him alone, he’s been quiet and usually just fall asleep. That is, until a few weeks ago.

Separation anxiety is a tricky thing to train, because you can’t there in person to correct the dog’s behavior. The bad behavior starts precisely because you are *not* there. It’s one of the top complaints among dog owners, and is the second most common reason for owners giving up or euthanizing their dogs[^1].

We looked at bringing back out our old treat dispenser, but it was clunky. The old version had to connect to a laptop, and the treat container was a plastic cup held together by scotch tape and paperclips. It also didn’t come with a nanny cam so we had to use Ustream, which while free, had ads and a 30 sec delay. And thus Treaty v2 was born.

I cobbled together this device, which streams video and audio in almost-real time (the audio has a 10 sec delay). I can use this to monitor the dog and dispense treat when he’s shows good behavior.

## Dog Treaty Demo Video

<iframe width="640" height="480" src="https://www.youtube.com/embed/mhdJi2rF1xA" frameborder="0" allowfullscreen></iframe>

This connects to a web interface I use to monitor and treat the dog. Well technically, the Raspberry Pi serves a page with a button that controls the dispenser’s motor. I can watch/listen to what’s happen and dispense a treat by clicking a button. This is helpful when I’m out and about, want to check on Ajax and more importantly reward him when he’s being calm and quiet.

![](/content/images/2015/06/1-nSa44VhzPnyBbGhgC8S1JQ.jpeg)

## The Modeling
The upper compartment contains the treats. You put treats between the fans, and the fan-like arm twists and scoots the treats along until it drops into the crate. The bottom compartment contains the stepper motor, which turns the fan when I click the “Give Treat” button.

![](/content/images/2015/06/1-U1Z70vS2J9La8VW9wsdp0w.jpeg)

Who says you can’t use [Blender](http://www.blender.org) to design mechanical parts?

This mechanism works well because you can use it with a variety of different types of treats. Many dispensers (e.g. gumball machines) one works with certain geometries. We tested it with biscuits, dried fish flakes, and even leftover steak. Kudos to Aaron for thinking of this idea.

## The hardware & webpage setup

For controlling the dispenser, I used a Raspberry Pi and followed [Adafruit’s Stepper Motor Tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-10-stepper-motors?view=all). For streaming video and audio, I also used the [RaspBaby](https://github.com/moustaki/raspbaby) setup, which installs mjpg-streamer for video and darkice running on icecast for audio. For the camera and mic, I just used an old Logitech webcam I had lying around. To serve the webpage, I set up nginx on the Raspberry Pi.

![](/content/images/2015/06/1-ClASvTZusbsTV_UQrQWsdA.jpeg)

![](/content/images/2015/06/1-8JyZgw9r-KV3aEIEmRN0ig.jpeg)

## What’s next

We’ve used this for a few times and it looks like Ajax is starting to show some improvements. Besides doggy improvements, there are also a few device improvements I’d like to work on for v3.

1. I want to get more real time audio stream. It’s very important to treat the dog right after his good behavior, so it’s important the audio is as realtime as possible. Right now it has about a 10 sec delay.

2. I want to put everything in one (small) box. As you can see the breadboard is quite bulky and there are a lot of wires swooping this way and that. Maybe I’ll try to design a PCB, or maybe I’ll use Adafruit’s solderable breadboard with [Pi Cobbler](https://www.adafruit.com/products/1148). In any case, the Raspberry Pi, wires, and treat dispenser (the cylindrical thin) should all be contained in one (probably 3d printed) case.

3. Right now the treats *sometimes* hits Ajax on the head when it drops from the container. Eek! Maybe I’ll make an attachable bowl or something that catches the treats. He can eat from the bowl instead of getting whacked by bits of steak.

In the meanwhile, Ajax can just stand back a little and look forward to some tasty treats!

![](/content/images/2015/06/1-inhcnpHmfX2DWqk_iXzUng.jpeg)

---

[^1]: http://www.dogbreedinfo.com/separationanxiety.htm