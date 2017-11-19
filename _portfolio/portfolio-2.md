---
title: "Authentication Schemes for Wearables"
excerpt: " Cybersecurity research project under Prof. Memon at NYU Tandon School of Engineering. <br/><img src='/images/TL1.png'><img src= '/images/TL2.png'>"
collection: portfolio
---

**Date**: July 2015- September 2015

**Platforms used**: Swift/Xcode for Apple Watch OS 2.0., R package to plot data, Java/Android Studio for AndroidWear devices.

**Summary**: Investigated authentication schemes for wearable devices and proposed a novel rhythmic tap based authentication for smart watches. Traditional PIN based schemes are clumsy and not very secure. I implemented the proposed method on Apple Watch OS 2.0 and shown through a preliminary user study that it has high success rate like traditional PIN method yet it is more secure from shoulder surfing. The rhythmic PIN is essentially a 4 tap password that includes time between taps on the watch surface divided into 4 quadrants.  It is recorded as P = (q1, d1, q2, d2, q3, d3, q4) where qi corresponds to the quadrant for ith tap and dj is the delay between taps j and j+1. A password attempt is authenticated if its Euclidean distance to the password P is within a certain threshold. A study with a small group of users was done to measure success rate (repeatability) and shoulder surfing. The app logged the data into CSV files and R package was used to analyze and plot results. 

TapLock Success                   | TapLock Fail
:---------------------------------:-------------:
![Alt Text](/images/TLSuccess.gif)|![Alt Text](/images/TLFail.gif)

DrawPassword 	|
:---------------:-------------:
![](/images/DP1.png)|![](/images/DP2.png)
:---------------:-------------:
![](/images/DP3/png)|![](/images/DP3.png)

