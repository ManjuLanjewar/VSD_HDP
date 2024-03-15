<html>
<body>

<p><a href="#C1">Day 1</a></p>
<p><a href="#C2">Day 2</a></p>
<p><a href="#C3">Day 3</a></p>
<p><a href="#C4">Day 4</a></p>
<p><a href="#C5">Day 5</a></p>
<p><a href="#C6">Day 6</a></p>
<p><a href="#C7">Day 7</a></p>
<p><a href="#C8">Day 8</a></p>
<p><a href="#C9">Day 9</a></p>
<p><a href="#C10">Day 10</a></p>




<h2 id="C7">Day 7</h2>
<h2 id="C8">Day 8</h2>
<h2 id="C9">Day 9</h2>
<h2 id="C10">Day 10</h2>

</body>
</html>

<h2 id="C1">Day 1</h2>

<details>
<summary>Introduction to Circuit Design and SPICE simulations</summary>

**Circuit Design** 

All logic gates are made-up of PMOS and NMOS transistors connected in very particuar fashion and once they are connected in that fashion ,
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
   - When the Pinch-off phenomenon is started, the channel begins to disappea. Basically, the channel starts to disappear only from the Drain side acquiring a triangular shape.
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

</details> 


<h2 id="C2">Day 2</h2>

<details>
        
<summary>velocity saturation and the basics of CMOS inverter Voltage Transfer Characteristics (VTC)</summary>

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

</details>

<h2 id="C3">Day 3</h2>

<details>
    <summary>CMOS switching threshold and dynamic simulations</summary>

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

The effect of increasing the pmos width. When the pmos width is wider than that of nmos, the switching voltage of the VTC shifts to the right slightly (advantage). As width of pmos increases as an integer multiple of that of nmos (for same L), the rise delay and fall delay decreases rapidly (time to charge decreases as width is wider) and increases respectively. For one some sizing (factor of 2), we observe an equal rise and fall times (symmetric property which is a typical characteristic of a clock inverter/buffer where resistance of pmos is approximately equal to resistance of nmos in that case due to the W/L ratios). Other sizing for inverters is used to get regular inverter/buffer that would be preferred in the data path.


#### CMOS Noise Margin Robustness Evaluation

Noise margin, which is another characteristic that defines static behavior of the inverter (robustness).

##### Part 1: Static Behavior Evaluation - CMOS Inverter Robustness: Noise Margin

The ideal and actual Input-Output characteristics of an inverter were observed

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/2f262800-a322-4f6f-9875-478ce101b647)

    - In the above diagram, the terms stated are explained as follows:

        o ViL is Input Low Voltage (ViL could be Vdd/4)
           -- Any input voltage level between 0 and ViL will be treated as logic '0'
        o Voh is Output High Voltage (ViH < VoH <= Vdd)
          --  Any output voltage level between VoH and Vdd will be treated as logic '1'
        o ViH is Input High Voltage (ViH could be 3.Vdd/4)
          --  Any input voltage level between ViH and Vdd will be treated as logic '1'
        o VoL is Output Low Voltage (0 <= VoL < ViL)
          -- Any output voltage level between 0 and VoL will be treated as logic '0'

- Actual Input-Output characteristics on an inverter were observed and they were plotted on a scale
  
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/52c8484e-32a9-4074-9bb3-a4405a8b2899)

- In the above diagram, the terms stated are explained as follows:

    * NMh is the Noise Margin High
       - Any voltage level in "NMh" range will be detected as logic '1'
    * NMl is the Noise Margin Low
       - Any voltage level in "NMl" range will be detected as logic '0'
    * Undefined region
       - Any signal in "Undefined region" will be an indefinite logic level

- Noise Margins are the tolerance levels of the noise
- The equations for NMh and NMl are as follows:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/96ca3a44-de57-4b19-8a1f-cf3bf811dc4a)

* Now with the voltage levels plotted in the noise margin scale, we have prepared a chart that will give the summary of the noise margin:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/e05ef4d8-5acb-4feb-9b67-65453f81eb5f)

The snap shot of the Noise induced bump characteristics at different noise margin levels

    - For any signal to be considered as logic '0' and logic '1', it should be in the NMl and NMh ranges, respectively.
    - If the height of the bump lies in between Vol and Vil then it's not hazardous because it still lies in the range of logic '0'. Any glitch that           occurs in this region is a safe glitch because it will still be considered as logic '0'.
    - If the height of the bump lies in the "undefined region" then it is potentially hazardous because it can acquire logic '1' which can be fatal. 
      Any glitch in this region is unsafe because it is unclear if it will go to logic '1' or fall to logic '0'. 
    - If the height of the bump lies in between Vih and Voh then it will definitely be considered as logic '1'. These kinds of glitches are the glitches       that need to be fixed.
    - The noise margins of the inverter at different values of Wp/Lp were observed and they were as follows:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/ee7cf26c-bc71-4882-bd73-33f1bfbe61c2)

A few conclusions can be inferred from the above table: 
    - When (Wp/Lp) = 2.(Wn/Ln) there is a rise at the NMh because PMOS is responsible for holding the charges on the capacitance. When the size of PMOS is increased, a low-resistance path from supply to the capacitance is formed and as a result of that, the capacitance is able to retain the charge for a longer amount of time resulting in an increased NMh. 
    - When (Wp/Lp) = 4.(Wn/Ln) there is a drop at the NMl because the NMOS has now become weaker than the PMOS - When (Wp/Lp) = 5.(Wn/Ln) the NMh almost comes to a static point.
    - In the above table, NMl is not affected much but NMh has increased by 120mV but this range is still acceptable and this proves the CMOS inverter robustness with respect to the Noise Margin.
    
Finally, the areas that can be used for digital and analog applications are stated in the figure below:

Noise margin, which is another characteristic that defines static behavior of the inverter (robustness). 
When Vin<=VIL (logic 0), Vout is expected to ber VOH, and when Vin>=VIH (logic 1), vout is expected to be VOL (note that the slope at VIL and VIH is -1). 
The noise margin is defined as VIH-VIL (undefined region: voltage ranges at which the logic does not differentiate between 0 and 1).
Noise margin high (interpereted as logic 1) = VOH-VIH and noise margin low (interpreted as logic 0) = VIL-VOL. 
Ideally, we want a CMOS inverter to have a noise margin of 0. When the width of the pmos increases with respect to nmos width, noise margin high increases while noise margin low stays the same then drops as the pmos is responsible for the high value output. 
Digital design relies on the areas of noise margin high and noise margin low.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/9c3a5d1e-ee7f-4d3b-b71b-6ed9b38b0dc5)

The snap shot of the Vout versus Vin curve showing the areas that can be used for digital and analog applications

Note: Lab Activity pending 

<pre>*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=1 l=0.15
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

.end
</pre>

Method to calculate the Noise Margins from the plot:

    - Run the ngspice command and open the plot
    - left click on the point towards the top of the graph where the curvature seems to be '-1'
    - In this case it was x0 = 0.766667, y0 = 1.71351
    - Now, left click on the point towards the bottom of the graph where the curvature seems to be '-1'
    - In this case it was x0 = 0.977333, y0 = 0.110811. Let's consider these points as x1 and y1 thus making the coordinates x1 = 0.977333, y1 = 0.110811
    - For noise margin high we need Voh-Vih and in this case VoH=y0 and ViH=x1
    - For noise margin low we need Vil-Vol and in this case ViL=x0 and VoL=y1
    - Therefore, we get NMh = 0.736177 and NMl = 0.655856
    
</details>

<h2 id="C4">Day 4</h2>

<details>
    <summary>CMOS Power supply and device variation robustness evaluation</summary>    
 
 power supply scaling and device variation, where the effect of those on the CMOS is another characteristic that defines static behavior of the inverter (robustness).
 
##### Part 1: Static Behavior Evaluation - CMOS Inverter Robustness: Power Supply Variation


    - Whenever we move from 250nm nodes to lower nodes like 20nm or so on, we scale our supply voltage as well. For example, if things were working at 1V sometime back, now they will be operating at 0.7V

    - A CMOS inverter can be operated at 0.5V as well and it has it's own advantages and disadvantages:
        * Advantages of using 0.5V supply:
            1) There is a significant increase in gain (close to 50% improvement)
            2) There is a significant reduction in energy consumption (close to 90% improvement)
        * Disadvantages of using 0.5V supply:
            1) Performance impact (0.5V supply rising and falling edge is insufficient to completely charge or discharge the load capacitance)

Note:  Lab activity is pending
To perform the lab activity for power supply scaling, we need the following code:

<pre>*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=1 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

.control

let powersupply = 1.8
alter Vdd = powersupply
        let voltagesupplyvariation = 0
        dowhile voltagesupplyvariation < 6
        dc Vin 0 1.8 0.01
        let powersupply = powersupply - 0.2
        alter Vdd = powersupply
        let voltagesupplyvariation = voltagesupplyvariation + 1
      end

plot dc1.out vs in dc2.out vs in dc3.out vs in dc4.out vs in dc5.out vs in dc6.out vs in xlabel "input voltage(V)" ylabel "output voltage(V)" title "Inveter dc characteristics as a function of supply voltage"

.endc

.end
</pre>

To define a loop in order to scale the power supply, use the syntax as defined in the picture below:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/8082a119-38c4-4fb6-addd-c21e73f19b2e)

Note : The snap shot of the terminal window to observe the power supply variation is pending 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/70452432-db4b-43ec-9184-51244c568239)

The snap shot of the output window to observe the power supply variation

    - To calculate the gain for the given plot:
        1) Select the curve for which the gain is to be calculated (In this case, we chose the plot for 1.8V Vdd)
        2) Left click on the point where the slope of the curve is almost changing toward the top of the plot
        3) The point obtained was x0 = 0.766667, y0 = 1.71351
        4) Now, left click on the point where the slope of the curve is almost changing toward the bottom of the plot
        5) The point obtained was x0 = 0.982667, y0 = 0.1 but for our convenience let us consider the coordinates of the point to be x1, y1
        6) Therefore, the point becomes x1 = 0.982667, y1 = 0.1
        7) Subtract y1 from y0. So, y0 - y1 = 1.61351
        8) Subtract x1 from x0. So, x0 - x1 = -0.216
        9) Now, gain = (y0-y1)/(x0-x1)
        Hence, Gain(g) = |(1.61351)/(-0.216)| = |-7.46995| = 7.46995

##### Part 2: Static Behavior Evaluation - CMOS Inverter Robustness: Device Variation

    1) There are two sources for device variation:
        - Etching Process Variation
        - Oxide Thickness

    * Etching Process Variation:
        - The etching process will define the structures in the layout of the CMOS inverter.
        - Etching is a very important fabrication step
        - It is the process that defines the structure (width and the height)
        - Based on the structures that get defined by the process, it directly impacts the delay

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/c563df91-8a7d-4771-a7a2-361d115951a6)

   2) In layout of the CMOS inverter we have:
        - P-diffusion region which is indicated by green color.
        - Poly-silicon area which is indicated by red color.
        - Metal layer which is indicated by blue color.
        - N-diffusion region indicated by yellow color.
        - Contacts between two layers indicated by black crosses.

   3) Thickness of poly-silicon layer is the gate length annd it defiens at which node we are (20nm, 30nm, 45nm, etc.).

   4) Thickness of the P-diffusion layer is the width of the gate of the PMOS and the thickness of the N-diffusion layer is the width of the
      gate of the NMOS.

   5) Width identifies overlap area between the diffusion layer and the poly-silicon layer.

   6) Fabrication is basically a lab where we have a lot of things like chemicals, water, gases, etc. running and due to these the ideal
      structure is distorted.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/7559be61-2ae7-4243-887b-6b7c7b6534ed)

Above is snap shot of the inverter chain

    1) Inverter Chain:
        - When inverters are connected back-to-back they are collectively called as "Inverter Chain".
        - In an inverter chain, the gates in the middle have same structures on both sides. So, it's very likely that this particular gate structure               will have a repeated distortion because they are exposed to same kind of structures.
        - In an inverter chain, gates in the middle will have a structure which is different from the gates at the ends because they might be connected            to different devices that will impact the gates.
        - Variation in L and W takes place because of non-ideal mask, which in turn impacts the drain current. 
        
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/06406461-7d6d-41c5-83a3-3a46a157902f)

    2) Oxide Thickness:
        - In an ideal oxidation process, the gate oxide thickness will be constant throughout the process.
        - In real oxidation process, the gate oxide thickness will not be constant along the gate length.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/3517788b-8d33-4d7f-a3da-45806dfd098e)

        - In an inverter chain, the gate oxide thickness can vary for each transistor.
        - Oxide thickness directly affects the Id equation because Cox is dependant on it.

    3) Strong PMOS:
        - PMOS with less resistance (possibly least resistance if the size chosen is the greatest size possible)
        - PMOS is wider in size (possibly widest PMOS available)

    4) Weak NMOS:
        - NMOS with high resistance (possibly highest resistance if the size chosen is the least size possible)
        - NMOS is small in size (possibly smallest NMOS available)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/424a4bac-6a0c-4ae1-bcfb-be09843ea3e4)

    5) Strong NMOS:
        - NMOS with less resistance (possibly least resistance if the size chosen is the greatest size possible)
        - NMOS is wider in size (possibly widest NMOS available)

    6) Weak PMOS:
        - PMOS with high resistance (possibly highest resistance if the size chosen is the least size possible)
        - PMOS is small in size (possibly smallest PMOS available)

** We can plot the variation if we move from Weak PMOS - Strong NMOS to Strong PMOS - Weak NMOS using SPICE simulation and the plot is given below:
    
    From the plot given above, we can make the following conclusions:
    
       - With the variation from Weak PMOS - Strong NMOS to Strong PMOS - Weak NMOS, the switching threshold varies from roughly 0.7V to 1.4V which is 
         fairly acceptable because behavior of the inverter is intact

  ![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/57b73d09-acb9-4779-99f2-77b848dbbaae)

      - Variation in Noise Margin high (NMh) is roughly from 2.5V to 2.1V which is a variation of 400mV which is good enough to filter
        out high voltage variations
      - Variation in Noise Margin low (NMl) is roughly from 0V to 0.3V which is a variation of 300mV which is good enough to filter out 
        low voltage variations

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/6037a72a-5fc7-4c32-8422-07d7bef31661)
 
      - Overall, variation in the Noise margins is low and this leaves the operation of the gate intact.

Note : Lab Activity: is pending 

- Since the pfet width is very huge as compared to the nfet width, the plot is shifted towards right
    * To find the value of the switching threshold:
        1) Zoom in on the plot where Vin ~ Vout by right clicking and dragging the cursor to select the area
        2) Zoom until the value of switching threshold becomes almost certain
        3) Left click on the point where Vin is roughly equal to Vout
        4) A point x0 = 0.988209, y0 = 0.988191 is obtained
        5) Since x0 ~ y0. Therefore, Switching Threshold Voltage = Vm = x0 = y0 = 0.988V

</details>

<h2 id="C5">Day 5</h2>

<details>
<summary>Introduction to Chip, Pads, Core, Die and Ip's</summary>

Consider a chip on an arduino board, it would contain the following components:-

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/652cf522-e255-4353-9b56-ee3e70ec00c9)! 

* It has several protocols, an external memory unit (SDRAM), GPIOS, PWM etc.
* Now all (except memory external chip) of these are contained in a package as shown below.
* It represents a 7x7 [dimensions] QFN-48 [Quad Flat No leads; 48 pins].
* The chip is connected to the package with the help of wire bonds

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/31c1a3b0-d101-44a5-9d9d-1f6b276f3c73)![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/da14e8a6-27e3-4ca3-8ea7-9ca990ae493e)!

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/d702cf45-5f1f-468c-bea7-df340f4fad4e)

- Chip is at the center of a package. 
- chip has PADs which allow signals to pass in and out of the chip (from core where the digital logic sits to outside or vice versa).
- The die defines the size of the chip, which is manufactured on silicon wafers.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/a58cb1c2-4f38-4a00-9055-31c1d4dc4cfd)

- A typical core consists of a CPU SoC, ADCs/DACs, SPI, PLL, and SRAM. PLL, SRAM, and DAC/ADC are called as foundary IPs.
- The core region contains Macros and Foundry IPs.
- Foundary is a big factory that has machines where chips get manufactured.
- We need an interface (some files) to communicate with the foundary.
- IP is intellectual property (needs intelligence to be built blocks of core).
- SPI and CPU SoC are macros. Macros are pure digital logic.

**Introduction To RISC-V**
- RISC-V is a new ISA that's available under open, free and non-restrictive licences. RISC-V ISA delivers a new level of free, extensible software and hardware freedom on architecture.
- It is far simpler and smaller than other commercial ISAs available.
- It avoids micro-architecture or technology dependent features.
- It has small standard base ISA and multiple standard extensions.
- It supports variable-length instruction encoding. 

**From Software Application to Hardware** 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/fe55f1d8-006f-45e0-9476-7c0f52b560cf)

- The above image represents the Software to Hardware translation. 
- The application software or apps are handled by the system software in order to run on the hardware. 
- System software consists of the OS, Compiler and the assembler.
- An OS performs low level system functions, handles IO operations, allocates memory.
- It starts at the software application level which takes in an input. This input is now processed by the Operating System (OS).
- It instigates the Compiler to convert high level abstract code of the software to Assembly/Low level machine instructions (ISA) according to hardware.
- The assembler then converts the instructions (abstract ISA, or 'architecture' of computer) to respective binary that is eventually fed to the hardware.
- Hardware understands patterns and accordingly generates output. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/664ddca0-242e-449e-8fb1-f3d6a177bf6c)

- Instructions acts as Abstract Interface between C/C++/JAVA language and hardware.
- Abstarct Interface is called The Instruction Set Architecture (ISA) which refers to the 'architecture' of the computer/processor. 
For example, if the ISA used is of RISC-V, the code converted by the compiler should give instructions suitable for RISC-V core.
Hence, one can say that ISA basically represents the Hardware at an intermediate stage.
- There is one more interface betwwen Instruction and Hardware is HDL ( Hardware description Language)
  
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/d61da171-b278-4269-ab18-14df4b1d34f2)

- The Assembler converts the instructions into a bitstream that is fed to the Hardware. 
- To obtain the hardware or final layout, a certain number of steps need to be followed.
- The RTL implements the instructions (the ISA), then RTL is synthesized into netlist which is physically implemented in hardware.
 
**Components of opensource digital ASIC design**

The design of digital Application Specific Integrated Circuit (ASIC) requires three enablers or elements
- Resistor Transistor Logic of Intellectual Property (RTL IPs),
- Electronic Design Automation (EDA) Tools and
- Process Design Kit (PDK) data.
  
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/46712f8c-221f-4d89-b791-d372e03e8837)

  * Opensource RTL Designs: github, librecores, opencores
  * Opensource EDA tools: QFlow, OpenROAD, OpenLANE
  * Opensource PDK data: Google Skywater130 PDK

**What is PDK?**

- A PDK (Process Design Kit) is the iterface between the fabrication and design (which were separated in the past). 
- It contains a collection of files used to model a fabrication process for the EDA tools used to design an IC.
- PDK includes device models, process design rules(DRC, LVS, PEX), digital standard cell libraries, I/O libraries, etc.. 
- Regular PDKs are distributed under NDAs (non disclosure agreements), but open PDKs (130nm, released by Google) do not require NDAs.

ASIC flow objective: RTL to GDSII also called Automated PnR and /or physical implementation 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/643ddf49-1959-45ef-86c8-d4c14248dd45)

Simplified RTL to GDSII Flow

- Synthesis (takes RTL as input, output is gate-level netlist. Standard cells have regular layouts)
    converts RTL to a circuit out of componnets from the Standard Cell Library(SCL).
    Resultant circuit is described in HDL and referred as Gate Level Netlist.
    Standard cells have regular layouts
-  Floor & Power Planning: Planning of silicon area to ensure robust power distribution
      Objective: Plan silicon are and create robust power distribution network to power circuit.  
      Chip Floor Planning : Partition the chip die between different system building blocks and place I/O Pads.
      Macro Floor Planning: Dimensions, Pin locations, rows defination
      Power planning : power network constructed typically chip is powered by multiple VDD and GND pins.
      power pins are connected to all componets through rings and  vertical and horizontal metal straps
- Placement: Placing cells on floorplan rows aligned with sites
    Usually done in 2 steps: Global and detailed placement.
    Global Placement: for optimal position of cells
    Detailed Placement: for legal positions
- CTS (creating clock distribution network to route the clock)
- Route (implementing the interconnect using metal layers)
  Global and detailed routing takes place in divide and conquer approach
- Sign off: Physical verifications (DRC, LVS) and Timing verifications (STA)
  Output is GDSII

The PDK is used in all these steps.
Developing an open ASIC design flow is tough as there are worries in tool qualification, tool calibration, and missing tools.

**OpenLANE ASIC Flow**

OpenLane is an open ASIC design flow (relies on multiple open-source tools).
The main goal is produce a clean GDSII without human intervention. Clean means no LVS, DRC, STA violations. 
OpenLane is tuned for skywater 130 open PDK. OpenLane can be used to produce GDSII for either macros and chips. 
It has two modes of operation: autonomous (one click of button) or manual (step by step). 
It provides a mean to sweep configurations allowing design space exploration, and has a large number of design examples available publicly.

Below is the detailed ASIC design flow in OpenLane.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/99807f46-78de-42bf-8b48-c9d937e07626)

OpenLANE is an opensource tool or flow used for opensource tape-outs. The OpenLANE flow comprises a variety of tools such as Yosys, ABC, OpenSTA, Fault, OpenROAD app, Netgen and Magic which are used to harden chips and macros, i.e. generate final GDSII from the design RTL. The primary goal of OpenLANE is to produce clean GDSII with no human intervention. OpenLANE has been tuned to function for the Google-Skywater130 Opensource Process Design Kit.
From conception to product, the ASIC design flow is an iterative process that is not static for every design. The details of the flow may change depending on ECO’s, IP requirements, DFT insertion, and SDC constraints, however the base concepts still remain. The flow can be broken down into 11 steps:

1) Architectural Design – A system engineer will provide the VLSI engineer with specifications for the system that are determined through physical constraints. The VLSI engineer will be required to design a circuit that meets these constraints at a microarchitecture modeling level.

2) RTL Design/Behavioral Modeling – RTL design and behavioral modeling are performed with a hardware description language (HDL). EDA tools will use the HDL to perform mapping of higher-level components to the transistor level needed for physical implementation. HDL modeling is normally performed using either Verilog or VHDL. One of two design methods may be employed while creating the HDL of a microarchitecture:
   
    a. RTL Design – Stands for Register Transfer Level. It provides an abstraction of the digital circuit using:

* i. Combinational logic
* ii. Registers
* iii. Modules (IP’s or Soft Macros)

    b. Behavioral Modeling – Allows the microarchitecture modeling to be performed with behavior-based modeling in HDL. This method bridges the gap between C and HDL allowing HDL design to be performed
  
3) RTL Verification - Behavioral verification of design
4) DFT Insertion - Design-for-Test Circuit Insertion
5) Logic Synthesis – Logic synthesis uses the RTL netlist to perform HDL technology mapping.
   The synthesis process is normally performed in two major steps:
    o GTECH Mapping – Consists of mapping the HDL netlist to generic gates what are used to perform logical optimization based on AIGERs and
      other topologies created from the generic mapped netlist.
    o Technology Mapping – Consists of mapping the post-optimized GTECH netlist to standard cells described in the PDK

6) Sandard Cells – Standard cells are fixed height and a multiple of unit size width. This width is an integer multiple of the SITE size or the PR boundary. Each standard cell comes with SPICE, HDL, liberty, layout (detailed and abstract) files used by different tools at different stages in the RTL2GDS flow.

7) Post-Synthesis STA Analysis: Performs setup analysis on different path groups.

8) Floorplanning – Goal is to plan the silicon area and create a robust power distribution network (PDN) to power each of the individual components of the synthesized netlist. In addition, macro placement and blockages must be defined before placement occurs to ensure a legalized GDS file. In power planning we create the ring which is connected to the pads which brings power around the edges of the chip. We also include power straps to bring power to the middle of the chip using higher metal layers which reduces IR drop and electro-migration problem.
Initial Layout of the Design.
   - Chip Partitioning --> divide the design into smaller blocks while maintaining functionality.
   - Macro Partitioning --> dividing and placing macros, rows and pins.
   - Power planning --> setting the VDD and GND layers. The top layers are used as they are wide and offer less resistance.
the above steps involve Partitioning, Floor planning and Power planning.

9) Placement – Place the standard cells on the floorplane rows, aligned with sites defined in the technology lef file.
   Placement is done in two steps: Global and Detailed.
   In Global placement tries to find optimal position for all cells but they may be overlapping and not aligned to rows,
   In Detailed placement takes the global placement and legalizes all of the placements trying to adhere to what the global placement wants.
   finalised layout of the modules, macros, pins and pads.

11) CTS – Clock tree synteshsis is used to create the clock distribution network that is used to deliver the clock to all sequential elements.
    The main goal is to create a network with minimal skew across the chip. H-trees are a common network topology that is used to achieve this goal.        * CTS alters the netlist. Functionality check is required before progressing
    * Logical Equivalence Check (LEC) --> formally confirm that the function did not change after modifying netlist
it is imperative to check functionality when the netlist is modified.

Note that DFT (design for testing) step is optional and facilitated by Fault tool. Note that we need to deal with antenna rules violations: when a metal wire segment is fabricated, it can act as an antenna which leads to damage some transistor gates during fabrication => two solutions: bridging and inserting antenna diodes. The two solutions are shown side-to-side below:

Note: Fake antenna diode insertion --> Antenna violations may occur which cause damage to the transistors as reactive charges begin to accumulate (usually taken care by Routing). There are two methods to approach this issue.

   ![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/8a67d7e8-5b0d-4252-814b-afdfda55a4d7)

OpenLane adds fake antenna cells to all gates after placement --> if ant violation is detected it will replace the fake cell with a real one.
OpenLane deals with those antenna violations and gives the user option to user either OpenLane or OpenRoad solution. The pdk directory inside the OpenLane directory has skywater-pdk which contains PDK files provided by foundry, open_pdks that contains scripts to setup pdks for opensource tools, and sky130A which contains sky130 PDK files.

13) Routing –
    * Implements the interconnect system between standard cells using the remaining available metal layers after CTS and PDN generation.
    * The routing is performed on routing grids to ensure minimal DRC errors.
    * The skywater pdk contains all the data ( location, size, thickness, pitch, vias ..etc) about the interconnect/metal layers.
    * Metal tracks form a routing grid.
      - Global Routing --> coarse grained grids used to generate routing guides
      - Detailed Routing --> fine grained grids and routing guides to implement actual wiring.
    * Physical Verification --> DRC and LVS.
    * Timing Verification --> STA

skywater130 pdk --> (1) lowest layer/local interconnect layer (Titanium Nitride) + 5 layers above (Aluminium) = (6)
Note: OpenLANE --> produce clean (no DRC, LVS, timing violations) GDSII with no human intervention.

Opensource EDA tools OpenLANE utilises a variety of opensource tools in the execution of the ASIC flow:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/659653ee-5b0e-451b-8729-b592b5aa1167)

14) DFT (Design for Testing)

    - Scan insertion
    - Automatic Test Pattern Generation (ATPG)
    - Test Patterns Compaction
    - Fault Coverage
    - Fault Simulation
      
      ![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/eae792db-4bf0-48da-90f9-a1fab803c839)

15) Physical Implementation (Automatic PNR) --> OpenRoad

    - Floor/Power planning
    - End Decoupling capacitors and tap cell insertion
    - Placement
    - Post Placement Optimization
    - CTS
    - Routing

OpenLANE design stages

    1. Synthesis
        o yosys - Performs RTL synthesis
        o abc - Performs technology mapping
        o OpenSTA - Performs static timing analysis on the resulting netlist to generate timing reports
    2. Floorplan and PDN
        o init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
        o ioplacer - Places the macro input and output ports
        o pdn - Generates the power distribution network
        o tapcell - Inserts welltap and decap cells in the floorplan
    3. Placement
        o RePLace - Performs global placement
        o Resizer - Performs optional optimizations on the design
        o OpenDP - Perfroms detailed placement to legalize the globally placed components
    4. CTS
        o TritonCTS - Synthesizes the clock distribution network (the clock tree)
    5. Routing
        o FastRoute - Performs global routing to generate a guide file for the detailed router
        o CU-GR - Another option for performing global routing.
        o TritonRoute - Performs detailed routing
        o SPEF-Extractor - Performs SPEF extraction
    6. GDSII Generation
        o Magic - Streams out the final GDSII layout file from the routed def
        o Klayout - Streams out the final GDSII layout file from the routed def as a back-up
    7. Checks
        o Magic - Performs DRC Checks & Antenna Checks
        o Klayout - Performs DRC Checks
        o Netgen - Performs LVS Checks
        o CVC - Performs Circuit Validity Checks
        
OpenLANE Files: 
The openLANE file structure looks something like this:

    * skywater-pdk: contains PDK files provided by foundry
    * open_pdks: contains scripts to setup pdks for opensource tools
    * sky130A: contains sky130 pdk files
    * Invoking OpenLANE and Design Preparation
    * Openlane can be invoked using docker command followed by opening an interactive session.
      flow.tcl is a script that specifies details for openLANE flow.

### Opensource EDA Tools used for physical Design

#### Python Installation

<pre>$ sudo apt install -y build-essential python3 python3-venv python3-pip</pre>

#### Docker Installation

<pre>$ sudo apt-get remove docker docker-engine docker.io containerd runc (removes older version of docker if installed)

$ sudo apt-get update

$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    
$ sudo mkdir -p /etc/apt/keyrings

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
$ sudo apt-get update

$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

$ apt-cache madison docker-ce (copy the version string you want to install)

$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io docker-compose-plugin (paste the version string copies in place of <VERSION_STRING>)

$ sudo docker run hello-world (If the docker is successfully installed u will get a success message here)</pre>
    
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/5a770edf-71a2-4d5f-ad70-7bdec390a873)

#### Opensource EDA Tools 

**OpenLane Directory Structure**

Openlane is automated RTL to GDSII flow that consists of multiple tools (obviously opensource) such as OpenROAD, Yosys, Magic, Netgen, and a number of custom scripts for design exploration and optimization. 
It has two modes to promote "No human in flow", that is, autonomous and interactive. For understanding the process of the flow, I will be using the "interactive" method.

All the Process Design Kit(PDK) are listed under the pdks/ directory.  Along with the Sky130A we are using some other open-source PDKs and other related files are also available in the directory. skywater-pdk has pdk related files means tech libs, cell lib etc. open_pdk any of silicon foundary files are compatible with commercial EDA tool and not for opensource tools. openpdk plans to mitigate that issue and they are set of scripts, files  converts foundary level pdks to be compatible with opensource EDA tools like Magic,Netgen etc.. The location of the PDK directory is given of $PDK_ROOT variable.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/288c6fe6-6af3-4c47-b9bb-aedf7edbde05)

sky130A is a pdk variant is made compatible to work with opensource enviornment. Under the variant, we have libs.tech and libs.ref 
sky130 is process name sky130nm, fd abbreviate foundary name, sc stands for standard cell library file and hd stands for high density is variant of pdk. osu is okloma state university. 
Openlane is compatible with pdks namely skywater130 and osu.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/a800e527-96b8-425f-94ec-dd5f1d092142)

libs.tech--> contains the library files related to the tools used in the flow 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/b5e066c4-867e-46e1-b8c3-43cbe78562ff) 

libs.ref--> contains process specific files timimg, cell lib.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/e0135089-9463-4636-b29f-2882cdc77b9f)

I will be using sky130_fd_sc_hd for my design. all technology files like  teclef files contains layer information, lib file contains all process corner information.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/a5762896-ea00-4e9a-80f4-0cccb7add0da)

Look into the different types of file types which are used to build a pdk.
- verilog --> netlists
- techlef --> metal layer data and design rules (technology files)
- spice --> circuit netlists of analog devices
- maglef --> used for displaying metal layers in the layout tool
- mag --> used for displaying layout on the layout tool
- lib --> contains the flavours of library files for different process corners. In short logical libraries.
- lef --> contains physical info such as shape, size, direction, and symmetry, input and output pins direction for each cellin the design.
- gds --> (GDSII) used to store IC layout information.
- cdl --> similar to spice netlists; stores electronic circuit information.

**Design Preparation Steps**

To start with OpenLane: 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/19fbaf48-36ed-4e66-84e1-9db77df097a5)

* OpenLANE Initialization
    For invoking OpenLANE in Linux Ubuntu, we should first run the docker everytime we use OpenLANE. 
    A custom shell script or commands can be generated to make the task simpler.
    - To invoke OpenLANE run the ./flow.tcl script.(as the name flow.tcl means using the script the flow has to go)
    - OpenLANE supports two modes of operation: interactive and autonomous(note that without interactive switch, OpenLane will run in automatic mode)
    - To use interactive mode use -interactive flag with ./flow.tcl (Interactive means step by steps)
  
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/809325d2-12e0-46b0-8773-a514332b64be)

Now prompt change to %
1. The first step after invoking OpenLANE is to import the openlane package of required version. This is done using following command. Here 0.9 is the required version of OpenLANE.
<pre>% package require openlane 0.9</pre>
All designs run in OpenLane are extract from "designs" folder.
<pre>vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane$ cd designs/</pre>
Here we are using picorv32a. It contains following files
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/2aaf2103-8021-4e26-adaa-af3666e9d13a)
- src file stands for source file which contain verilog file for RTL present as well as .sdc information
- pdk specific configuration file.
- config.tcl that has configurations for the design that will overwrite the default OpenLane settings. 
Note: For a custom design. You will need to create a config.tcl. The sky130_fd_sc_hd_config.tcl is not compulsory as it will not affect flow.
How OpenLane takes value? first it takes default values set in OpenLane. Then config.tcl and then sky130A_sky130_fd_sc_hd_config.tcl
Config.tcl overwrites default parameters.
sky130A_sky130_fd_sc_hd_config.tcl has higher priority which overwrites values in config.tcl.
So the question that arises is what is in the config.tcl file?
<pre>
# Design
set ::env(DESIGN_NAME) "picorv32a"

set ::env(VERILOG_FILES) "./designs/picorv32a/src/picorv32a.v"
set ::env(SDC_FILE) "./designs/picorv32a/src/picorv32a.sdc"

set ::env(CLOCK_PERIOD) "5.000"
set ::env(CLOCK_PORT) "clk"

set ::env(CLOCK_NET) $::env(CLOCK_PORT)

set filename $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/$::env(PDK)_$::env(STD_CELL_LIBRARY)_config.tcl
if { [file exists $filename] == 1} {
        source $filename
}
config.tcl (END)
</pre>
Config.tcl is used to set the files and parameters in the flow environment. As shown in the snippet above.

2. Design setup stage: The next step is to prepare our design for the OpenLANE flow. Means need to setup file system specific to flow like each and every step of flow will be fetching files property to location that location need to be created. That is design setup done using following command:

  <pre>% prep -design design-name</pre>

Some additional flags that can be used while preparation are:
  
    * -tag <name-for-current-run>
    * All the files generated during the flow will be stored in a directory named <name-for-current-run>
    * -overwrite - If a directory name mentioned in -tag already exists, it will be overwritten.
    
<pre>% prep -design picorv32a</pre> 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/a6bc3395-a5e8-4ad4-b548-9e85c5b3467e)

During the design preparation the technology LEF and cell LEF files are merged together to obtain a merged.lef file. The LEF file contains information like the layer information, set of design rules, information about each standard cell which is required for place and route.
Also, a "runs" directory is created inside the picorv32a directory, and inside it a directory with the current date is created. Inside that directory, all folder structures required by OpenLanes are present empty, except for temp folder. temp folder has the merged LEF files. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/47f2adcf-2ac0-408d-85b9-20387cc92b3a)

**Design Synthesis and Results**
To run the synthesis of the picorv32a design, I used the following command (During this step yosys and ABC tools are utilized to convert RTL design to the gate level netlist, which will be found in the folder runs/<RUN_today_date>/results/synthesis):

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/c5b2754e-40f1-4c54-861d-972a87b3262e)

% run_synthesis

The obtained logs and reports are found in runs/<RUN_today_date>/logs/synthesis and runs/<RUN_today_date>/reports/synthesis respectively.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/022bc8cf-8009-4b41-b939-4e4c0bed43f6)

Below are screenshots of the logs I obtained for STA results:
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/89480869-511e-4df2-94a0-ab7442eef8b2)

To calculate the flop ratio, I used the following formula, and the numbers are extracted from the report whose screenshot is included below:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/4621a3db-1b8b-4f3c-81c9-32879c976494)

<pre>Flop ratio = Number of D Flipflops / Total Number of cells
dfxtp_2 = 1613,
Number of cells = 14876,
Flop ratio = 1613/14876 = 0.1084 = 10.84%
Chip area for module '\picorv32a': 147712.918400</pre>

</details>

<h2 id="C6">Day 6</h2>

##### Good Floor Plan Vs Bad Floor Plan and Introduction to Library Cells 

<details>
<summary>Chip floor planning, Placement and Routing</summary>

**Utilization factor and Aspect ratio**

- In physical design flow, first step of floor planning is defining height and width of the core and die. 
- Recall that logic cells are placed inside the core. 
- Lets consider a basic example of a basic netlist consist of combo logic between capture and launch flops. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/8bb9173f-e2b9-4495-94aa-7a0fdd0cb089)

- Now to produce the components of the netlist (cell and flops) , it needs to be structured on the silicon wafer die. 
  Hence I would need to place these components of the netlist in certain way such that it fits in the core to be placed on the die.
- Here we are intrested in dimension of core and die. So in that case intrested in dimension of std. cells and not wires.
- Each cell and each flop will have dimensions. In this case lets take unit dimensions. 
- Let's dimension of std. cells are 1 unit X 1 unit. So area = 1 sq. unit
  Let's dimension of F/F's are 1 unit X 1 unit. So area = 1 sq. unit
  Let's calculate area occupied by netlist on silicon wafer.
  Now remove wires and place all on single plate. Now length will be 2 unit and breadth will be 2 unit. So, area will be 4 sq.unit

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/c63e4b09-a464-4916-9e5a-27130859c953)

- silicon wafer on which all logic implemented. One section of wafer is die and inside die, there is core. Die encapsulate core.
- Circuit is build in area of die so will exceed die area. Place all logical cells inside core. 

- Utilization factor of the core = Area occupied by netlist / Total area of the core.
  When netlist completely occupies core area then utilization factor is 100%. Then there will be no space to add any logic.
  Ideally a 50-60% utilization (of cells only usually) is good and Utilization factor will be 0.5/0.6

- Aspect ratio = Height of core / width of core. 
  When Aspect ratio = 1, signifies chip is square shaped core;
  When Aspect ratio is other than 1 signifies chip is rectangle shape core. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/9258984e-b452-4e1f-aefb-be3ed6234fad)

- Here, Utilization factor = (2 unit x 2 unit) / (4 unit x 2 unit) = 0.5
  Aspect ratio = (2 unit ) / (4 unit) = 0.5

**Concept of pre-placed cells**

The second step of floor planning is defining the locations of preplaced cells. 
lets consider a combo logic which consists of a massive number of gates (50,000). When implementing this on a single die the utilization factor will surely increase. Hence the gates are partitioned into smaller blocks with input and outputs between these blocks. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/d9d991ce-7e15-48b2-8546-47dcf9a4dcc1)

We cut big logic cells into different blocks, we extended IO pins, black box the blocks, and then separate the black boxes and implemented as two different IPs or modules. IPs are implemented once and can be instantiated multiple times to aid in reuseability of the function in the design.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/77cf4791-574c-4fc9-a81c-54399132b710)

IP's are preplaced cells as their arrangement is done by user-defined locations and hence placed in the chip before automated placement-and-routing. The automatic placement-and-routing will place the remaining logical cells in design onto chip. It is important to place the preplaced cells in locations that are relevant to the design as this lcoation won't change.
The arrangement of these IP's in a chip is referred as Floorplanning. 
Some example of IP's availale are Memory, Clock-gating cell, Comparator, Mux. All of them implemented once and can be instantiated multiple times on to netlist. This is part of top level netlist. They performs some functions, receive some inputs signals, they delivers some output signals but functionality of this particular cell implemented once. 
    
**De-coupling Capacitors**

Third step in floop planning is to define the decoupling capacitances around the preplaced cells. 
Memories are often placed close to the input side. Memory units serve as pre-placed cells. Now connectivity with these units is done through the supply/power lines in the chip. They are connected with wires. The physical distance between the source and the cell will cause a drop in the voltage. In such a scenario, if the voltage reaching the cell is not sufficient to meet the Noise Margin specifications, it would cause an unpredictable output at the cell. The solution for it is to use de-coupling capacitors to provide a "backup supply" closer to the unit(zero to minimal voltage drop due to very short distance).

How does a de-coupling capacitor work?
lets take an AND gate. During switching from 0 to 1 state, if the voltage being supplied to the gate from the Power line drops below the required voltage, the capacitor Cd discharges and supplies power to the AND gate temporarily to ensure correct voltage is being supplied. When no switching is taking place the Cd is charged by the Power lines. Hence it ensures proper voltage is being supplied to the gate during switching operations.
It also bypasses high frequency noise from other units and prevents crosstalk between closely placed cells.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/b43af33c-c793-4803-8852-feec7c24f657)

Decoupling capacitances are used to decouple circuits from the main supply, and they are placed closer to the cell. The decoupling capacitances are important during the switching activity as it makes sure signal is delivered with attentuation that lies in the noise margin regions (as opposed to huge attentuation that can take place because the main supply is physically far away from the cells. The decoupling capacitances replenish their own charge when there is no switching activity.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/136fd791-23ba-4c46-8370-5462514849aa)

**Power Planning**

The forth step is power planning. 
Macro is a predefined and reuseable blocks of logic which can perform specific tasks. There are two types of macros, namely:

    Hard macros --> non-flexible, PPA and timing is fixed, available as ICs, industry graded.
    Soft macros --> flexible, PPA and timing is unpredictable, synthesizable RTL.

The power fluctuation issue was stabilised for a local module using de-coupling capacitors. Now I will have to consider fluctuations between multiple such modules in the chip. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/4712a390-507d-4ae7-9083-a307bf6c9334)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/cc8e7f26-40b1-4df3-8d9a-50201fb8be09)

It is not feasible to have capacitors throughout the chip. However, if not considered it will lead to voltage drooping and ground bounce which will momentarily affect the working of the chip (it is bad for large designs). Voltage drooping is a condition in which multiple capacitors (of a bus) draw current from the same power line causing the source voltage to drop below the original value. Closely, ground bounce is a state when the ground value is slightly above zero because of many capacitors discharge current into a single ground line. These will definitely lead to uncertaintity in the internal functioning of the chip.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/2e38c719-d8b5-4e2a-9da4-4bfa16297f55)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/d2d0239e-0201-4028-987b-186a97c69108)

This is used for global communication between the different macros as the receiving macro (load) should receive the same signal sent from the sending macro (driver). Using one power supply to feen in the signal can cause problems in ground bounce or supply droop if multiple decoupling transistors try to charge or discharge at the same time. The solution to this problem is to use multiple sources for the power supply, where each cell will take its power from the nearest supply. The problem of placing those multiple power supplies is called power planning (in OpenLane, this is done post placement). 
The solution to this problem is the introduction of many other power lines in the form of a grid/mesh. Hence the capacitor closest to the power line can tap into whichever needed. VDD power lines are placed in vertically and horizontal layers with metal contacts. The GND lines are also placed similarly in the same level as VDD. However it is made sure that both these lines are isolated from each other. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/1e30f925-711c-4f12-80ad-495e6d6d8478)

**Pin placement**

The fifth step in floor planning is pin placement.
The connectivity between the cells is defined in the netlist, and pin placement is the problem of placing those pins on the chip's die. Note that clock pins are bigger than other pins as this pin drives more cells. 

A chip will have input as well as outputs and to tap into these values I will require pin placement on the chip. Once the design is complete, all the inputs and outputs are placed in a region specifically reserved for pins. This is done by adding a blockage element to that area to restrict the tool from placing cells. This is called as logical cell placement blockage.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/50f3b920-e729-46c1-af68-144c3094bdd4)

The pins are optimized by fanout from a common point and are placed in a random order in the reserved area. Many parameters are considered while placing the pins such as connectivity, proximity, type of pins (eg i/o, clk, power/gnd),.. etc. Clock signal is used to facilitate all the flops and sequential elements in the chip. Hence, the clk pin is larger than the i/o pins so that it offers least resistance to the path.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/12041dfd-ecdc-402a-8cc5-09ae0b6fc80a)

The sixth step is logical cell placement blockage where a blockage is placed in die area outside core to present tools from placing cells in that area.

**Floorplan using OpenLANE**

Note that when synthesis is performed for example a file will be created inside the results/synthesis directory. 
Inside the runs/<RUN_today_date> directory there is a config.tcl file which contains the default OpenLane configuration settings, and it is important to check whether our modifications are reflected in it.
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/f4a17a60-3d57-4b35-8cd5-a6a268d6cb3d)

Change switches/variables ( info under configuration) in the design config.tcl to suit your needs. It is not necesaary to set all switches. You can set any depends on where you are on floor. 

<pre>vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/configuration$ less README.md</pre>

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/b4d03e37-5cce-4a3b-9ee9-6bbe77e5b9e3)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/9f5de4f3-4b80-49e0-9f1a-7bc96a78fdd0)

These are all default values of floorplanning and placement switches in floorplan .tcl and placement .tcl file.

<pre>vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/configuration$ less floorplan.tcl</pre>

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/dd4dcbe8-77c7-409d-9fac-950d4cac1bdf)

These are default values which can be set. 

 <pre>set ::env(FP_IO_MODE) 1; # 0 matching mode - 1 random equidistant mode</pre>
FP_IO_MODE: How you want your pin configuration to be around core? FP mode - 1 means pin position randomly but equidistant mode.
When FP mode - 0 means pin position not equidistant. 
These are system default values which have lowest priority. (settings in floorplan.tcl / placement.tcl)
After that next priority to config.tcl of design (Note that these config.tcl files of designs are present in ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14_03_10_54) and then highest priority to pdk variant.tcl, here sky130A_sky130_fd_sc_hd_config.tcl 
In openlane flow, in config.tcl, FP_IO_VMETAL and FP_IO_HMETAL layer are one more than what is specified.  

**Floorplan Files and Steps to view floorplan**

To run the floorplanning after synthesis of the picorv32a design, I used the following command (During this, the 6 steps mentioned are done, and a .def is created in the results/floorplan directory inside the chosen design directory. The results can be found in OpenLane/designs//RUN_*/runs):

% run_floorplan

Note that some of the floorplan switches (can be included with the command above) are FP_CORE_UTIL (floorplan core utilization), FP_ASPECT_RATIO (floorplan aspect ratio), FP_CORE_MARGIN (Core to die margin area), FP_IO_MODE (defines pin configurations: 1 = equidistant and 0 = not equidistant), FP_CORE_VMETAL (vertical metal layer), and FP_CORE_HMETAL (horizontal metal layer). The default values of these are defined in OpenLane/configuration/floorplan.tcl. In order to overwite these, we can define those switches in OpenLane/designs//config.json. Note that in OpenLane, horizontal and vertical metal are one value added to the value we specify.
Successful floorplanning gives a .def file as output which contains the die area and placement of standard cells.
Here, .def (Design Exchange Format) file is created in floorplan directory.
<pre>vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-03_10-54/results/floorplan$ less picorv32a.floorplan.def</pre>

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/163208ab-b6c8-4cda-8742-039d9bda247e)
 
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/f40ad91c-26ff-451e-a11b-370f8c7ea055)
Here, DIEAREA ( 0 0 ) ( 660685 671405 ) ; This is area of complete die. 
1st '0' is lower left X; 2nd '0' lower left Y; '660685' is upper right X and '671405' is upper right Y. Using this calculate area of Die.
Unit is set by UNITS DISTANCE MICRONS 1000; databites units per micron i.e 1 micron is equal to 1000 databits units. So, ( 660685 671405 ) these numbers when divided by 1000, we get dimensions of chip in micrometer.

vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-03_10-54/logs/floorplan$ less 4-ioPlacer.log
Here we can see design.tcl file has overriden system defaults.

<pre>vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/configuration$ less README.md
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/configuration$ less floorplan.tcl</pre>

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/a130eba7-b5ef-403e-88fe-5793fe730752)

Here, design config.tcl file have default values. Ex: FP_CORE_UTIL = "50" 
    
<pre>vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-03_10-54$ less config.tcl</pre>
    
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/4101dc76-1fd3-4836-8bee-c0c78c8dbc37)

Here, switch values are overrideen. set ::env(FP_CORE_UTIL) "35"
    
 <pre>vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a$ less sky130A_sky130_fd_sc_hd_config.tcl</pre>

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/fcb79c53-2743-43ea-8c12-1fcaf7e92bc0)

Here set ::env(FP_CORE_UTIL) "35"

Note :  design config.tcl should overwrite system defaults. But one fact is that sky130A_sky130_fd_sc_hd_config.tcl has highest priority. so, it happens like that design config.tcl     switch value remains same due to pdk config.tcl. 
Ex: CORE_UTIL ="50" of sytem default should be overridden by 65 of design config.tcl. But  CORE_UTIL = 50 of config.tcl of pdk file doesnot allow to change switch CORE_UTIL = 65 of design config.tcl

**Review Floorplan Layout in Magic** 
Looking at .def file (floorplan result) doen't make sense . Don't know where what place? So, to see actual layout after floorplan, first done in Magic. 

Magic Layout Tool is used for visualizing the layout after floorplan. In order to view floorplan in Magic, following three files are required: 1. Technology File (sky130A.tech) 2. Merged LEF file (merged.lef) 3. DEF File
Tech file location : 

<pre>/home/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech</pre>

merged.lef file location:

<pre>~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-03_10-54/tmp</pre>

To view the layout of the floorplan in magic, I used the command below in the results/floorplan directory (note that in my case the pdk was previously downloaded on my desktop in the open_pdks directory):

<pre>~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-03_10-54/results/floorplan$ magic -T /home/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &</pre>

A screenshot of the obtained layout is below:
![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/1a1e08d7-2ef4-44ad-9c81-e3f1d52fab43)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/4d692249-90c2-411b-9a69-4b735f346ce8)

After zooming in (left click, right click, z), below is the obtained screenshots (note that when we highlight (s after positioning the cursor), we can type "what" in the tkcon window and it will provide the layer of the highlighted object. The standard cells can be found on left bottom corner of the layout, as floorplan does not place those):

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/cd2f66da-f78f-4684-a901-6c2d1d38bd6c)

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/7ca44908-52e4-4b5b-bc60-655b39629243)


#### Library Binding and Placement

**Netlist Binding and initial place design**

Placement involves the placing of standard cells onto the floorplan of the die/core. It occurs in 2 steps, that is, Global Placement and Detailed Placement.
Global Placement is a coarse placement of cells which will consider initial timing constraints, congestion and multi-voltage variants. However they are not legalised (meaning the cells are placed such that they are not present on the standard cell rows, not appended with each other [incase of high frequency operations] and they overlap other cells --> in short they arent placed perfectly). In global placement, tool finds optimal position for all cells which may not be legal and cells may overlap. Optimization is done through reduction of half parameter wire length.

In detailed placement, the tool changes the position of cells post global placement so as to legalise them. Legalisation occurs in Detailed Placement. This will give rise to new timing violations as the postions of cells will be minutely changed and hence the wire lengths (capacitances) will also change. This will have to be optimised to progress forward. 

The first step in placement and routing is binding the netlist with physical cells. This means taking every component in the netlist and giving them a proper width and height. These widths and heights are taken from the library. Library will have following infrmation: height and widhth, delay information of of each and every cell and required conditions of particular cell Ex. at what condition F/F sends output i.e. When condition?, various flavours of cells available based on timing condition and based on sapce available on floorplan. The library has various options of widths and heights for the same cell (bigger is faster). 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/8a4f5870-4bb1-4dd9-9b6d-b182262b6585)

The above image shows a physical view of logic cells.
These cells are placed onto the core space in the following manner. 
The second step in placement and routing is placement. 
In this step, the netlist is placed on the floor plan (which already has the preplaced cells by now). The placement is important as it affects the delays. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/72facaf9-f9c3-4041-b2eb-a4e27ed5e6f2)

The third step is optimized placement to ensure that the timing is maintained. The respective cells are placed as close as possible to the related derivatives. The wire capacitances are estimated and the placement is optimized by adding buffers (repeaters that replicate the original signal) where needed to maintain the integrity of the signal. The distances for signals are calculated according to slew values and transition delay. Criss cross can occur when placing, and should be avoided. In case signal intergrity fails due to large distance between the cells, repeaters (buffers) are placed in the path to reproduce the signal and drive it to the respective cell. Hence Area is compromised for better timing and performance.

**Need for Libraries and Characterization**

All stages of Logic Synthesis, floorplanning, placement, Clock Tree Synthesis and Routing need library characterization. 
Standard cells are placed inside libraries, which defines their functionalities and their different versions: different sizes and threshold voltages
Library file contains information about the gate functionality, dimensions, capacitance rating, timing and delay values and much more.
We build, characterise and model these cells so that the tool can understand it.

</details>

<h2 id="C7">Day 7</h2>

<details>

   <summary>Cell Design and Characteriztion Flow</summary>

**Inputs for Cell Design Flow**

For one standard cell, the cell design flow defined in the library consists of:

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/45a93fcd-60ad-4c67-bb5d-f9262f27ccfe)

It consists of 3 parts:-
1) Inputs
   - Inputs to cells from Process Design Kits.
   - pdks comes from foundary: consist of DRC and LVS rules, SPICE models, library and user-defined specs
   - PDKs --> files which contain information about the technology being used for your design.
   - DRC & LVS --> Physical design rules that need to be met so that the foundry can fabricate the cell.
   - SPICE Models --> contains characteristics of the transistors that will be used to build the cell (threshold voltage, aspect ratio, capacitances,
     etc).
   - library and user-defined spec --> cell height (space between Vcc and Gnd rails), cell width (delay constraints, drive strength), supply voltage
     (noise margin), metal layer specs (specific metal layer to be used), pin location (close to Vcc or Gnd).

2) Design steps: 
    - Circuit design --> The circuit is designed by making use of the industry parameters and inputs where sizing takes place.
      First step is to implement functionality.
      Second steps is to model PMOS and NMOS transistors. For instance, to model the aspect ratio of 2.5,the PMOS = 2.5 NMOS dimensions while keeping         height constant based on the technology file. Similarly, Switching threshold is also model based on the requirement.
    - Layout design --> build the circuit with transistors to meet the required functionality, apply Euler's Path (unidirectional traverse only) and          create the respective network graphs, implement the stick diagram of the circuit topology. Then stick diagram is converted to layout by sticking        to the DRC rules and LVS checks defined by the foundary.
    - Characterization --> specific flow; Gives information on Timing, Power and Noise in the form of .libs files along with functionality.

3-) Outputs: 
    - Circuit Description Language (CDL)
    - GSDII, LEF, extracted SPICE netlists (.cir) which includes the parasitics (resistand and capacitance of each cell)
    - Timing, noise, power .libs, function
    
**Typical Characterization flow**

There are few problems of Standard Cells in polygon level format (GDSII). Some of them are:

    * Extraction of functionality is complicated and unnecessary as it is known
    * Functional/Delay simulation takes way too long
    * Power extraction for a whole chip takes too long
    * Automatic detection of timing constraints (e.g. Setup time) is difficult

A solution to above problems is Cell Characterization. It is a simple model for delay, function, constraints and power on cell/gate level. 

Characterization Flow (GUNA). 
    1. Read the SPICE Model file     
    2. Read extracted SPICE netlist
    3. Recognise the behavior of the circuit design*
    4. Read sub-circuit of the design
    5. Set the Power supply
    6. Apply stimulus
    7. Provide the load capacitance (NLDM --> range of capacitances)
    8. Provide simultion constraints

These 8 steps are fed via a configuration file to the characterization software called "GUNA". And the software will generate timing, noise, power models,.libs function.

There are hence three characterization types: timing characterization, power characterization, and noise characterization.

##### General Timing and Characterization Parameters

**Timimg Threshold Definations**

Timing Characterisation --> Delays between input and output wave from (Propagation Delay), Rise time; Fall time delays (Transition delay).
Timing threshold definitions are points whose definitions help us calculate slew from the waveforms (definitions are for slew_low_rise_thr, slew_high_rise_thr, slew_low_fall_thr, and slew_high_fall_thr), and the delay of the cell between input and output plots (definitions are for in_rise_thr, in_fall_thr, out_rise_thr, and out_fall_thr).

Solution --> Choosing the correct threshold points, Having proper circuit designs to reduce the wire delays. Negative delays are intolerable. 

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/82b7371a-846f-4d38-8cdb-d01395f86d4d)

**propagation delay and transition time**

The choice of the threshold definitions is important to get correct propagation delay and transition time. 
Propagation delay = time(out_thr) - time(in_thr). 
Fall/Rise Transition time = time(slew_high_thr) - time(slew_low_thr). 

</details>

<h2 id="C8">Day 8</h2>

<details>

   <summary>Design library cell using Magic Layout and ngspice characterization</summary>

##### Labs for CMOS Inverter ngSpice Simulations

**Spice Deck creation for CMOS Inverter**

  To simulate the inverter, first its spice deck needs to be created.
  Recall that a spice deck includes component connectivity, component values, identify nodes, Name nodes. The netlist to simulate includes model  
  description, netlist description, simulation type and parameters, and needed libraries.

**Note: Spice Simulation Lab from ShonTaware**

**Threshold Voltage Vm**

  Recall that the switching threshold (Vm, used to evaluate static behavior) of a CMOS inverter is the point on the voltage transfer characteristic curve where input voltage equals output voltage: at which both PMOS and NMOS are in saturation region which gives rise to a leakage current.

**Lab VSDcell gitclone**mariam aashish


#### Inception of Layout : A CMOS Fabrication Process

**16-mask CMOS process steps**

1-) Selecting a substrate: selecting body/substrate material (P-type substrate)
    High resistivity(5 ~ 50ohms),doping level(10 to power 15 / cm cube ), orientation(100)

2-) Creating active region for transistors: First create isolation between active region pockets by SiO2, then perform ~40nm SiO2 on P-type substare and then ~80 nm Si3N4 deposition, then ~1nm photoresist deposition, and then apply photolithography (part of photoresist is covered by mask1 to protect it against UV light). Areas that are not protected against UV light are then washed out using developing solution and etching is done, then photoresist is chemically removed. Then we place CMOS in oxidation furnace,and field oxide is grown (process is called LOCOS or Local Oxidation of Silicon). After that, Si3N4 is stripped using hot phospheric acid.

3-) N-well and P-well formation: Photoresist is deposited and mask2 is used to define the protected area. UV light reacts with exposed area, and then we wash the area which is unprotected. After that, the mask is removed (this is lithography). Ion implantation by Boron for P-well is then done, followed by ion implementation of Phosphorous for N-well formation (after photoresist, mask application, and wash out). Then the CMOS is put in a high temperature furnace for a high temperature for a long time, which will diffuse the N-well and P-well (the pockets). In N-well the pmos will be created and in P-well the nmos will be created.

 ![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/d8c372ae-80b4-4f29-b44f-e71759c64e5b)

4-) Formation of gate terminal: Doping Concentration and Oxide Capacitance are important term in gate formation as they control threshold voltage Vt. The nmos and pmos gates are formed by depositing photoresist, using mask4, exposing UV, applying wash out, removing the mask, doping with Boron to modify the doping concentration in the P-well. Similar steps are repeated for P-well to control the threshold voltage or doping concentration in the N-well. Extra oxide is diluted then re-grown again to give high quality oxide. A polisilicon layer is then deposited to form the gate, then N-type material is doped on the gate to make it low resistance. Then photoresist is dumped, mask6 is used, unprotected material is washed out, mask is removed, and the remaining areas of polisilicon are etched away.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/0da6abab-c9b2-4442-8038-f294f75ebe35)

5-) Lightly Doped Drain (LDD) formation: LDD is formed to prevent hot electron effect and short channel effect: P+, P-, P doping profile is needed for pmos and N+, N-, N profile is needed for nmos. Why need P- and N- ? Two Reasons Hot Electron Effect and short channel Effect
In Hot Electron Effect, When device size reduces, electric field E = V/d increases, energy of electron and holes attains tremendous amount of energy which break si-si bonds leading to some more addition of electron and holes which we don't want because control doping profile very well. 
Enegry might be so high that it crosses 3.2eV barrier between si conduction band and SiO2 conduction band. If it crosses this band it might enters into oxide layer which is present above substate which create issue.   
Short channel effect, when device size reduces, drain field penetrate channel, difficult to Gate to control current.

Photolithography is applied, Phosphorous is doped to create N- implants on P-well side. The lithography is repeated for N-well side and we get P- implant after doping Boron. A thick Si3N4 or SiO2 is deposited on whole material and plasma anisotropic etching takes place to create the side-wall spacers where source and drain will be later affected in next step.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/efa07cff-941f-4a29-8d38-241a97faf3ba)

6-) Source and drain formation: Thin layer of screen oxide is added to avoid channelling during implantation. Then after photolithography, Aresenic implantation/doping takes place above P-well (below side-wall spacers). Then after photolithography, Boron implantation/doping takes place above N-well (below side-wall spacers). The material is put in high temperature furnace (called high temperature annealing).

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/8a2ecec0-1aa5-4a6a-8c6d-da65712dec66)

7-) Contacts and local interconnect formation: Etching/removal of screen oxide by HF solution. Then Ti (Titinum) is deposited on material for low resistant contacts using sputtering (hitting Ti by Ar+ and the then Ti will be deposited on the substrate with heating). Then lithograpphy is used, and RCA cleaning is used to etch TiN. Result = TiN used only for local communication.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/e4c04c01-1771-4783-9c01-1467a81fbc5f)

8-) Higher level metal formation: A thick layer of SiO2 doped with phosphorous or boron is deposited on the material. CMP is used for planarizing the wafer (polishing it), then photolithograpphy is used in areas where we want the metal to be formed, then TiN is deposited. Tungsten is then deposited, followed by CMP again. Al is then deposited on the material, and photolithography is used. Result is we get the first layer of metal. To get higher layers, SiO2 is deposited again, CMP is used, lithography is used, TiN is deposited, Tungsten is deposited, followed by CMP again. Al is then deposited on the material, and photolithography is used. The result is a metal layer which is higher and thicker (thicker Al). Si3N4 is deposited on top to protect the whole chip. Finally, mask16 is used to open contact holes on this top layer and connect the highest metal layer to the top.

![image](https://github.com/ManjuLanjewar/VSD_HDP/assets/157192602/01e2d91c-dc52-42ec-9092-f0bbe06e1054)

CMOS after finishing the fabrication process
