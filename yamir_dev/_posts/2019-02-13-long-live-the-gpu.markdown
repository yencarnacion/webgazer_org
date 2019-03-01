---
layout: post
title:  'Long Live the "GPU"'
author: Yamir Encarnacion
date:   2019-02-13 16:30:00 -0400
categories: update webgaze
---
Long Live the "GPU"
===================

This post is an articulation of an observation that a lot of the boom 
we are currently seeing around artificial intelligence/machine learning/deep learning 
will have the ultimate result that low power “GPUs” (Graphical Processing Units) 
will be everywhere.  See 
[https://www.gartner.com/smarterwithgartner/gartner-predicts-the-future-of-ai-technologies/](https://www.gartner.com/smarterwithgartner/gartner-predicts-the-future-of-ai-technologies/). 

Part of the logic behind the statement above relies on the realization that it is not 
always practical (and it is sometimes impossible) to send all the data required for 
Artificial Intelligence (AI) up to the cloud, where computing resources are more abundant. The 
sea of data just does not fit through the bandwidth straw up to and down from the cloud. See 
[https://www.statista.com/statistics/471264/iot-number-of-connected-devices-worldwide/](https://www.statista.com/statistics/471264/iot-number-of-connected-devices-worldwide/). Also, 
reliable global communications are not here yet.  Google reported in 2018 that 60% of 
mobile communications worldwide are over 2G.  See [https://www.youtube.com/watch?v=Hq026dfyIqU&t=85](https://www.youtube.com/watch?v=Hq026dfyIqU&t=85).

The logic behind the “GPU” statement above also derives from the fact that current 
machine learning/deep learning relies heavily on a lot matrix multiplications being 
performed really fast. But, the General Purpose Processors that are found on most 
electronic devices are not particularly good at matrix multiplications.  On the 
other hand, Graphic Processing Units (GPUs), like those made by 
[nVidia](https://www.nvidia.com/) excel at parallel matrix multiplications.  

While the GPU -- or whatever marketing decides to call these fast matrix multiplication 
devices in the future -- is a necessary component of modern day machine learning, a 
modern day GPU would not be realistic in everyday situations.  For the AI powered by 
machine learning to be realistic with “just” our phones or at the 
“[edge,](https://en.wikipedia.org/wiki/Edge_computing)" you also need the calculations 
made by these “GPUs” to consume low power.  An nVidia GPU can consume 250 Watts - which 
is way too much for a low cost device running off a battery.  For reference, the USB 
adapter for charging the iPhone is 5 Watts.  See [https://www.apple.com/shop/product/MD810LL/A/apple-5w-usb-power-adapter](https://www.apple.com/shop/product/MD810LL/A/apple-5w-usb-power-adapter). Something 
like the [Intel Neural Compute USB Stick](https://software.intel.com/en-us/movidius-ncs) is closer to what is needed.  The Intel USB stick can produce results while using just 1 Watt.

To recap, I believe we will soon see a lot of low cost, low power, massively parallel 
computing devices capable of extremely fast matrix multiplications for the purpose of 
enabling Artificial Intelligence at the edge.  I called the massively parallel 
computing devices “GPUs” in this post for lack of a better word.

--
Edit on February 14, 2019:  
The article at [https://www.technologyreview.com/s/612722/cheaper-ai-for-everyone-is-the-promise-with-intel-and-facebooks-new-chip/](https://www.technologyreview.com/s/612722/cheaper-ai-for-everyone-is-the-promise-with-intel-and-facebooks-new-chip/),
which I just learned about, validates my post.  It was published on January 7, 2019.

--
Edit on February 18, 2019:  
The article [Facebook joins Amazon and Google in AI chip race](https://www.ft.com/content/1c2aab18-3337-11e9-bd3a-8b2a211d90d5) published
by the Financial Times on February 19, 2019 in the UK (hence the time travel) is also related.


