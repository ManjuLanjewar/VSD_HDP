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




