# Telescopic OTA LDO:

## Abstract:

* This work presents a capacitor-less Low Dropout Regulator (LDO) designed using dual-path Ahuja compensation to achieve fast transient response and high stability without the need for large external capacitors. The compensation technique leverages strategic placement of poles and zeros through a buffered feedforward path, enhancing phase margin and improving both transient behavior and power supply rejection (PSR).
* The LDO is implemented in a 90nm CMOS process, occupying a compact silicon area of 0.037 mm². Measurement results show minimal output voltage deviation 44 mV undershoot and 46 mV overshoot—during a 0 to 15 mA load step with a 200 ps edge transition. The PSR is measured at better than 46 dB at low frequencies and remains above 8 dB across the entire frequency range under full load using only a 200 pF integrated capacitor.

## Introduction:

* Low Dropout Regulators (LDOs) with high Power Supply Rejection Ratio (PSRR) over a wide frequency spectrum are critical components in noise-sensitive systems such as radio frequency (RF) and Internet of Things (IoT) applications. These systems demand compact, energy-efficient voltage regulation capable of isolating supply noise across broad frequency bands.
* Among various LDO topologies, capacitor-less designs have gained substantial attention from both academia and industry due to their minimal silicon footprint and compatibility with full integration in system on chip (SoC) solutions.
* However, a key challenge in capacitor-less LDOs lies in the stability of the control loop. The absence of a large off-chip output capacitor results in the output node being associated with a non-dominant pole, which complicates frequency compensation and loop stability.
* To address these issues, several compensation techniques have been proposed, such as Miller and Ahuja compensation schemes. Ahuja compensation, in particular, has shown promise due to its ability to extend the capacitive load range while enhancing PSRR.
* Despite these advantages, Ahuja compensation may introduce complex conjugate poles at the output node, potentially leading to degraded stability and peaking in the frequency response. Attempts to mitigate these effects by modifying only the main feedback loop are often constrained and insufficient. Moreover, many prior works limit their stability analysis to the dominant and non-dominant poles of the main loop, overlooking the potential impact of additional feedback paths and signal interactions.
* While Ahuja compensation has frequently been implemented using folded cascode operational transconductance amplifiers (OTAs), this work adopts a telescopic OTA architecture instead. Telescopic OTAs offer superior performance in terms of speed, power efficiency, and noise characteristics when compared to folded cascode designs. Their simpler structure results in higher bandwidth with reduced parasitic loading and lower current consumption.
* Additionally, telescopic OTAs provide better phase margin and occupy less chip area. Although they have limited output swing and input range, these trade-offs are acceptable in high-speed, low-power LDO applications where compactness and performance are prioritized.
* In this paper, we propose a capacitor-less LDO design that leverages Ahuja compensation in conjunction with a telescopic OTA architecture to achieve high PSRR and rapid transient response, while ensuring stability across a wide load current range with minimal on-chip capacitance.
* Section II provides a detailed analysis and simulation results of the proposed LDO, emphasizing zero-pole placement and the role of Ahuja compensation in stabilizing the system under multiple-loop dynamics.

### Capacitor-less LDO with Ahuja compensation in two paths circuit:
![1](https://github.com/user-attachments/assets/4bb1c013-2b4e-4ecc-a3b5-6aba45bb6417)


## Proposed LDO figure:

* The schematic of the proposed LDO is shown in Figure below.The inserted compensation capacitors C1, C2, zero-pole placement Rz and Cz enhance the stability of the LDO. The zero-pole placement eliminants the output voltage ringing.

### Capacitor-less LDO with dual-path compensation and zero-pole placement circuit:
![2](https://github.com/user-attachments/assets/a21d33f3-006c-4dcf-9664-4888e94826e9)

## LUT FOMS and Dimensions of LDO Transistors:

| Transistor     | gm/Id (1/V) | gm·ro (–) | Id/W (A/m) | L (µm) | W (µm)   |
|----------------|-------------|-----------|------------|--------|----------|
| M<sub>pass</sub>        | 15          | 10.5      | 9.369      | 0.1    | 213.464  |
| M<sub>1,2,3,4</sub>     | 15          | 30.866    | 1.29514    | 0.64   | 19.302   |
| M<sub>6,7,8,9</sub>     | 14.5        | 30.866    | 2.64       | 0.7    | 9.44     |
| M<sub>10,11,12</sub>    | 14.5        | 30.866    | 0.909      | 0.91   | 55       |

### Problems in Ahuja Compensation:

* The Transfer function for the main loop with C1 without taking care of pole zero placement.
* We shall assume C1 and C3 to be the net capacitances of the first and second stages with transconductances gm9 and gm5. The compensation transistor
has a transconductance gm6 and a parasitic gate-source capacitance Cgs6. Small-signal analyses of the above circuits yield, after suitable approximations.
* W0 = 2f0 is the unity gain bandwidth. An inspection of the loop gain plot reveals a system that satisfies classical stability criteria, exhibiting a phase margin of approximately 101° and a prominent gain peaking (figure) phenomenon that remains well below the 0 dB crossover point.
  
### Loopgain Plot without Rz and Cz:
![3](https://github.com/user-attachments/assets/a5219254-ced5-4aa3-afcf-6fbc5562830d)

* This peaking is attributed to a pair of complex conjugate poles, introduced by the compensation strategy. While this configuration ensures adequate frequency domain stability, its time-domain response under dynamic load conditions is suboptimal.
* Specifically, with a compensation capacitor Cc1 of 25 pF, the output demonstrates noticeable voltage ringing (figure) during load transients. This suggests
that despite a sufficient phase margin, the system’s damping is inadequate, potentially due to a low damping factor associated with the complex pole pair.
* Consequently, further investigation beyond traditional phase and gain margin analysis is necessary to fully understand and mitigate transient performance limitations.
  
### Load Transient response plot without Rz and Cz:
![4](https://github.com/user-attachments/assets/3eabb8e2-cce0-4b71-bcd2-39354342dd38)

* The introduction of a pole-zero pair is achieved by appropriately selecting the values of Rz and Cz, which are chosen to be 1kohm and 10 pF,respectively. This compensation strategy effectively modifies the frequency response of the system.
* The below figure, shows the gain peaking typically associated with a complex conjugate pole pair is no longer observed. This indicates that the non
dominant pole pair has been sufficiently separated or damped, thereby eliminating the gain peaking and enhancing the overallstability of the loop. And no voltage ringing is observed as seen in below figure.

### Load Transiet Response plot with Rz and Cz:
![5](https://github.com/user-attachments/assets/f086109f-a345-4538-b3ff-3adf0b2b31e0)

### Loopgain Plot with Rz and Cz:

![6](https://github.com/user-attachments/assets/693833c8-835a-48fc-9dd4-e59b1507e40f)

## PSRR of the Proposed LDO:

* In low-dropout regulators (LDOs), supply ripple can propagate to the output through three key routes: the bandgap reference, the error amplifier, and the power transistor. While the LDO typically maintains good power supply rejection (PSR) within its bandwidth, performance degrades at mid-to-high frequencies,primarily due to the power transistor’s influence.
* To address this, the use of Ahuja compensation, has proven effective in boosting PSR by improving signal path characteristics. In addition, incorporating an R1 and C4
network creates a ripple voltage at the output that is phase shifted relative to the incoming disturbance, allowing partial cancellation. This zero-pole engineering further enhances PSR.
* As illustrated in figure, both simulation and measurement results confirm that the minimum PSR improves from –6.68 dB to –17.95 dB.

### PSRR comparison with and without Rz and Cz:
![8](https://github.com/user-attachments/assets/09fbe589-063c-4076-8157-996e1ed7a4e0)


### Proposed LuT based Design Methodolgy for LDOs:
* This section presents a device LuT-based design methodology.Transistor sizing based on lookup-tables instead of MOSFET square law brings hand calculations closer to Spice simulations.The detailed design procedure is described below:

### 1) Given: Iload_min,Ibias and Loopgain
### 2) Pass-FET sizing:
* Assume ( gm/Id ) = 15 and LPass = Lmin (for low area).
* Use LuT techplots to find (gm*ro) and (Id/W).
* Calculate pass-FET width by:
* W5= [ILoad_min/(Id/W)]
* APass ≃ (gm5 ∗ rds5)

### 3) Calculate OTA Gain:

* Calculate Gain Aota as,
* Aota = gm9 (gm1rds1rds2 ∥ gm6rds6rds9)

### 4) Error Amplifier Design:
* To calculate Aspect ratio of NMOS (W6,7,8,9/L6,7,8,9) and PMOS (W1,2,3,4/L1,2,3,4).
* Overall Gain will be like, Aldo = (gmro)^2_ota x (gmro)pass
• Assume (gm/Id) = 15, From Aldo find (gmro)pass from techplot.
• Find (gmro)ota by substituting the values of Aldo and (gmro)pass.
• We will get the lenght from the (gmro)/(gm/Id) techplots of PMOS and NMOS.
• Now, go to (Id/W) techplot and find (Id/W) at ( gm/Id ) = 15.
* Use,W =[(Ibias/2)/(Id/W)]
* You will get W and this is how you will get your required aspect ratio for each MOSFET in OTA.

### 5) Current Mirror Design:
• Assume ( gm/Id ) = 15 and L = Lmax because longer channel length improves accuracy, output resistance,and matching.
• Now, From (Id/W) techplot of NMOS find,
* W =[Ibias/(Id/W)]
* The outlined methodology ensures accurate transistor sizing that aligns well with both analytical calculations and simulation results.
* The developed design principles are incorporated into a lookup table (LuT)-based transistor sizing framework, which offers scalability across various LDO topologies and technology nodes.
* This approach, which utilizes technology characterization plots (techplots), provides improved accuracy and practicality compared to traditional square-law-based sizing methods.


### Techplots:

<img width="1920" height="1080" alt="Screenshot from 2025-05-06 16-11-23" src="https://github.com/user-attachments/assets/27fc86aa-c02d-4fa7-baed-e22d7d2a3f69" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 16-07-44" src="https://github.com/user-attachments/assets/daa985fc-c323-4b41-91f2-a09ede24ae80" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 16-07-34" src="https://github.com/user-attachments/assets/3de72104-dbc4-4fa3-9937-24b448dab470" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 16-03-31" src="https://github.com/user-attachments/assets/f8f087ca-6b96-472a-8419-b13206f2b94e" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 16-03-24" src="https://github.com/user-attachments/assets/ccb53443-5025-4346-8426-9627d4cfb3e0" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 15-05-00" src="https://github.com/user-attachments/assets/65ce0a85-62aa-4ee6-962d-d317745a11e6" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 15-04-06" src="https://github.com/user-attachments/assets/78ff308d-bf6f-42bf-859b-75bce28c96cf" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 15-03-32" src="https://github.com/user-attachments/assets/e9944913-efcd-41c9-be6a-2f937c76a897" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 15-01-08" src="https://github.com/user-attachments/assets/41e98082-46da-4bad-bb78-2665b4ff515b" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 15-00-19" src="https://github.com/user-attachments/assets/caecd8a4-b7f2-4d0d-bf6c-c88948ac38a8" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 14-57-33" src="https://github.com/user-attachments/assets/14ed73a5-7c12-4ae6-b1c7-aeca06b0f6ef" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 14-57-30" src="https://github.com/user-attachments/assets/7145e761-c176-4166-9bc3-f4d850af5061" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 14-57-17" src="https://github.com/user-attachments/assets/12cad6ab-1d0f-4e3e-91dd-eba6631c5967" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 14-51-08" src="https://github.com/user-attachments/assets/30a46184-a53f-48b4-8c84-42caf5ae4d79" />
<img width="1920" height="1080" alt="Screenshot from 2025-05-06 14-50-55" src="https://github.com/user-attachments/assets/0741980d-7163-4318-ad47-692f896a2b90" />

## LUT FOMS and Dimensions of LDO Transistors:

| Transistor     | gm/Id (1/V) | gm·ro (–) | Id/W (A/m) | L (µm) | W (µm)   |
|----------------|-------------|-----------|------------|--------|----------|
| M<sub>pass</sub>        | 15          | 10.5      | 9.369      | 0.1    | 213.464  |
| M<sub>1,2,3,4</sub>     | 15          | 30.866    | 1.29514    | 0.64   | 19.302   |
| M<sub>6,7,8,9</sub>     | 14.5        | 30.866    | 2.64       | 0.7    | 9.44     |
| M<sub>10,11,12</sub>    | 14.5        | 30.866    | 0.909      | 0.91   | 55       |

## Conclusion:

The proposed capacitor-less LDO, implemented with dual-path Ahuja compensation, demonstrates excellent transient response, robust PSR, and high stability without relying on large off-chip capacitors. Using 90nm CMOS and maintaining performance under rapid load transients and wide frequency ranges, this design proves highly suitable for modern SoC and low-power mixed-signal applications requiring fast, reliable on-chip voltage regulation.
