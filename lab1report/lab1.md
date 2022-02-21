<!-----

Yay, no errors, warnings, or alerts!

Conversion time: 0.799 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β33
* Sun Feb 20 2022 22:48:01 GMT-0800 (PST)
* Source doc: Lab 1 Report
----->


**EE 133: Intro to RF Systems Laboratory**

**Lab 1: The Secret Life of Passive Components**

**And**

**We meet a new friend, the VNA**

**Author: Marc Huerta**

**Lab Partners: Ben Clark and Devorah Simon**


                        **_Instructor:_**


                        Steven Clark


                        Lecturer


                            Electrical Engineering Department


                        David Packard Building, Room 112


                        350 Jane Stanford Way


                        Stanford, CA, 94305-9505


                        +1 650 723 1660


                        [steven.clark@stanford.edu](mailto:steven.clark@stanford.edu)

**Abstract**

In the process of making and designing real systems whether it be any fun gizmo or especially a more serious measurement or precise system we need for a variety of purposes, it is important to model things before realizing them. Though it is not always the case that if a model works the real life translation will, better models provide a higher chance of success for our systems we design and a higher chance they do what we want them to do with good precision. Though I had not much initial experience with much of the instrumentation we used in this lab (like a VNA or even with modeling components in simulations), by the end of the lab I was able to understand more thoroughly what a VNA does, how to use it, and how it can help us in understanding unintended parasitics in real components like capacitors. Thus in understanding these parasitics and how to use these instrumentations, I am now in turn able to use these abilities in the future when I need to model something or am planning to work on a project that requires some sort of modeling; additionally I also have a better understanding of passive components as a bonus.

**Introduction**

As the first real lab of the quarter, we were given a lab handout and were given instructions on what to do and objectives on what we should hopefully learn by the end of the lab. Among the objectives, they included understanding how to use a VNA and then from there knowing and understanding the passive components we had in the lab via the VNA and simulation. 

Before the lab, I was rather unfamiliar with what a VNA was or what it really did so as the lab progressed, one of my goals was to really figure out how useful this tool was and what it tells us about components or things we’d like to measure. Among other goals I had after reading through the lab handout with regards toward using a VNA, I needed to know how to not abuse the VNA (not exceeding its capacities or abusing its ports), I needed to know how to calibrate a VNA (and why it’s necessary to in the first place), and finally wanted to know how to read and measure different components on a VNA. After doing this, the plan was then to use the skills I had gained by using the VNA to get a better understanding of my physical components and then model them better in software like LTspice.

**Experimental Setup**

To start, we were given mini-VNAs and had to learn how to use these little VNAs. Specifically it was the NanoVNA2 Plus4 ( shown in **Figure 1) **which are small but relatively affordable VNAs that were essentially ‘good enough’ to get most of the measurements we needed. The best thing about it was that there was some open source software called vna_qt available to interface the VNA with our computer and view the smith chart and data from the VNA on the computer.

After establishing familiarity with our NanoVNA, we could move onto calibrating, then onto measuring, and finally reporting. The first part of this setup was calibrating the VNA. After getting the NanoVNA software downloaded and booted, we connected and powered on our NanoVNA to our computer to interface with the software. On the software, it gives us options for calibration and on the webpage for the software, it also shows us what steps exactly to do for calibration. Within the lab handout as well, it reminds us of SOLT and how we should calibrate. First calibrate the short, open, load, and finally the through! All went smooth and with our connected wires and we calibrated the VNA successfully.

From then on we had our testing board which contained different passive components and filters. This was the RF demo kit board (shown in **Figure 2). **Having calibrated the VNA, we could then capture what these components looked like on the smith chart shown on the VNA.

Finally, for the last part of the lab, we soldered a copper ground plate to 2 SMA connectors and with the VNA measured and swept (after recalibrating the VNA of course) to find the resonance frequencies of an inductor and a capacitor. We could also see the reflection from port 1 to port 1 of the VNA which also tells us about the components and should match almost the opposite for the through (2 to 1) measurements. This was essential for helping better our spice model of these components.

**Measurements and Results**

We’ll first quickly go through some of the measurements we got on the VNA while measuring the RF demo kit. For the most part, a lot of the measurements were consistent with what the RF demo kit (**Figure 2) **said they should look like so I won’t show all the measurements we took, only some good examples to note.

The first measurement we’ll look at is some basic resistors we measured from the RF demo kit as shown in **Figure 3**. As we know them to be, resistor impedance is real and the middle line and axis on the smith chart plots real values so we expect the resistor to lie on that axis and it does. It also matches what **Figure 2 (components 3 and 4) **said they should look similar to as well. We see here that it does sweep a bit up towards being a bit inductive but this is due to parasitics as we swept from 0 to 200mHZ.

More on the smith chart, with the rest of the results we know that resistors should lay across the middle line, capacitors span the bottom half of the chart, and inductors span the top half. Of course none of the components look exactly precise but they look very close but the point of the VNA is to see how un-ideal they are in a sense as the RF demo kit shows us their ideal smith charts. 

Next, we’ll be looking at the components with complex impedance: a capacitor and inductor. For these, the capacitor should span the bottom side of the smith chart and the inductor the top half as just aforementioned. We show these to be approximately what we measured in **Figure 4** as the inductor was a tad bit more un-ideal but this is a little more expected due to just the general build of an inductor and all the paratstics that inherently come from it more so than a capacitor.

Finally, the last of the RF demo kit VNA measurements I’ll be showing is of some of these components in series and parallel. Looking at **Figure 5**, we see component 2 from the board. It is a capacitor and inductor in series in parallel with a resistor. As the frequency gets sweeps, it goes from being real at low frequency so it’s just the resistor on the real axis, then sweeps to being more capacitive til it meets its resonant frequency where its equally capacitor and inductive and energy is just oscillating between the 2 components and then finally ends up being more inductive as the capacitor acts more like a short at high frequency. 

Next we have what the individual components we measured were. These were the ones we soldered onto a copper plate with SMA connectors and then soldered the ends of the passive components to the middle connection of the SMA connector. We measured a capacitor first and this is what the smith chart for it looked like as seen on **Figure 6. **What we can gather here is that the self resonance frequency is at around 30MHz. How see this is from the S11 blue measurement on the VNA display, we see at that frequency, a dip happens to around -35db. I take this to mean that at that frequency, the circuit isn’t reflecting back as much as it was and instead is absorbing and dissipating energy out from itself as it does when it resonantes. This also largely looked as it should as we can see the resonance frequency here where it starts acting like an inductor for a little then goes back to being capacitive after crossing the resonance point.

For the inductor we got a little bit of an iffy/weird smith chart but since an inductor is a less ideal component, I just casted it away to that though it was still pretty ugly barring that.When things don’t look right to me, I ask around and look to my peers for guidance and just check in to make sure I am not completely off; I did so in this situation and the ones whom I asked said their measurements for the inductors looked similar as well. Looking at **Figure 7, **on this smith chart it appears there's really almost 2 points where it resonates and acts as a capacitor for a good chunk of the sweep as it dips and spirals into the lower bottom half of the smith chart. I attribute this too as well to the fact that when the inductor gets really high in frequency, it acts like an open so more of the parasics and capicances may take over when the set up I soldered on the inductor too didn’t have the best insulation and protection from parasitics. Yet still, it had it’s largest resonance frequency at around 111 MHz so this is what we’ll want to simulate later on.

Finally onto the LTspice simulation, we can see that what we simulated isn’t quite exactly what we measured in real life but we adjust it as we go to try and understand the parasitics of components and just generally the setup of them. Below on **Figure 8** is the spice simulation for the capacitor which we see goes downwards in it’s resonance and then goes back up as the capacitors allow high frequencies through. For this model, I had to tweak the inductance which I believe to be high because of the set up of the board and how close the plates and connectors all are to each other–it was a bit messy and caused some ugly parasitics. Yet still, I was able to get the simulation to peak at around a resonance of 30MHz as we got in real life.

The opposite is then true for the inductor which only allows low frequencies to pass so we see it go from allowing low db to peaking and allowing some frequencies through at its resonance frequency which we measured and then simulated to be around 110 MHz shown in **figure 9.**

**Discussion **

For the first part of the lab, everything was rather smooth, it was more controlled and less room for error so it makes more sense why that first part went smooth. When it comes down to the second part of the lab and measuring the capacitor and inductor values, then more problems come in with various things. First to start, the chart on the inductor is very unideal (more so than expected at least). Explanations for this could be lots of parasitics due to how we soldered and measured on the inductor and also just the fact that inductors are just a very unideal component relative to capacitors. Yet, with simulations, we were able to still model the resonant frequencies but not all of them as oddly measured on the VNA.

I used values given in a practice simulation from the lab handout and quite frankly don't understand where the values came completely from but if we can better model the whole system setup with the SMA connectors and copper board, I’d assume it’d be a bit closer to modeling our passive components as well. All in all, I do feel more confident in using a VNA to look at the behavior of components and then apply this gathered information to models.

**Summary**

All in all, the lab allowed me to work with VNA and passive components and get a chance to understand each respective one more via using the other other respective one and that goal was definitely achieved. I feel more comfortable understanding a VNA now and it is cool to see just how ‘unideal’ a passive component can be and how we do in fact get a 3 for 1 deal when it comes to passive components. Physically seeing these parasitics and measuring them for myself to then go ahead and model in a simulation gives me great insight and hands on experience which I lacked beforehand when I was simply just told that these components have paratics but never knew how to measure or even model them.
