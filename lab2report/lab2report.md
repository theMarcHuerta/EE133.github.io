**EE 133: Intro to RF Systems Laboratory**

**Lab 2: Build An Oscillator, NOPE! Buy a clock generator, YUP!**

**Author: Marc Huerta**

**Lab Partners: Ben Clark and Devorah Simon**


                        **_Instructor:_**
                        Steven Clark
                        Lecturer
                        Electrical Engineering Department
                        David Packard Building, Room 112
                        350 Jane Stanford Way
                        Stanford, CA, 94305-9505

**Abstract**

This lab was based around understanding the value of learning transferable skills in a lab/class setting. In this lab, we worked with a clock generator– namely the Adafruit Si5351A and used a microcontroller (the ItsyBitsy) to control it. The goal of working with premade clock generators is to show we don’t want nor need to build everything from scratch; there is no reason to if that is not our domain of specialization. It is more efficient for engineers with time constraints to take proven hardware that has already been tested and is better than any oscillator we could waste time building. In the lab, we also took time to practice the skills it takes to do research on a piece of hardware, and learn of any extra accessories (like a microcontroller) that are necessary to fully get the functionality we want out any hardware piece we want to integrate into a more general purpose gizmo we’d like to make.

**Introduction**

For many engineering students, most lab experiences early on in their academic career are made with the goal of not always learning and taking away skills that can be broadly applied in the future but rather with the goal of simply completing a lab and answering a couple lab questions. This is brought up because it is important to approach this lab differently than we would the traditional labs we’ve had. When reading about this lab from the announcements tab on our class page, it was relatively more broad than a structured traditional lab. Realizing that especially in this class one of the primary goals is to take away transferable skills from the things we do and learn, it made more sense as to where we were going with the learning goals of the lab.

The goals still stood of actually understanding how to use a clock generator and even using an oscilloscope and VNA to see just how good of a clock generator it was; that was a large part of the report which I will be going over as well. Yet, in this introduction, let’s emphasize the skills that were gained as a result of having to dig through websites and pages to find information/code that was needed to be able to run the clock generator through ItsyBitsy. More of the technical discoveries made will be shown in the latter parts of the report such as investigating a bit on how the clock oscillator works internally on a high level and looking at how we can tell when the clock generator works best.


**Experimental Setup**

To begin, let’s list out the 2 main physical pieces of hardware we were given to start this lab. Firstly as already mentioned, we were given a Adafruit Si5351A Clock Generator Breakout Board and secondly we were given an Adafruit ItsyBitsy M4 express. Of note right away is that they are both parts made by Adafriuit so the hope with this is that the ItsyBitsy will have support in the form of a code library to help us interface face with the Si5351A. To recap this first step, we got these 2 pieces of hardware and soldered on three end-launch SMA connectors onto the clock generator breakout board. We then with some jumper wires connected the corresponding pins from the breakout board to the microcontroller and double checked on the breakout board documentation if these were the correct pins to connect the board to. The put together board can be seen here in **Figure 1**. 

<p align="center">
  <img src="images/image1.jpg" width="500" height="400" />


After getting the hardware setup on the board, we moved onto using the microcontroller to interface with it. This where the transferable skills of self research into a manufacturers websites came in handy. Though we were given a good starting point from our instructor as to the links to look towards, it still took a bit of digging to find what we needed. To summarize quickly what we did to get set up with the software side of things:

* We first download the recommended editor to interface with the ItsyBitsy which is the Mu Editor in this case
* We then read documentation on how to load up the ItsyBitsy by updating the bootloader on the ItstyBitsy and then installing CircuitPython onto it which allows us to use the necessary libraries we’ll need to control the clock generator as we please.

After doing all these steps and sifting through various libraries to download and run the clock generator with ease, we got to this point as shown in **Figure 2** where we had editable code and could run 3 different clock frequencies on the breakout board!

<p align="center">
<img src="images/image2.jpg" width="500" height="420" />


**Measurements and Results**

Before we can formulate more specific questions, the first and most important question to start measurements off with is “does this work” and then possibly even more importantly ask “does this work well… if not, then why?”

To start with the cleanest output we got, we refer to clock 2 running at 10.7KHz as we see in **Figure 2**, the bottom of the screen is the serial output which is coded to show us frequencies each clock is running at. Here is a good point to form a basis of how internally the Si5351A does this at the level of a block diagram. Shown below in **Figure 3.** Essentially what the code does is it sets each PLL (both A and B) to a multiple frequency of the onboard 25MHz reference crystal. Within the PLL part of the diagram, there is some internal multiplier that does this and with the arduino and I2C interface, we can set the multiple of the local reference oscillator we want the PLL to be set to. Then for the clock output, it divides this intermediary frequency using fractional dividers which essentially just means it can divide this intermediary frequency fractional by a divisor of 1MHz to 100KHz. The range on an output of a clock is said by the manufacturer to be 160Mhz to as low as 8KHz.

  
<p align="center">
<img src="images/image3.jpg" width="500" height="350" />


A good clock oscillator looks ideally like a perfect square wave. We do know that due to the fact we can’t have infinitely summed high frequencies, there will be imperfections in a recreated square wave, usually some sort of Gibbs phenomenon which leads to peaking at the rising edge of the clock and at the falling edge. Now we look at **Figure 4** on the left hand side, we can see that the 10KHz clock signal on the oscilloscope looks pretty good like a square wave with some of that gibbs phenomena discussed. On the right hand side, we see a measurement on the VNA (this picture taken courtesy of lab partner Devorah Simon). We see there is relatively low noise surrounding the signal as well. 


<p align="center">
<img src="images/image4.jpg" width="500" height="350" />


Going into the 13MHz clock, we start to see both more noise on the spectrum and see the square wave start to look a bit uglier and imperfect. This is caused by several reasons. First of all, a probe was used to measure the clock generator output and it had the unintended consequences of adding extra unwanted capacitance to the signal measured. As a result, this extra capacitance forms a low-pass filter which filters out high frequencies and hence, makes the square wave look uglier at higher frequencies. The probe also has limited bandwidth lower than the oscilloscope which has a bandwidth of 500MHz so this also contributes. Below in **Figure 5**, is a set up of the probe (left) along with the measured 13MHz clock signal (right).

  
<p align="center">
<img src="images/image5.jpg" width="500" height="350" />


Finally for our last measurement, clock 0 is the output of the clock generator breakout board. Again there was much noise gathered here that made the signal look bad as it did for the 13MHz one. Comparing the SNR on the VNA of the 10KHz clock and this 112MHz clock, we can see a lot more phase noise as the peak is more broad as well in **Figure 6** and the SNR is lower than it was in the 10KHz spectrum. The amount of noise we can see here compared to the 10KHz signal indicates that it is not a low noise part.

  
<p align="center">
<img src="images/image6.jpg" width="500" height="330" />


**Discussion**

This will be a brief discussion of some of the possible applications. |Reading through data sheets tells you good applications of whichever piece of hardware you would like to use because they want you to use it and want you to buy the part. What was located on the Adafruit clock generator datasheet was a bit disappointing. The things it’d be useful for included generating synchronous signals and asynchronous signals– which we expected. The synchronous signals would be good for a PLL and also being able to have a running reliable clock could eliminate the need for a general oscillator or VSCO depending on your application. The hope was that the datasheet would tell more beyond this but knowledge of a PLL and its applications would be enough to find other uses so the datasheet refrains. 

**Summary**

All in all, this lab helped bolster the idea of self-research and the importance incompetence in research parts that one is interested in using. Having a sense of where to look and what to look for (for example a software library) can make the process go faster and smoother. Engineers always would like to make processes simpler and quicker; we accomplished this in this lab by avoiding 1. Building a piece from scratch (like an ossocialtor) and 2. Writing code from scratch for hardware we’re unfamiliar with. Along the way, we also got to keep working with oscilloscopes and VNAs and through testing (and some errors) picked up some tidbits of knowledge and understanding which will be useful going forward. Again, these are practical skills that can transfer over to working on projects such as our final project for this class.
