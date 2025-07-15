# Telescopic OTA LDO:

## Abstract:
* This work presents a capacitor-less Low Dropout Regulator (LDO) designed using dual-path Ahuja compensation to achieve fast transient response and high stability without the need for large external capacitors. The compensation technique leverages strategic placement of poles and zeros through a buffered feedforward path, enhancing phase margin and improving both transient behavior and power supply rejection (PSR).
* The LDO is implemented in a 90nm CMOS process, occupying a compact silicon area of 0.037 mm². Measurement results show minimal output voltage deviation 44 mV undershoot and 46 mV overshoot—during a 0 to 15 mA load step with a 200 ps edge transition. The PSR is measured at better than 46 dB at low frequencies and remains above 8 dB across the entire frequency range under full load using only a 200 pF integrated capacitor.

## Introduction:
* Low Dropout Regulators (LDOs) with high Power Supply Rejection Ratio (PSRR) over a wide frequency spectrum are critical components in noise-sensitive systems such as radio frequency (RF) and Internet of Things (IoT) applications. These systems demand compact, energy-efficient voltage regulation capable of isolating supply noise across broad frequency bands.
* Among various LDO topologies, capacitor-less designs have gained substantial attention from both academia and industry due to their minimal silicon footprint and compatibility with full integration in system-on-chip (SoC) solutions.
* However, a key challenge in capacitor-less LDOs lies in the stability of the control loop. The absence of a large off-chip output capacitor results in the output node being associated with a nondominant pole, which complicates frequency compensation and loop stability.
* To address these issues, several compensation techniques have been proposed, such as Miller and Ahuja compensation schemes. Ahuja compensation, in particular, has shown promise due to its ability to extend the capacitive load range while enhancing PSRR.
* Despite these advantages, Ahuja compensation may introduce complex conjugate poles at the output node, potentially leading to degraded stability and peaking in the frequency response. Attempts to mitigate these effects by modifying only the main feedback loop are often constrained and insufficient. Moreover, many prior works limit their stability analysis to the dominant and non-dominant poles of the main loop, overlooking the potential impact of additional feedback paths and signal interactions.
* While Ahuja compensation has frequently been implemented using folded cascode operational transconductance amplifiers (OTAs), this work adopts a telescopic OTA architecture instead. Telescopic OTAs offer superior performance in terms of speed, power efficiency, and noise characteristics when compared to folded cascode designs. Their simpler structure results in higher bandwidth with reduced parasitic loading and lower current consumption.
* Additionally, telescopic OTAs provide better phase margin and occupy less chip area. Although they have limited output swing and input range, these trade-offs are acceptable in high-speed, low-power LDO applications where compactness and performance are prioritized.
* In this paper, we propose a capacitor-less LDO design that leverages Ahuja compensation in conjunction with a telescopic OTA architecture to achieve high PSRR and rapid transient response, while ensuring stability across a wide load current range with minimal on-chip capacitance.
* Section II provides a detailed analysis and simulation results of the proposed LDO, emphasizing zero-pole placement and the role of Ahuja compensation in stabilizing the system under multiple-loop dynamics.

* Image of Capacitor-less LDO with Ahuja compensation in two paths:
![1](https://github.com/user-attachments/assets/4bb1c013-2b4e-4ecc-a3b5-6aba45bb6417)

## Proposed LDO:

* The schematic of the proposed LDO is shown in Figure below.The inserted compensation capacitors C1, C2, zero-pole placement Rz and Cz enhance the stability of the LDO. The zero-pole placement eliminants the output voltage ringing.
* Image of Capacitor-less LDO with dual-path compensation and zero-pole placement:
![2](https://github.com/user-attachments/assets/a21d33f3-006c-4dcf-9664-4888e94826e9)




