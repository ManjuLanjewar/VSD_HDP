##### Introduction to Circuit Design and SPICE simulations

Cicuit Desgin : All logic gates are made-up of PMOS and NMOS transistors connected in very particuar fashion and once they are connected in that fashion ,
they perform required functionality of that particular respective gate. 

Spice Simulation: This particular Circuit has to be fed in with some waveforms to identify output charactristics and simulate using spice.
Simulated waveforms decides delays of particular cell. Based on value of delay, tune W and L ratio of particular transistor. 
W/L ratio is factor that decides the value of output current which eventually decides waveform shape, which decide delays of particular cell. 
To tune delay, how to tune W/L ration, is basically obtain using Spice simulation. 

Why do we need simulation? 
In physical design flow,  whatever we are doing in clock tree, timimg, crosstalk they are built on spice. 
If no SPICE, then there is no term delay. If no delay then clock tree, timimg , crosstalk doesn't make any sense. 
From where delay of cell comes from? 
To check Delay models are accurate? supply same input slew and output load in SPICE simulation and get delay value from SPICE and 
match it with delay table value. 
To verify static timing analysis is correct? delay values, slack values in STA are correct or not? 
Source of delay table comes from SPICE. 
Spice simulation involves characterisation of PMOS and NMOS transistors into details or any CMOS logic int odetails.

**** NMOS transistors and their characteristics. 

NMOS is n-channel Metal Oxide Semiconductor built on p-substrate 
It is a four terminal device.
It consists of a P-substrate body
It has 2 isolation regions, differentiating between two transistors. 
It has 2 n+ diffusion region is present near the SiO2 layer.
It has a Gate oxide layer
A Poly-Si (metal gate) layer is placed on top of the gate oxide layer and this form Gate terminal, which drive NMOS.
4 terminals mainly G - Gate, S - Source, D - Drain, B- Body or Bulk 
Terminal B in NMOS is grounded but important to understand threshold voltage charactersitics of NMOS. 

![image](https://github.com/ManjuLanjewar/vsd-hdp/assets/157192602/ebe16b5a-bcf0-4f76-a3c9-1a47c2e44c21)

PMOS is just an inverted NMOS (p+ on n-substrate) but all other characteristics are common.

Basically there are 3 modes of operation. Cutoff, Resistive and saturation 

- Threshold Voltage (Vt)

    - The threshold voltage accurately describes the transistor. 
    - For an NMOS, when Vgs=0, and drain, source and bulk connected to ground. 
      So, substrate Drain (B-D) and Substare Source (B-S) forms p-n junction diodes connected back to back. 
    - Both junctions are off due to 0V bias. Hence S-D resistance is high.
    - In p substarte, majority charges are positive charges and minority are negative charges. 
    - Now if we apply a small +Vgs, metal gate is positively charged, this gate terminal area form oxide capacitance 
      and repel all positively charges present in p substrate, leaves behind negative charges. so, a negatively charged region (depletion region) forms        between n+ regions. 
    - Now if we keep increasing Vgs until Vgs = threshold voltage = Vto (Vsb=0 here, and Vto is a function of process manufacturing), 
      we get strong surface inversion.

• Threshold Voltage (Vt)

    The 'Vgs' voltage at which 'Strong Inversion' occurs is known as Threshold Voltage (Vt)

• Concept of Strong Inversion

    The phenomenon at which a part of the P-substrate becomes N-substrate (due to the high Vgs value) is called 'Strong Inversion'

Further increase in Vgs, there is no change in depletion region width. Electrons from heavily doped n+ source region are drawn in region under Gate 'G'.
Continuous n-channel formation from S-D, whose conductivity is modulated by Vgs.

If we keep increasing Vgs now, a continuous channel is created between n+ (gate attracts negative n+ as no p+ are left to repel, they are all depleted) -> cutoff region. 

• Impact of Source-to-bulk Voltage (Vsb)

    In presence of substrate bias voltage 'Vsb', an additional potential is required for strong inversion to occur.

If Vsb is positive (with D grounded and 'Vgs' small voltage to form depletion region),the depletion layer width increases near S due to reverse bias between Source 'S' and substrate (or Bulk) 'B'

Now as Vgs increases in this case, the negative charges formed due to depletion are attracted towards the S terminal which is connected to positive node of voltage source. 

When Vsb = 0, Semiconductor surface inverts to n-type material at voltage Vgs = Vto.

When Vsb is positive value , Semiconductor surface inverts to n-type material at voltage Vgs = Vto + V1

In presence of substrate bias 'Vsb', additional potential is required for strong inversion. 

Now, if Vgs increases again, inversion gets delayed. This needs additional potential to achieve strong surface inversion whereby it happens for 

• Threshold Voltage Equation

Screenshot of equation (Day1 - L4)

where

    - Vto is the Threshold Voltage when Vsb = 0 and is a function of manufacturing process
    - ϒ is the body effect coefficient and it expresses the impact of changes in body bias 'Vsb' (unit of ϒ is V^0.5)
    - фf is the Fermi Potential

• Body Effect Coefficient expression

screenshot of equation (Day1-L4)

where
    - εsi is the relative permitivity of silicon (=11.7)
    - NA is the doping concentration
    - q is the charge of an electron
    - Cox is the oxide capacitance

• Fermi Potential Equation

screenshot of equation (Day1 -L4)

where

    ni is the intrinsic doping parameter for the substrate

###### NMOS Resistive region and Saturation region of operation

- Resistive region

    - It is also known as the Linear Region of operation
    - Since, Vgs=Vt, let us observe what happens at different voltages of 'Vgs>Vt'.
    - As Vgs increases, channel width increases. Means induced charges because of gate voltage is proportional (Vgs-Vt) which is potential needed to
      turn on transistor i.e. Induced charge (Qi) α (Vgs-Vt)
    - The analysis is performed at Vgs=1V and a small Vds (Say 0.05V). Assume Vt(NMOS) = 0.45V

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/2a0a281f-e6ab-411f-8bc3-a9287613e8d6)

    - In absence of Vds, the voltage across the n-channel was constant but with application of Vds it is no more constant.
    - Let the effective channel length be L and 'x' axis represent the channel length and 'y' axis represent width perpendicular to the channel length
    - Let V(x) be the voltage at any point 'x' along the channel.
    - In absence of Vds, every point on channel had got Vgs voltage. With the application of Vds, every point on channel will have volatge of Vgs-Vx.
      V(x) is differnet at every point 'x' along the channel.
    - Effective channel volatge or gate-to-channel voltage on application of Vgs will be Vgs-V(x).
    - At every point in channel, volatge will vary. This lead to current flows from source to drain. Drain current drive delay of cell. 
    - Therefore, in the channel, induced charge at any point 'x' Qi(x) α - ((Vgs-V(x))-Vt)
    - First order analysis
![Screenshot from 2024-03-04 23-27-52](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/87d3f155-1e12-4691-950d-5ad42b9e34dd)

tox is oxide thickness, i.e. gate oxide present between gate and P-substrate which is constant. 

From device point of view, there are two kinds of current: Drift current and Diffusion current

    * Drift current is the current due to the potential difference
    * Diffusion current is the current due to difference in carrier concentration

• The drift current (Id) = (velocity of charge carriers * available charge) over the channel width

![Screenshot from 2024-03-04 23-44-06](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/5be22502-3001-49a0-8d3b-cef70aad5343)
above is snapshot of top view of the MOSFET showing the channel width 'W'

Here focus is on the drift current, Id, (velocity of charge) that is flowing over the channel width.

• Drift current (Id) formula

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/ab3230a8-cbac-4e2f-8727-e8629ddaf894)

    - The term µn.Cox is denoted by kn' and kn' is known as process transconductance
    - kn'.(W/L) is denoted by kn and kn is also known as gain factor
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/4c8892aa-6518-49a3-8a60-219c33f55b08)

• Condition on Vds for the MOSFET to be in linear/resistive region or saturation/pinch-off region

    * When Vds <= (Vgs-Vt), the MOSFET is in linear region of operation
    * For this region, Id=kn.(Vgs-Vt).Vds as (Vds^2)/2 is a very small amount in this case
    * Vds can be sweeped from 0V to (Vgs-Vt) to make the device work in linear region of operation

Spice Simulation is used to calculate Id for different values of 'Vgs' and at every value of Vgs, sweep Vds till (Vgs-Vt) using linear equation for Id. 

Dependance of Id on Vds in pinch-off region

   - The chanel voltage is denoted with Vgs-Vds
   - Pinch-off condition is when Vgs-Vds=Vt
   - When the Pinch-off phenomenon is started, the channel begins to disappea. Basically, the channel starts to disappear only from the Drain side           acquiring a triangular shape.
   - When Vgs-Vds<=Vt, there is no channel present near the Drain terminal
     
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/49b9df56-f87d-4a38-9215-27a9e7721216)

   - Id becomes (kn/2).(Vgs-Vt)^2
   - It looks like a perfect current source i.e current is constant. It is not true because effective conductive channel length is
     modulated by applied Vds.
   - As Vds increases, the depletion region at the drain terminal increases and hence, the effective channel length decreases.

    Now the Drain current equation becomes:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/d82b73b5-fe52-422a-8835-e56203b716fe)

Here, λ is the channel length modulation

###### Introduction to SPICE 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/0bac5469-a87c-4598-8ae0-2ed9dfce57e1)

in above snapshot, yellow highlighted are called Spice model parameters which are constants. 
First check is to identify weather model parameters coming from correct technology node or not? 
Spice model parameter + Spice netlist when feed to Spice Engine then we get desired output waveforms.
The spice waveforms can be used to calculate the delay of a cell. These delays are very close to the practical delays observed used for STA.

Spice Netlist

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/8b0530f7-a056-46e5-90b5-38536a09b317)

The snap shot of SPICE netlist of the above NMOS

   - R1 is protection resistance is added as it is not desired that the current from Vin would be directly fed to the gate of M1.
   - Source and substrate connected to ground.
   - SPICE syntax
     Identify nodes. In above snapshot, blue dots shows nodes. Then names nodes. Here nodes are name as in, n1, vdd, 0.
       - Definition of nodes and the method to identify them
          * A node is can be defined as a point connecting two termials. If two terminals of a single device are short circuited then the node
            is said to be in between these two terminals. But most of the times a node connects two different devices.
          * The method to identify nodes is to identify the SPICE netlist for the device and all the wires connecting different components
            have one node on them.

    <pre>M1 vdd n1 0 0 nmos W=1.8u L=1.2u 
           Here , M1= MXX= MOSFETXX (M stands for MOSFET and XX can be any number. Here it is 1) 
                  vdd- Drain
                   n1- Gate
                   0- Source
                   0 - substrate
                nmos- MOSFET name in Technology File.
                  W - Width of channel
                  L- Length of Channel 
                  
           R1 in n1 55
             Here, RXX= ResistorXX=R1
                   R1 is in between in (first terminal) and n1 (second terminal and value of R1 is 55ohms
           Vdd vdd 0 2.5
            Here, VXX- Volatge Source XX - Vdd
                  Vdd between vdd and 0 
                  2.5 - Volatge Source value
           Vin in 0 2.5
             Here Vin between in and 0 and value is 2.5</pre> 

- Define Technology Parameters
     Vt, Id (Saturation region), Id (Linear Region) are Model of NMOS.
     To evaluate these models, model parameters are needed.

Before writing a netlist, we need to define names for the nodes in the circuit.

To include a technology file then define a resistor, transistor, voltage source, and a capacitor use the syntax below:

     <pre>.LIB "<name: xxx>.mod" CMOS_MODELS
     R<name> <1st node> <second node> <value>
     M<name> <drain> <gate> <source> <bulk> <name in tech file> w=<value> L=<value>
     V<name> <1st node> <second node> <value>
     C<name> <1st node> <second node> <value> </pre>

Technology file (xxx.mod) of NMOS and PMOS should have the following syntax: 

<pre>.lib cmos_models
.Model <name that should match in netlist> NMOS (TOX = .. VTH0 = .. U0 = .. GAMMA1 = ..)
.Model <name that should match in netlist> PMOS (TOX = .. VTH0 = .. U0 = .. GAMMA1 = ..)
.endl</pre>

To simulate a spice netlist with sweeping (left side will be sweeped for each value on the right side), use the following syntax in the netlist:

.<mode: dc> <voltage node to sweep: Vin> <start value: 0> <end value: 2.5> <steps: 0.1> <voltage node to sweep: Vdd> <start value: 0> <end value: 2.5> <steps: 2.5> 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/949a8d75-dbb5-441e-91bc-620ec375fb09)

To use ngspice for plotting, use the following commands:
<pre>ngspice <spice file name>
plot -<name node></pre> 

   -  Method to save SPICE model

    - Method to write code for SPICE simulation


#### Day 2
<summary>velocity saturation and the basics of CMOS inverter Voltage Transfer Characteristics (VTC)
</summary>

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/28c8ee57-f423-437a-8a4e-9c6f22be7568)

The snap shot of various regions of operation of NMOS on graph plotted between Ids and Vds.

- The distribution of various regions of operation of NMOS over the graph plotted between Ids and Vds.
- From the I-V charachteristic of an NMOS, when Vgs>=Vt, then we see two regions, one with linear increase of current when Vds<=Vgs-vt and
  one with saturated current when Vds>Vgs-Vt. 
- The plot overlapping with the 'x' axis is at Vgs=0V and that is because there is 0 drain current at that point of time and the reason is that when
  Vgs=0V the nmos is not turned 'ON' so, there is no channel present.
- cut-off region of NMOS.
        * When Vgs<Vt the region of operation of the NMOS is said to be the cut-off region
        * Cut-off region is a region where the device has been cut-off or it is 'OFF'

* Short channel effect
  
    When W/L is constant, drain current Id is constant at any node (At any Node means W and L increase or decrease) but practically this will not happen. When W and L (from long channel to short channel device) have decreased in value, we stop seeing quadratic dependance of Ids on Vgs after a certain Vgs value, and we see linear dependance, and also peak current decreases from long channel case due to velocity saturation effect.

* Velocity Saturation effect
  
  - For the lower values of electric field, the velocity tends to be a linear function of the electric field. But, after a certain point (cut-off) the
    velocity just saturates. This point of saturation is represented by εc (critical electric field)
  - Vn(m/S) = linear for ε<=εc
  - Vn(m/S) = constant for ε>=εc

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/81366930-3e43-47a5-acf3-4ac6ac4bfc0f)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/82ecb560-4840-4ee1-a130-72eb65dd18de)
 The snap shot of the graph of velocity saturation effect
εc = 2 Vsat / µn

- There is region of opertion for higher values of Vgs, called Velocity Saturation. 
- For long channel (L>250nm) has 3 modes of operation: cutoff, resistive, and saturation
- For lower nodes/channel (L<250nm), there are 4 regions of operations. Cut-off, Linear, Saturation and Valocity Saturation.
- Let's call (Vgs-Vt)=Vgt
- For both channel in cut-off mode, Id=0 for Vgs<Vt
- for all other modes, the equation of Id for long channel and short channel devices

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/f9a5da17-e8ff-40e7-8ce5-dad4b57c520b)

Vdsat is a technology parameter saturation voltage i.e voltage at which device velocity saturates and is independent of Vgs or Vds


The various modes when the value of Vmin is different

    - When Vgt is the minimum of Vgt, Vds, Vdsat, then Vds and Vdsat at huch higher volatage and  the device is in saturation region.
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/089571be-7777-447b-aa4e-7877f6a06132)

    - When Vds is the minimum of Vgt, Vds, Vdsat, then device is in resistive region.
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/59f4442d-bf9a-4f7a-add2-f7ad21b954e5)

    - When Vdsat is the minimum of Vgt, Vds, Vdsat the device is in velocity saturation region.
![Screenshot from 2024-03-06 15-29-48](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/8cb97131-d8f1-4b4a-8cdb-5044a65823e7)

    - It looks like current should increase at lower nodes.

- When move from higher device to lower, Velocity Saturation causes device to saturate early and as result of that peak current for same W/L is differenet in two differnet cases. 

#### CMOS VTC

- MOSFET as a Switch
     - CMOS VTC defines the delays of cell.
     - A CMOS acts like a switch. 
       o device is off (With infinite 'Off' resistance) and no current flows from source to drain when |Vgs|<|Vt|  
       o device is ON (with finite 'On' resistance) when |Vgs|>|Vt|
       
- Working of CMOS Inverter
      o  when Vin is ‘high’ and equal to ‘vdd’, PMOS turns 'OFF'and NMOS turns 'ON' and Vout is 0 (open switch).
      o  when Vin is ‘low’ and equal to ‘0V’, PMOS turns 'ON' and NMOS turns 'OFF' and Vout is Vdd (closed switch).
  - The flow of current when Vin is ‘high’ and when Vin is ‘low’
- When Vin=Vdd
    o Direct path exists between Vout and Vss resulting in Vout=0V
- When Vin=0V
    o Direct path exists between Vdd and Vout, resulting in Vout=Vdd
In either case, there is a resistance with the switch which represents the equivalent resistance of the nmos (Rn) and pmos (Rp) respectively as shown in the picture below.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/81422057-7b82-4f6a-ba66-e2da754a0227)

The snap shot of the circuit diagram of CMOS inverter

- By observation:
  
    * For the NMOS, voltage equations (Vss =0)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/7ef5daa7-0ed0-403a-a90d-284e5572a41b)

    * For the PMOS, voltage equations
    
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/bd366836-d29f-485d-913d-e32e07eb87ab)

    * For the relationship between the currents
    
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/27924e75-24e1-4886-a7dc-9266529a4128)

The VTC of a CMOS (Vout vs Vin) is derived by first plotting IdsN vs Vout for different values of VgsN = Vin (load curve for NMOS) as shown 
Load curve for PMOS transistor in CMOS inverter

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/046ae9b8-741f-4322-9466-cce9ecc6c598)

Similarly,  Load curve for NMOS transistor in CMOS inverter is graph of IdsP vs Vout for different VgsP as shown 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/25dd7dcd-fa05-42f3-9604-8cb417946ae2)

Finally, Superimposing the load curve of NMOS on the load curve of PMOS because Vout and Vin is common for both PMOS and NMOS. So graphically if we want to derive VTC of CMOS, it has to be intersection points between PMOS and NMOS. So, for intersection points between common Vin values gives us the common Vout value in the VTC. and plotting Vin vs Vout from the graph obtained. Graphically, the Vin points from the intersection of corresponding load lines are picked-up.
superimposed load curve of NMOS and load curve of PMOS as shown 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/45dceb14-46e1-490a-9b61-a334bc390b77)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/4a0bead9-6596-4d01-a6b1-2b95cca5c060)

 VTC has 5 regions: 1-) PMOS linear, NMOS off, 2-) PMOS linear, NMOS saturation, 3-) PMOS and NMOS in saturation, 4-) PMOS saturation, NMOS linear, and 5-) PMOS off, NMOS linear as shown in third picture (1, 3, and 5 regions are of importance).

##### Day 3: CMOS switching threshold and dynamic simulations
how to simulate a CMOS circuit using spice in order to obtain the VTC and evaluate the static behavior. Spice deck needed to write a netlist: component connectivity, component values, identify nodes and name them. The switching voltage Vm is that where Vin=Vout (nmos and pmos in saturation), and it defines the robustness of the CMOS.

    o Voltage transfer characteristics and SPICE simulations

        - The various components of a SPICE deck:

            * Component connectivity
            * Component values
            * Identification of 'nodes'
            * Naming 'nodes'


![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/34fe897a-7869-411a-84d6-7bf85b3a6a35)

The snap shot of the SPICE netlist considered

The used models of MOSFETs and netlists for simualtions are taken from <pre>https://github.com/kunalg123/sky130CircuitDesignWorkshop.git</pre>

The SPICE code for the above netlist looks something like following:
<pre>
***MODEL Description***
***NETLIST Description***
M1 out in vdd vdd pmos W=0.375u L=0.25u
M2 out in  0   0  nmos W=0.375u L=0.25u

cload out 0 10f

Vdd vdd 0 2.5
Vin  in 0 2.5

***SIMULATION Commands***
.op
.dc Vin 0 2.5 0.05

***.include tsmc_025um_model.mod***
.LIB "tsmc_025um_model.mod" CMOS_MODELS
.end</pre>


(Note terminal window screenshot pending))
###The snap shot of the terminal window for plotting the Vtc characteristics of CMOS inverter
Lab Activity:(Pending) 
For plotting the Vtc characteristics of CMOS inverter, the following code is needed:
<pre>*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op

.dc Vin 0 1.8 0.01

.control
run
setplot dc1
display
.endc

.end</pre>

Note: The snap shot of the terminal window for plotting the Vtc characteristics of CMOS inverter Pending 
Note : The snap shot of the output window for plotting the Vtc characteristics of CMOS inverter Pending 

  - To find the switching threshold voltage (Vm), it is known that Vout = Vin so zoom in on the plot where roughly Vout = Vin by
    selecting the area of the plot by right clicking on the screen and dragging it to select the area.
  - Zoom twice or thrice until the point where Vm lies becomes almost certain.
  - Left click roughly on the point on the curve where Vm should approximately lie.
  - Values of x0 and y0 will now appear on the terminal window.
  - Since we are finding Vm, therefore x0 ~ y0 and hence x0=y0=Vm.

For performing the transient analysis, the following code is required:
<pre>*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 PULSE(0V 1.8V 0 0.1ns 0.1ns 2ns 4ns)

*simulation commands

.tran 1n 10n

.control
run
.endc

.end</pre>

Note: The snap shot of the terminal window for performing the transient analysis is pending
Note :The snap shot of the output window for performing the transient analysis is pending 

    - To calculate the rise delay:
        * Zoom on the part of the curve having fall of the input pulse and rise of the output pulse around voltage of (Vdd/2) by right clicking
          on the screen and dragging it to select the area.
        * Now, left click on the rising edge of the output curve at (Vdd/2) to get a point x0,y0 on the terminal.
        * Similarly, get the point at (Vdd/2) for falling edge of the input curve.
        * The difference between the x-coordinate of the rising edge of the output curve and the falling edge of the input curve is the rise delay.
    - To calculate the falling delay:
        * Zoom on the part of the curve having rise of the input pulse and fall of the output pulse around voltage of (Vdd/2) by right clicking 
          on the screen and dragging it to select the area.
        * Now, left click on the falling edge of the output curve at (Vdd/2) to get a point x0,y0 on the terminal.
        * Similarly, get the point at (Vdd/2) for rising edge of the input curve.
        * The difference between the x-coordinate of the falling edge of the output curve and the rising edge of the input curve is the fall delay.


#### Static Behavior Evaluation - CMOS Inverter Robustness: Switching threshold

- CMOS inverter is a robust device because the shape of it's input versus output curve remains the same for all different values of (W/L) ratios.

- Static Behavior Evaluation: CMOS Inverter Robustness

    * Switching Threshold
    * Noise Margin
    * Power Supply Variation
    * Device Variation

- Switching Threshold (Vm)

    * It is the point where Vin = Vout

    * Graphical method to find Vm is to draw a line across the graph of output voltage to input voltage of a CMOS inverter starting at the origin
      and ending at the opposite diagonal of the plot (basically a line with a 45 degree inclination with the x-axis). Now, the x-coordinate of the            point of intersection of this line and the curve is the switching threshold.

    * Vm when (Wp/Lp) is 1.5 is approximately equal to 0.98V and when (Wp/Lp) is 3.75 it is approximately equal to 1.2V

    * Wp and Lp in the above section are Width of PMOS channel and Length of PMOS channel

    * At Vm, both PMOS and NMOS are turned 'ON' because Vgs almost crossed the threshold region for both of them.

    * A few observations can be made from the information stated above,

          1) Vgs = Vds

          2) IdsP = - IdsN which means that IdsP + IdsN = 0

    We know the equations for IdsN and IdsP which are as stated below:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/e431539d-eafe-4560-b983-fc33b2234858)

We ignore the 1+λVds because the term is very small and it makes the equations very difficult for hand calculations.

Since, IdsP + IdsN = 0

Therefore, the equations can be re-written as:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/d690c63d-dae5-4db9-b996-3ba143086752)

Let's consider this as equation 1

Solving the above equation for Vm,

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/0fb1bef2-8020-4990-ad21-4d982282bf55)


* Alternatively, the required ratio of PMOS versus NMOS transistor size can be derived such that Vm is set.

   Equation 1 must be taken in the form IdsN = - IdsP

Therefore,

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/d79c060c-3697-4698-b6e0-7e7389fe76a1)

Here,
    - Wp is the width of the channel in PMOS
    - Lp is the length of the channel in PMOS
    - Wn is the width of the channel in NMOS
    - Ln is the length of the channel in NMOS
    - kn' is the process transconductance of the NMOS
    - kp' is the process transconductance of the PMOS
    - Vdsatn is the Vdsat of the NMOS
    - Vdsatp is the Vdsat of the PMOS
    - Vm is the switching threshold voltage
    - Vt is the threshold voltage
    - Vdd is the supply voltage
    
To define a pulse, use the syntax as defined in the picture below:   

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/89073e28-1431-45f4-8712-81646a4b2381)

- We experimented with the sizes of the PMOS with respect to the sizes of NMOS and came up with the following conclusions

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/055f7258-ecc0-414a-8505-31beb34c421d)

    - We can make some conclusions from the above table:
        * When (Wp/Lp) = 2.(Wn/Ln), there is an approximately equal rise-fall delay
        * Due to the equal rise-fall delay, (Wp/Lp) = 2.(Wn/Ln) create typical characteristics for a clock inverter/buffer
        * The conditions other than (Wp/Lp) = 2.(Wn/Ln) can still be used as regular inverters/buffers and these can be preferred for data path
        * Switching Threshold for (Wp/Lp) = 2.(Wn/Ln) and (Wp/Lp) = 3.(Wn/Ln) is very small. Similarly, switching threshold for (Wp/Lp) = 4.(Wn/Ln) 
          and (Wp/Lp) = 5.(Wn/Ln) is also very small

    - When Wp/Lp is increased, the rise delay is significantly reduced because time required for the output capacitor to charge decreases significantly        and the reason is the availability of a bigger area to charge the capacitor.

    - Ron(PMOS) ~ 2.5*Ron(NMOS)

#### CMOS Noise Margin Robustness Evaluation

