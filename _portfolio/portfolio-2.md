---
title: "Pill Reminder"
excerpt: "An easy adjustable pill bottle cap that reminds users when to take their medication. <br/><img src='/images/PillLanding.png'>"
collection: portfolio
---

**Date**: March 2019 – April 2019

**Skills/Platforms used**: C++, CAD, Arduino, 3D Printing

**Summary**: Annually, there is an estimated 100 to 300 billion dollars in health care spending in the US that is incurred because people don’t take the medications they’re prescribed. Additionally, around three million older adults are admitted into nursing homes per year because of medication mismanagement. The aging population often have memory problems that make it difficult to manage taking their prescription pills at the right time. They also have weakened motor skills and dexterity from diseases such as arthritis and Parkinson's that make it difficult to open the child proof bottles that these pills come in, such as the push-down twist off cap. 

This project is aimed to help solve two problems related to medication bottles. The first one is the difficulty that people have opening these bottles, specifically the elderly. The second is to remind patients to take their pills at the correct time while having low power consumption. Hence, the primary deliverable for this project is a device that can be placed on pill bottles of any dimension that solves the two aforementioned problems. We believe that these problems are important to tackle as they would reduce medication errors and make the lives of people, especially the elderly, easier. Although there are existing devices of this nature, we believe that our design is unique because it fits to multiple cap sizes and can last on a single charge for over three years.

<figure class="video_container">
  <iframe src="https://drive.google.com/file/d/1WmsgLgFXXyfxLY3vVa-yg_yOvBjYullB/preview" frameborder="0" allowfullscreen="true"> </iframe>
</figure>

*Technical Overview*

The image below shows the the assembly of our final device. Once the user places the device on their bottle cap, they have a minute to set how many pills they are supposed to take daily, using the red buttons on the side. To reset this minute phase, the user can press the black button, which restarts the minute and resets the pill count. After this minute, the time interval for each pill is calculated. To let the device know that the user has taken a pill, they need to press the black button. If this button is pressed close to the time that the pill is supposed to be taken or after the buzzer goes off, the timer is reset for the next pill. If not, then a warning pops up letting the user know it’s not time to take the pill yet.

![Fully assembled device](/images/PillTop.png)

*Mechanical*

This device comprises of two parts. There were two main design choices made for the component holder. The first was to make a hex key insert to allow the cap to be placed on any pill bottle. This works by sticking the base hex key holder to the original pill bottle cap using an adhesive backing. The second design choice was to make the cap cross shaped so the cap is easier to grasp, especially for the elderly. The cross sections of the cap also allow for higher torque to be applied to the cap which is useful for the common twist off pill bottle caps.

![CAD images of hex key insert and holder](/images/PillCAD.png)
![CAD images of internal compartment](/images/PillCAD2.png)


*Hardware/Software*

For the microcontroller, we used a TinyZero Processor Board, which is developed by TinyCircuits, a maker of tiny open-source electronics. Its small size was helpful in keeping the device as small as possible. This board also has many different sensors and shields that it can connect to using its 32 pin connector. We used a seven-segment LED display and protoboard shields for the board.

The circuit used in this device comprised of the following components: the microcontroller and its sensors and shields, lithium battery, push-button switches, resistor and a buzzer. The switches were used to increase, decrease and reset the pill count and confirming that a pill was taken. We also had to account for some error in the switches. The switches had to be pulled down in order to eliminate electrical noise and receive a constant low signal when they were open. We also had to handle switch bouncing, which is where the switches mechanically bounce, causing the connection to toggle between open and close quickly and make a single press seem like multiple presses. To tackle this, we had a debounce delay, where we would wait till after a set amount of time to read the signal from the switch.

![Device internals](/images/PillInternal.png)

The code run on the microcontroller was written in C++, like an Arduino sketch. The code had a main loop which served as a state machine between the pill counting state and the reminding state. As aforementioned, in the pill counting phase, we would read signals from the up and down buttons. The reset/confirm button was configured to be an interrupt, so when it was pressed, the interrupt handler was called. The interrupt handler either reset the pill counter, displayed a warning or restarted the pill timer depending on the state it was in and how much time had elapsed. We also used the ​ArduinoLowPower​ library to reduce the current consumption of our device. While our device was in the reminding state, we put the SAMD21 microcontroller on the TinyZero board in standby mode. This meant that all clocks and functions unless mentioned otherwise are stopped. The following three instructions are executed for it to go into standby mode. First, the deep sleep bit in the system control register is enabled. This is a register in the CPU that controls the low power features for this processor. Next, there’s a Data Synchronization Barrier (DSB) instruction that is called to ensure that all instructions interfacing with memory occur in the correct order. Lastly, there is a Wait for Interrupt call, to wait for the interrupt to wake the processor up. As all the other clocks were turned off, we had to use the Real Time Clock on the microcontroller to keep time. This helped us maintain a state of low power.

To calculate the device’s battery life, we used the datasheets of the components and the following formula:

![](/images/PillEFormula.png)

Using this formula, we estimate the battery life to be approximately 3.11 years. This is because the device is in a deep sleep mode for a majority of its lifespan. However, this is only an estimate due to many variable factors such as temperature, pills taken and times the interrupt button is pressed.





