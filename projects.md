---
layout: page
title: Projects
permalink: /projects/
---

# The Brewhob

*This project was completed during a semester-long senior design course (advanced embedded systems). Our 5 person multi-disciplinary team worked hard to bring this idea to market in 4 short months. This was the most enjoyable, most unexpected, and most rewarding project I worked on during college.*

The Brewhob is an espresso machine control board designed to bring old espresso machines into the age of IoT and data analytics. It features plug-and-play installation with any espresso machine that currently uses a Gicar 3d5, an outdated and overpriced control board.

Espresso machines can be challenging to troubleshoot when they stop operating properly. Sometimes it may not be easily noticed that the flow rate has slightly dropped or that the machine is struggling to regulate the temperature. With machines that rely on boards like the Gicar, these issues can be time-consuming to troubleshoot, and the user may not even realize there is a problem until significant damage is caused to the machine.

The Brewhob board records sensor data in real time and uploads the data to the user's dashboard. This information can be used to monitor the system and detect issues with the machine before it becomes a serious problem. If something does go wrong, historical graphs for temperature, flow rate, and other parameters can be reviewed to further aid the repair process.

More information can be found on our (not so serious) website, [brewhob.com](https://brewhob.com).

![Brewhob poster](/assets/img/brewhob_poster.PNG)

# The Auto-Otamatone

This monstrosity was created in an introductory embedded systems course. The [Otamatone](https://en.wikipedia.org/wiki/Otamatone) is a fretless toy instrument that is incredibly hard to play in tune. Due to the fretless neck, there is no good way to tell where any real notes are located.

We decided to take all our knowledge of FPGAs, MMIO, serial communication, verilog, and low-level C programming and make a self-tuning otamatone that can be controlled with a MIDI keyboard. Unnecessary? Yes. Hilarious? Yes. 

![Otamatone poster](/assets/img/otamatone_poster.PNG)

# Solar System Shadowbox

I wanted to combine woodworking and electronics, something that I hadn't done before. A routing table purchase and a few dozen LEDs later, the solar system shadowbox was finished.

The LEDs are connected to an Arduino which receives IR signals to control the lights. There are various flashing and blinking patterns available, including obnoxious strobes and much calmer fading patterns using PWM.

The planets were made by drilling circular depressions in the wood, drilling a hole in the middle for the LED, and filling the depression with hot glue.

The stars are made from thin optic fiber strands taken from a lamp. About 5 fibers are connected to a single LED in order to minimize the amount of pins required on the Arduino. I carefully drilled into the top of the LEDs, set the strands inside the hole, and glued them in place. This was as maddening as it sounds.

# Raspberry Pi Gameboy

When the Raspberry Pi Zero came out, I thought it would be really cool to make some sort of handheld device with it. Since it has fairly limited computing power, I knew it wouldn't be an extremely capable device in terms of performance.

Retro game emulation is a common use-case for Raspberry Pis, so why would the Zero be any different? I decided I would make a retro game emulator that fits inside one of my favorite childhood video game system, an atomic purple Gameboy Color.

At the moment, emulation and controls work without issue. I have yet to begin installation into the Gameboy shell because I need to double-check the battery charging circuitry. I would hate to finish the project, plug it in to charge and watch it explode.

This project has been put on the backburner since I have no reason to rush it and I want to take my time and do it right.

# Backlit GBA and GBA SP

Just a fun little mod to bring a backlit screen to the original GBA, and upgrade the one in the GBA SO. The motivation behind this project was nostalgia as I entered into my final semester of college and I wanted to push away the iminent reality of adulthood.

I've done a few of these mods at this point. All it requires is some minor soldering work and filing down part of the interior plastic.
