# Find the @boardname@ puzzle (using radio signal strength) 

For this puzzle you have to use your @boardname@ to find four other @boardname@s in the top hall. You need to find them in the right order.  On each of the hidden @boardname@s pressing button ``||A||`` will reveal a letter from the padlock code and pressing the ``||B||`` button will reveal infomation on how to find the next hidden @boardname@.

The four letters are the first four letters of a five letter word which you can use to open a padlocked box, you'll have to make an educated guess at the last letter. If you open the box you will win the house points inside!

![Breakout Box](https://github.com/belmont-admin/SignalStrengthFinderInstructions/raw/master/docs/images/BreakoutBox.jpg)

## Introduction

You will use your @boardname@ with the STOP:bit lights attached to use as a signal strength meter so you can track down the location of four hidden @boardname@s. Effectively you'll be playing a game of Hotter or Colder to find the @boardname@.
1. When you are far away from the @boardname@ the **red** light should come on
2. When you are nearer the @boardname@ the **yellow** light should come on
3. When you are right by the @boardname@ the **green** light should come on

When the @boardname@ recieves a message via an ``||radio:on radio received||`` message you also get the strength of the radio signal as ``||radio:received packet signal strength||``

Here's a number line which shows how the the value of ``||radio:signal strength||`` indicates a **strong** (green), **medium** (yellow) or **weak** (red) signal

![Number line](https://github.com/belmont-admin/SignalStrengthFinderInstructions/raw/master/docs/images/Number%20line.png)

## Step 1 - Set things up

You will find each @boardname@ by sending it a message which it will then echo back to you. You will send the message **"ping"**. The word *ping* comes from the sound sent out by a submarine which then echoes back off any nearby object allowing the sonar operator to know how near another vessel is.

First you need to use the ``||radio:radio set group||`` block to set the radio channel to use for the message. The first @boardname@ you need to find uses channel **1**. Let's store that in a ``||variables:channel||`` variable so it will be easy to change later when you need to.

Also use a ``||radio:radio set transmit power||`` block to set the power to the maximum possible value of **7** so you can detect the @boardname@ from as far away as possible.

```blocks
let channel = 0
channel = 1
radio.setGroup(channel)
radio.setTransmitPower(7)
```
## Step 2 - Send out a "ping" message

Use a ``||radio:radio send string||`` block to send out the "ping" message when button ``||B||`` is pressed.

```blocks
input.onButtonPressed(Button.B, function () {
    radio.sendString("ping")
})
```

You should also make sure all the lights on the STOP:bit are off before sending the message. Here is the block added to make sure the red light is off

```blocks
input.onButtonPressed(Button.B, function () {
    pins.digitalWritePin(DigitalPin.P0, 0)
    radio.sendString("ping")
})
```
Now add two more ``||pins:digital write pin||`` blocks to make sure the yellow and green lights are also turned off.

## Step 3 - Process any echoes of the "ping"

Use an ``||radio:on radio received receivedString||`` block to write code which will run when a message is received back from the hidden @boardname@ that you are looking for:

Create a variable ``||variables:strength||`` and then set this to ``||radio:received packet signal strength||``

```blocks
radio.onReceivedString(function (receivedString) {
    strength = radio.receivedPacket(RadioPacketProperty.SignalStrength)
})

```
## Step 4 - Turn on a light depending on signal strength

Now use a ``||pins:digital write pin||`` block to turn on the green light if the strength is strong. Remember from the number line above:

1. If strength is greater then -60 the signal is **strong**
2. If strength less than -61 but greater than -80 the signal is **medium**
3. If strength less than -80 the signal is **weak**

```blocks
radio.onReceivedString(function (receivedString) {
    strength = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (strength > -60) {
        pins.digitalWritePin(DigitalPin.P2, 1)
})
```
Now click the **+** on the ``||logic:if||`` block to add an ``||logic:else||`` so you can add another ``||pins:digital write pin||`` block to turn on the yellow light if the strength is greater than -80

```blocks
radio.onReceivedString(function (receivedString) {
    strength = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (strength > -60) {
        pins.digitalWritePin(DigitalPin.P2, 1)
    } else if (strength > -80) {
        pins.digitalWritePin(DigitalPin.P1, 1)
    }
})
```
Finally click the **+** on the ``||logic:if||`` block again so you can add one final ``||pins:digital write pin||`` to turn the red light on

## Step 5 - Download your code and find the @boardname@

When your code is downloaded onto your @boardname@ you are ready to go into the top hall and find the first hidden @boardname@

Press your ``||B||`` button to send a "ping" and then see which colour LED lights up.

1. No light means you're **freezing**
2. A red light means you're **cold**
3. A yellow light means you're **warm**
4. A green light means you're **hot**

## Step 6 - Find the other @boardname@s

When you find the first @boardname@ you need to do two things:

1. Press its ``||A||`` button to display a letter. This is the first letter of the word which will open the padlock. Make a note of it on a piece of paper
2. Press its ``||B||`` button to dispay the radio channel you need to use to find the next @boardname@ this will be a number from 2 to 9. Again make a note of it on your piece of paper

Think carefully about what you need to change in your code in order to be able to find the next @boardname@

Pressing the ``||A||`` button on the second @boardname@ will tell you the second letter of the word which will open the padlock
Pressing the ``||B||`` button on the second @boardname@ will tell you which radio channel you need to use to find the next @boardname@

Pressing the ``||A||`` button on the third @boardname@ will tell you the third letter of the word which will open the padlock
Pressing the ``||B||`` button on the third @boardname@ will tell you which radio channel you need to use to find the next @boardname@

Pressing the ``||A||`` button on the fouth @boardname@ will tell you the fourth letter of the word which will open the padlock

## Step 7 - Open the padlock and get your prize!

You will have to guess what the fifth letter of the word which opens the padlock is but that shouldn't be too hard :)

Release the padlock by lining up the dials on the padlock to spell out your five letter word and then open the box to access your well deserved prize! 
