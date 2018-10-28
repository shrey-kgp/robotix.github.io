---
layout: post
title: "Cubiscan Tutorial"
categories:
 - event
image: img/tutorial/event/stax/image_7.png
---
#### Problem Statement

To Build a robot capable of detecting the dimensions of the block to estimate the volume of the block and then indicate the increasing order of volume of blocks.
#### USP

* Autonomous Traversal (Line Following)

* Dual axis sensor traversal 

* Estimation of object dimensions

#### Components List

| Materials											         | Quantity |
|-------------------------------------------------------------------|---:|
|Arduino Mega 												        | 1 |
|L293D Motor driver 									            | 1 |
|5V stepper motor with motor-driver board (ULN2003)		            | 2 |
|Rack and pinion                                                    | 2 |
|Chassis                                                            | 1 |
|IR sensor module                                                   | 2 |
|IR sensor Array                                                    | 1 |
|DC Motors                                                          | 2 |
|Wheels                                                             | 2 |
|Castor Wheel                                                       | 1 |
|Jumper Wires                                            | As required  |
|Breadboard                                                         | 1 |
|9-12V power supply                                                 | 1 |

#### Line Following

##### 1.IR LED Pair
**Working**- IR sensor or an infrared sensor consists of an IR LED coupled with a photodiode. This pair is generally called an IR pair or photocoupler. An infrared sensor emits infrared radiations which are detected by the photodiode. Resistance of photodiode changes according to the amount of IR radiation falling on it, hence changing the voltage drop against it. Further, by using the voltage comparator (like LM358) we can sense the voltage change and generate the output accordingly.

![](/img/tutorial/event/stax/image_2.jpg){:.img-responsive}

**Usage** - To follow a line, we can use the difference in reflectivity of the line and surface.

![](/img/tutorial/event/stax/image_6.png){:.img-responsive}

**Pseudo Code:**

{% highlight cpp %}
while(all IR pairs give low value)
{
	if (IR pair gives high value)

		{

			turn in the direction to stop receiving high value

		}

}
{% endhighlight %}

##### 2.IR Sensor Array

For better accuracy we can use multiple IR LED pairs in an IR sensor array.

![](/img/tutorial/event/stax/image_3.jpg){:.img-responsive}

![](/img/tutorial/event/stax/image_4.jpg){:.img-responsive}


#### Scanning

##### Dual axis scanning (rack and pinion)

To scan the block, the IR sensor needs to be moved along two axes. Alternatively, two IR sensors can be used and both the axis would be independent. To get the linear motion of the sensor, we use a Rack and pinion mechanism. This mechanism is used to convert rotational motion into translatory motion. By attaching a stepper motor to the pinion, we can get the translatory motion of the rack. To this rack, the IR sensor (to be used for scanning) will be attached.


![](/img/tutorial/event/stax/image_5.png){:.img-responsive}

##### Stepper Motor

A stepper motor is a brushless DC electric motor that divides a full rotation into a number of equal steps. The motor's position can then be controlled to move and hold at one of these steps without any position sensor for feedback, as long as the motor is carefully sized to the application in respect to torque and speed. <br>
The detailed tutorial can be found here.

##### IR Sensor

One IR sensor each will be attached to both the racks (one for horizontal scanning and one for vertical scanning). The Blocks will be white in colour so the IR sensors can be used to scan the blocks. The IR sensor will sense white when the block is in front of it and it will sense black when the block is not in front of it. By counting the no. of steps taken by the stepper motor while the IR sensor is sensing white colour, the dimensions of the block can be determined.


#### **Pseudo Code**

Vertical Scanning 
{% highlight cpp %}
while(block exists)
{
	Move sensor up and count;
}
Use the value of count as measure of height;
{% endhighlight %}


Horizontal Scanning
{% highlight cpp %}
if (block edge detected for 1st time)
{
	Move sensor horizontally and start counting;
}
if (block edge detected 2nd time)
{
	End counting and use this count as a measure of width; 
}
{% endhighlight %}

