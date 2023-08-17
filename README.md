# Fibonacci-Generator-Using-Logisim


Working Principle:-
The Fibonacci Generator follows the same procedure as we do in any Programming Language:
def fibogen(n)
	a=0;
	b=1;
	c=1;
for I in range (0,n):
	print(a);
	c=a+b;
	b=c;
	a=b;
We have implemented this logic in the Logisim. First we have used 3 Registers of 32-bits  as variables. Registers stores the data and update the data when it’s clock pulse goes low to high. We use pull up registers to assigning 0(low) for Register clock inputs because without low signal clock can’t go high.

We gave the registers predefined values like A=0,B=1,C=1. Then we have used loop for updating the Registers. 1st print A which is 0, then update C to be A+B then done shifting of B=C, A=B.
We used control buffers for assigning B to 1(We didn’t directly connect constant 1 to B because it can create conflict). Control buffers decide whether to drive the signal on the output, when the bottom line also called control line goes low to high means 0 to1 it allows the signal to go through output line.

When we are setting the circuit we control one buffer to assign 1 to B, but when we are using the loop we drive value of C to B.
We used SR-Latch to control buffers. For assigning 1 to B we connected SR latch’s inverse/complement output to control buffer(when the Register B’s clock pulse will change it will assign B=1). The second output is connected to other control which is going to update B with the value of C when Loop starts. Also we connected output of B to input of Register A so the shifting of B=A can happen during Loop.

We have used multiple buttons connected to the different input of Registers and SR Latch. By manually press button Reset which  connected at clear line of all the components to clear data. Then press B button to load the B with 1 then press Enable button for enabling SR Latch. After that click button C to load data in register C. Press button it will update the content of A with C. By pressing button B you update content of B with C. Do this in order C, A and B. we can see output in probe in decimal format.






Making the Circuit Automatic:-

We want to control circuit automatically by enabling the clock and clicking one button.. For that we used demux control circuit. Demux circuit can be implemented by using a Demux with 2 selecting bits. At select line we used a counter(counter basically counts how many time signal goes low(0) to high(1)).
We have used an inverter at the input of counter the reason we want  the counter to  update to next line  of Demux when the clock output goes low if we don’t connect inverter it will send a signal to and count  at the same time which will not give correct output we want.

We have used a AND gate and SR latch at the input side where AND gate’s one input is connected to a clock(Frequency:2Hz) and second input is connected to the output of SR Latch. When the SR Latch is enabled the signal will go through AND gate and gives the signal to Demux.
The control buffers been used at output of Demux. 1st line of output is  connected to  both Register A and SR Latch’s clear line so both are zero at starting. 3rd buffer is connected to Register B’s clock input so it will update the Register B. 4th Buffer is connected to preset line of SR Latch to enable the SR Latch.
We have to disable the SR Latch in the Demux control circuit so we can enter our main loop. For disabling it we used a falling edge detector (when signal goes high to low it detect it and send a brief signal).

We made the falling edge detector using one AND gate and two NOT gates(When input is low(0) 1st input will be high(1) and 2nd will be low(0) but signals don’t propagate instantly there will be bit Lag at second NOT gate so for that one moment the edge detector will go high).
We connected the Falling edge detector to the third cycle so  when the Demux’s third cycle goes low the edge detector disables the SR Latch.


![image](https://github.com/Dangerpool0003/Fibonacci-Generator-Using-Logisim/assets/131488631/21852fd6-ad27-4b49-8654-6712a1c34984)

![image](https://github.com/Dangerpool0003/Fibonacci-Generator-Using-Logisim/assets/131488631/656b959c-c265-43fd-a990-41de38096cc3)



