# 6-Band Analog Equalizer for Electric Piano

<p align="center">
  <em>Universidad del Istmo de Guatemala</em><br>
  <em>Faculty of Engineering</em><br>
  <em>6-Band Analog Equalizer for Electric Piano</em><br>
  <em>Microelectronic Devices</em>
</p>

<div align="center">
  <img src="Imagenes/Logo_UNIS.png" alt="UNIS Logo" width="45%"/>
</div>

<p align="center">
  <em>Uriel Pérez</em><br>
  <em>Diego Lemus</em><br>
  <em>Diego Solis</em><br>
  <em>2026</em>
</p>

## Project Description

This repository contains the development of a six-band analog equalizer designed for audio processing of an electric piano. The main objective of the project was to design, simulate, and analyze a system capable of modifying different regions of the instrument's frequency spectrum, allowing independent control of bass, mids, presence, attack, and brightness.

The circuit is based on active band-pass filters built from second-order Sallen-Key stages. Each band is formed by cascading a high-pass filter and a low-pass filter, resulting in a fourth-order band-pass response. Afterwards, the filtered signals are sent to an inverting summing stage, where the gain control for each band is implemented.

The design was oriented toward an adequate response for an electric piano, whose useful range is approximately between 40 Hz and 6 kHz. To improve the response at the center frequency of each band, a two-octave bandwidth was used, reducing attenuation at the center point of each filter.

## Project Objective

To design a six-band analog equalizer for an electric piano that allows different frequency ranges to be amplified or attenuated, using active Sallen-Key filters, per-band gain control, and an output stage capable of driving an 8 Ω speaker.

## System Architecture

The system is divided into four main stages:

1. **Coupling stage:** uses a voltage follower to provide high input impedance and prevent signal loss from the instrument.
2. **Filtering stage:** formed by six active band-pass branches, each built with Sallen-Key high-pass and low-pass filters.
3. **Gain control stage:** allows the amplification or attenuation of each band to be adjusted using potentiometers.
4. **Power stage:** uses BJT transistors in a class AB configuration to deliver the processed signal to an 8 Ω speaker.

## General Diagram

Electric Piano Input  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
High-Impedance Buffer  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Six Band-Pass Filters in Parallel  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Per-Band Gain Control  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Active Inverting Summer  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Class AB Power Stage  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
8 Ω Speaker

## Frequency Bands

The bands were selected taking into account the musical behavior of the electric piano and the most important areas of its sound spectrum.

| Band | Initial Range | Center Frequency | Musical Function |
|---:|---:|---:|---|
| 1 | 40 - 80 Hz | 57 Hz | Controls the depth and weight of the low notes |
| 2 | 80 - 200 Hz | 127 Hz | Adjusts the body and warmth of the instrument |
| 3 | 200 - 500 Hz | 316 Hz | Helps correct dull or boxy sounds |
| 4 | 500 - 1500 Hz | 886 Hz | Adds definition and presence in the mix |
| 5 | 1500 - 3000 Hz | 2121 Hz | Controls the attack and detail of the sound |
| 6 | 3000 - 8000 Hz | 4900 Hz | Adjusts brightness and upper harmonics |

## Cutoff Frequencies Used

To improve the performance of each filter, a two-octave bandwidth around the center frequency was used. The final frequencies used for the design were:

| Band | Lower Cutoff | Upper Cutoff | Center Frequency |
|---:|---:|---:|---:|
| 1 | 28.5 Hz | 114 Hz | 57 Hz |
| 2 | 63.5 Hz | 254 Hz | 127 Hz |
| 3 | 158 Hz | 632 Hz | 316 Hz |
| 4 | 443 Hz | 1772 Hz | 886 Hz |
| 5 | 1060.5 Hz | 4242 Hz | 2121 Hz |
| 6 | 2450 Hz | 9800 Hz | 4900 Hz |

## Filter Construction

Each equalizer band is composed of:

- A second-order high-pass filter
- A second-order low-pass filter
- A gain control stage
- A connection to the active summer

By cascading the high-pass filter and the low-pass filter, a fourth-order band-pass response is obtained. This configuration allows better separation between bands and an approximate attenuation of **-40 dB/dec** outside the passband.

The filters were designed with a Butterworth-type response, using an approximate quality factor of:

**Q = 0.707**

This value allows a flat response in the passband and controlled attenuation at the cutoff frequencies.

## Sallen-Key Topology

The project uses the Sallen-Key topology to implement the second-order active filters. This topology was selected because it allows high-pass and low-pass filters to be built with operational amplifiers, resistors, and capacitors, while maintaining a simple structure suitable for audio applications.

Each filter was configured with unity gain, leaving the level control of each band for a later stage.

## Calculated Component Values

### Band 1 - 57 Hz

| Component | HP2 | LP2 |
|---|---:|---:|
| R1 | 3.9 kΩ | 27 kΩ |
| R2 | 8.2 kΩ | 16 kΩ |
| C1 | 1 µF | 0.1 µF |
| C2 | 1 µF | 0.047 µF |

### Band 2 - 127 Hz

| Component | HP2 | LP2 |
|---|---:|---:|
| R1 | 18 kΩ | 12 kΩ |
| R2 | 36 kΩ | 6.8 kΩ |
| C1 | 0.1 µF | 0.1 µF |
| C2 | 0.1 µF | 0.047 µF |

### Band 3 - 316 Hz

| Component | HP2 | LP2 |
|---|---:|---:|
| R1 | 6.8 kΩ | 47 kΩ |
| R2 | 15 kΩ | 30 kΩ |
| C1 | 0.1 µF | 0.01 µF |
| C2 | 0.1 µF | 0.0047 µF |

### Band 4 - 886 Hz

| Component | HP2 | LP2 |
|---|---:|---:|
| R1 | 24 kΩ | 16 kΩ |
| R2 | 51 kΩ | 10 kΩ |
| C1 | 0.01 µF | 0.01 µF |
| C2 | 0.01 µF | 0.0047 µF |

### Band 5 - 2121 Hz

| Component | HP2 | LP2 |
|---|---:|---:|
| R1 | 11 kΩ | 6.8 kΩ |
| R2 | 22 kΩ | 4.3 kΩ |
| C1 | 0.01 µF | 0.01 µF |
| C2 | 0.01 µF | 0.0047 µF |

### Band 6 - 4243 Hz

| Component | HP2 | LP2 |
|---|---:|---:|
| R1 | 4.7 kΩ | 30 kΩ |
| R2 | 9.1 kΩ | 18 kΩ |
| C1 | 0.01 µF | 0.001 µF |
| C2 | 0.01 µF | 470 pF |

## Gain Control

The gain control stage was implemented using an inverting summer with a feedback resistor, series resistor, and potentiometer. This allows the contribution of each band to the final output to be modified.

The designed gain range was approximately:

**-12 dB to +12 dB**

The selected commercial values were:

- Feedback resistor: **Rf = 13.3 kΩ**
- Minimum series resistor: **Rs = 3.3 kΩ**
- Potentiometer per band: **Rp = 50 kΩ**

With these values, the following results are obtained:

| Condition | Rp Value | Approximate Gain |
|---|---:|---:|
| Maximum boost | 0 Ω | +12.12 dB |
| Unity gain | 10 kΩ | 0 dB |
| Maximum attenuation | 50 kΩ | -12.06 dB |

## Output Stage

For the system output, the following speaker was considered:

**8 Ω / 35 W RMS**

This speaker was selected because it allows the system to work with a class AB power stage without requiring excessive currents. It also provides an adequate safety margin to avoid saturation or damage caused by signal peaks.

The maximum RMS voltage allowed by the speaker was calculated using:

**Vrms = sqrt(P × R)**

**Vrms = sqrt(35 W × 8 Ω)**

**Vrms ≈ 16.7 V**

This makes it possible to establish a safety limit for the equalizer output signal.

## LTspice Simulation

The design was simulated in LTspice using TL081 operational amplifier models. The simulations included:

- Individual analysis of high-pass and low-pass filters
- Comparison between one-octave and two-octave bandwidths
- Joint simulation of the six band-pass bands
- Validation of the inverting summing stage
- Evaluation of the gain range of **-12 dB**, **0 dB**, and **+12 dB**

During the initial one-octave analysis, it was observed that the maximum filter response did not reach 0 dB, so the bandwidth was adjusted to two octaves. With this correction, the attenuation at the center frequency was considerably reduced.

## Main Results

- Six equalization bands focused on the sound range of the electric piano were designed.
- Each band was implemented as a fourth-order active band-pass filter.
- The Sallen-Key topology was used for the high-pass and low-pass filters.
- The two-octave bandwidth improved the response at the center frequency.
- The inverting summing stage allowed each band to be controlled within an approximate range of ±12 dB.
- The output stage was designed considering an 8 Ω and 35 W RMS speaker.
- The LTspice simulations made it possible to verify the general behavior of the system.

## Tools Used

- LTspice
- TL081 operational amplifiers
- Active Sallen-Key filters
- BJT transistors for class AB stage
- Okawa-denshi tool for filter calculation
- AC analysis for frequency response
- Analog circuit design and analysis

## Team Members

- Uriel Pérez
- Diego Lemus
- Diego Solis

## Project Video

The following link presents the general operation of the project:

[Watch video on YouTube](https://youtube.com/shorts/Q-_U898Za5Q)
