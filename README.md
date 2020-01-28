# Find the @boardname@ puzzle (using radio signal strength) 

For this project you have to use your @boardname@ to find four other @boardname@s in the top hall. You need to find them in the right order and then press button ``||A||`` to reveal a letter from each @boardname@.

The four letters are the first four letter of a five letter word which you can use to open a padlocked box, you'll have to make an educated guess at the last letter. If you open the box you will win the house points inside!

![Breakout Box](https://github.com/belmont-admin/SignalStrengthFinderInstructions/raw/master/docs/images/BreakoutBox.jpg)

## Introduction

You will use your @boardname@ with the STOP:bit lights attached to use as a signal strength meter so you can track down the location of the four hidden @boardname@s. Effectively you'll be playing a game of Hotter or Colder to find the @boardname@.
1. When you are far away from the @boardname@ the **green** light should come on
2. When you are nearer the @boardname@ the **yellow** light should come on
3. When you are right by the @boardname@ the **red** light should come on

When the @boardname@ recieves a message via a ``||radio:on radio received||`` message you also get the strength of the radio signal as ``||radio:received packet signal strength||``

Here's a number line which shows how the the value of ``||radio:signal strength||`` indicates a **strong** (green), **medium** (yellow) or **weak** (red) signal

![Number line](https://github.com/belmont-admin/SignalStrengthFinderInstructions/raw/master/docs/images/Number%20line.png)

## Step 1

You will find each @boardname@ by sending it a message which it will then echo back to you. You will send the message **"ping"**. A ping is a sound sent out by a submarine which then echoes back off any nearby object allowing the sonar operator to know how near another vessel is.

First you need to use the ``||radio:radio set group||`` block to set the radio channel to use for the message. The first @boardname@ you need to find uses channel **1**. Let's store that in a ``||variables:channel||`` variable so it will be easy to change later when you need to.

Also use a ``||radio:radio set transmit power||`` block to set the power to the maximum possible value of **7** so you can detect the @boardname@ from as far away as possible.

```blocks
let channel = 0
channel = 1
radio.setGroup(channel)
radio.setTransmitPower(7)
```

