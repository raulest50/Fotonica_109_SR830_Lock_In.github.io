# Fotonica_109_SR830_Lock_In.github.io
Lecture para introducir sobre uso del Lock In (SR 830) para estudiantes nuevos en el laboratorio de Fotonica de UnalMed.

https://raulest50.github.io/Fotonica_109_SR830_Lock_In.github.io/

# Lock-in Amplifiers in Atmospheric Lidar Systems (2015–2025)

## Introduction

Atmospheric lidar systems often face the challenge of detecting extremely weak optical signals against overwhelming noise (e.g. daylight or electronic noise). A lock-in amplifier (LIA) is a phase-sensitive detection technique that addresses this by isolating signals at a known reference frequency. In practice, the lidar transmitter (laser or LED) or detection is modulated, and the return signal is demodulated at that same frequency. This approach extracts the weak backscatter signal while rejecting ambient background and 1/f noise​
pdfs.semanticscholar.org
. Over the past decade (2015–2025), numerous studies have applied lock-in amplifiers – including modern digital implementations – to atmospheric lidars of various types. The results consistently show improved performance: reduced noise and background interference, enhanced signal-to-noise ratio (SNR), extended measurement range, and even new measurement capabilities​
pdfs.semanticscholar.org
​
pubmed.ncbi.nlm.nih.gov
. Below, we review how LIAs have been implemented in different lidar modalities (LED-based, Raman, Doppler, DIAL) and the specific performance gains achieved in each case.

## LED-Based Lidar Systems

LED-based lidars use low-power, incoherent light sources, making signal detection particularly difficult. To overcome this, researchers employ high-frequency modulation of the LED output and lock-in detection to boost sensitivity. For example, Shiina et al. designed an “LED mini-lidar” for near-ground atmosphere monitoring that drives a simple LED with <1 MHz pulses​
colab.ws
. Even though only a few photons return per pulse, the high repetition rate allows the SNR to increase through rapid averaging​
colab.ws
. A custom high-speed photon counting receiver (4 ns bins) synced to the modulation was used as a lock-in–like detector. This mini-lidar demonstrated aerosol and dust measurements up to ~500 m at night and ~100 m in daytime, using a 20 cm lens​
colab.ws
. The ability to operate in daytime is credited to the high-frequency modulation and narrow-band detection that filters out ambient light. Other LED-lidar implementations use traditional lock-in hardware. A 2024 study by Li and Wang describes a mobile transmissometer (a simplified horizontal lidar) using a continuous 532 nm LED or laser source with a mechanical chopper and LIA in the receiver. The optical chopper modulates the beam at a fixed frequency, and a lock-in amplifier referenced to the chopper extracts the signal from the photodetector. This scheme “effectively suppress[es] optical noise” from ambient and system sources​
researchgate.net
. By collimating and chopping the continuous beam, then detecting with a phase-sensitive amplifier, the system achieved better than 10% visibility measurement accuracy, something difficult for standard lidar under high background noise​
researchgate.net
​
researchgate.net
. Multi-wavelength LED lidars have also been explored (e.g. a recent multi-color LED lidar prototype​
link.springer.com
); in such systems, each LED can be modulated at a distinct frequency and a multi-channel lock-in detection can separate the returns. Overall, lock-in amplification is essential for LED lidars – it enables usable range and SNR out of extremely weak sources that would be swamped by noise without narrowband detection.

## Raman Lidar Systems

Raman lidars detect the inelastically scattered light from molecules (e.g. N₂, O₂, H₂O), which is typically 4–6 orders of magnitude weaker than elastic backscatter. The weak Raman signals, especially in daytime, benefit greatly from lock-in techniques that reject background light. In early implementations (and some modern setups), a mechanical modulator (chopper) is placed in the optical path and the detector output is fed to a lock-in amplifier tuned to that modulation frequency​
ntrs.nasa.gov
​
ntrs.nasa.gov
. This was the case for a NASA Raman lidar developed for hydrogen leak detection: by modulating the signal and using a lock-in, the team could extract the hydrogen Raman signature from a high-noise background​
ntrs.nasa.gov
. The lock-in output (example shown in Figure 8 of the report) clearly revealed the H₂ Q-branch Raman peak at 652–656 nm​
ntrs.nasa.gov
. Without phase-sensitive detection, such a peak would have been buried in ambient light and fluorescence noise. The authors note that improvement in sensitivity and SNR was required for low concentrations, and the lock-in scheme was a key part of achieving that goal​
ntrs.nasa.gov
. In recent years, high-power pulsed lasers plus gated detectors (or photon counters) are commonly used for Raman lidars, often obviating the need for an analog lock-in. However, digital lock-in and filtering techniques are still employed to enhance Raman signal retrieval. For instance, Tang et al. (2019) introduced an intensity-modulation method to improve daytime Raman water vapor measurements, effectively using a software lock-in to filter out broadband sunlight (J. Instrum., 2019)​
researchgate.net
. Moreover, modern multi-channel Raman lidars (e.g. for multi-species detection) sometimes incorporate synchronous detection to separate overlapping return signals. As a general principle, “the lock-in amplifier can detect very weak signal from a relatively [strong] background” in Raman lidar applications​
sciencedirect.com
. This leads to better daytime operation and lower detection limits. In summary, while not every Raman lidar uses a lock-in amplifier, those that do report notable noise reduction and sensitivity gains, allowing detection of trace species (e.g. hydrogen, water vapor) in conditions that would otherwise be prohibitive.

## Doppler (Wind) Lidar Systems

Doppler lidars measure the frequency (or phase) shift of backscattered light due to motion, typically to retrieve wind speeds. The coherent Doppler lidar architecture, which mixes the return signal with a local oscillator (LO) laser, is fundamentally a lock-in detection process at optical frequencies. The photomixing produces a beat note at the difference (Doppler) frequency, and by amplifying and band-pass filtering around that beat, the system achieves extraordinary sensitivity to velocity-induced shifts. In the past decade, coherent Doppler lidars have pushed into regimes of detecting very weak molecular backscatter and far-range winds by leveraging this principle. For example, Baidar et al. (2022) demonstrated that heterodyne detection can be used not only for wind speed and uncalibrated aerosol returns, but even for quantitative molecular backscatter and extinction measurements, which require much higher sensitivity​
pubmed.ncbi.nlm.nih.gov
. In other words, lock-in-based coherent receivers have extended Doppler lidar capabilities to perform tasks traditionally done by high-power direct-detection systems​
pubmed.ncbi.nlm.nih.gov
. This extension directly ties to SNR improvement – heterodyne detection approaches the shot-noise limit and rejects broadband noise, allowing longer range and higher resolution wind profiling. Lock-in amplifiers also appear in the signal processing of Doppler lidars. A 2023 mid-IR heterodyne lidar experiment (MIR wind sensing) used a high-speed LIA to demodulate the beat signal. The system sent a 140 MHz phase modulation to the LO or transmitter and then demodulated the 140 MHz heterodyne beat in a lock-in amplifier (Zurich UHFLI), isolating the phase and amplitude quadratures of the Doppler signal​
arxiv.org
. By observing the in-phase (I) and quadrature (Q) outputs of the lock-in, the researchers could track real-time phase shifts corresponding to wind-induced optical phase changes​
arxiv.org
. This two-channel lock-in detection is analogous to a quadrature mixer in radar and provides robust rejection of noise outside a few kHz around the 140 MHz reference​
arxiv.org
. The result was precise measurement of both amplitude and phase modulation on the beam, demonstrating how lock-in detection enables simultaneous wind speed (phase) and intensity measurements in a coherent lidar​
arxiv.org
. It’s worth noting that advanced variations of coherent detection have been proposed to further enhance sensitivity. One concept is dual-signal heterodyne lock-in amplification, where two signal beams are mixed with one LO, yielding two beat notes; the lock-in then detects at the difference of those intermediate frequencies. Theoretical work showed this can drastically lower the noise-equivalent power compared to conventional single-signal heterodyne​
link.springer.com
. While this particular scheme (published in 2006) lies just outside our 10-year window, it has influenced modern designs aiming to maximize SNR for space-borne coherent lidars. In summary, Doppler lidars from 2015–2025 have capitalized on lock-in principles mainly through heterodyne receivers, achieving higher SNR, longer range, and even new measurement quantities (e.g. aerosol backscatter coefficients) that were not feasible with earlier technology​
pubmed.ncbi.nlm.nih.gov
.

## Differential Absorption Lidar (DIAL) and Gas Sensing

Differential Absorption Lidar (DIAL) systems probe atmospheric gases by sending laser pulses at two wavelengths (on-line and off-line) and comparing their attenuation. Because the differential signal (due to absorption) is often small, especially over long paths, lock-in amplifiers and related techniques are extensively used to improve gas detection sensitivity. A common approach in the last decade is to apply wavelength modulation spectroscopy (WMS) to DIAL: instead of simple on/off pulses, the transmitter wavelength is rapidly dithered or modulated around the absorption feature, and a harmonic of the modulation (usually 2ƒ) is detected by a lock-in amplifier. This yields a dispersion-like signal that is proportional to gas concentration but largely immune to baseline noise. For instance, Zhang et al. (2020) modulated an interband cascade laser at 3.93 µm for open-path N₂O detection and used a software lock-in to retrieve 1ƒ and 2ƒ signals simultaneously​
cpb.iphy.ac.cn
. The rising edge of their scan waveform was demodulated to give a 2ƒ signal (for sensitive detection), while the falling edge (no modulation) yielded a direct absorption measurement​
cpb.iphy.ac.cn
. By comparing these, they could quantify N₂O with high confidence. The lock-in-based 2ƒ channel provided better signal-to-noise under low-pressure and low-concentration conditions than direct absorption, enabling detection of N₂O in the ppb range that would otherwise require a much longer path or higher power​
cpb.iphy.ac.cn
. Essentially, the lock-in amplified harmonic signal boosted the SNR by rejecting laser intensity fluctuations and 1/f noise, focusing only on the narrowband modulation imprint of the gas. Another notable development is the use of digital lock-in amplifiers (DLIAs) embedded in software or FPGA for multi-species DIAL. Liu et al. (2020) built a hybrid NIR/MIR sensor for CO, N₂O, and CH₄ that combined two lasers into one path​
pubmed.ncbi.nlm.nih.gov
. Rather than time-sharing the measurement, both lasers operated simultaneously, each with its own sinusoidal modulation. A LabVIEW-based DLIA algorithm running on a PC demodulated the photodetector signal at the two modulation frequencies (and at 2ƒ for each) in real time​
pubmed.ncbi.nlm.nih.gov
. This enabled simultaneous detection of three gases without crosstalk. The use of lock-in detection was crucial to achieve sensitivities of ~5 ppb for N₂O and ~6 ppb for CO in 1 s, improved further to sub-ppb at 15 min averaging​
pubmed.ncbi.nlm.nih.gov
. Such low detection limits are on par with laboratory FTIR instruments, demonstrating how LIAs elevate DIAL performance to new heights. The authors report that the DLIA made the system more compact and flexible (no bulky hardware lock-in), and by optimizing the integration time they attained the best trade-off between sensitivity and response time​
pubmed.ncbi.nlm.nih.gov
. Field-deployed DIAL systems also employ lock-in techniques to contend with ambient noise. Siozos et al. (2022) developed an autonomous CO₂/CH₄ IPDA (Integrated Path DIAL) for greenhouse gas monitoring. In their design, each laser is sent out continuously but chopped at 400 Hz, and the receiver’s photodiode is fed into a dual-phase digital lock-in referenced to that chopper​
pdfs.semanticscholar.org
​
pdfs.semanticscholar.org
. Because sky background and solar radiation are unmodulated (DC or very low-frequency), the lock-in outputs represent only the modulated laser returns. This gave the system a huge advantage: “The lock-in amplifier used in [the] IPDA device extracts the weak signal from the reflected light and rejects the background signal from daylight… the device can operate continuously throughout the day.”​
pdfs.semanticscholar.org
. In fact, their instrument demonstrated stable operation over 18 months outdoors, retrieving CO₂ and CH₄ concentrations over a 0.1–10 km range even in full sunlight​
pdfs.semanticscholar.org
​
pdfs.semanticscholar.org
. The lock-in integration time was set to 1 s, much longer than the 2.5 ms chopper period, to maximize sensitivity for the weak absorption signals​
pdfs.semanticscholar.org
. By carefully tuning the time constant and laser modulation ramp, they avoided distortion of the gas absorption line while still smoothing out noise. This is a clear example of how lock-in amplification extends the range and usability of DIAL – enabling long-path greenhouse gas measurements with high SNR in daytime, which would be nearly impossible by direct detection (the sunlight background would overwhelm the tiny absorption difference).

## Conclusion

Over 2015–2025, lock-in amplifiers have become an indispensable tool in atmospheric lidar, improving performance across nearly all system types. By confining detection to a narrow band around a known frequency, LIAs dramatically reduce noise and increase sensitivity. Key impacts include:
Noise Reduction: Phase-sensitive detection allows lidar signals to be extracted even under bright background conditions. For example, chopping and locking to a 400 Hz reference enabled continuous daytime CO₂/CH₄ DIAL measurements by filtering out sunlight​
pdfs.semanticscholar.org
. Similarly, an optical chopper + LIA in a visibility lidar suppressed ambient light, yielding accurate results under high-noise conditions​
researchgate.net
. This noise rejection extends to electronic noise as well – unwanted 1/f drifts are eliminated by AC-coupling the measurement to the modulation frequency.
SNR Enhancement: Lock-in techniques improve the effective SNR by orders of magnitude, allowing detection of extremely weak optical signals. In harmonic absorption lidar (WMS-DIAL), a 2ƒ lock-in channel can detect gas absorption down to parts-per-billion levels​
pubmed.ncbi.nlm.nih.gov
. In a hydrogen Raman lidar, the lock-in extracted a clear signal where a direct approach struggled with SNR​
ntrs.nasa.gov
​
ntrs.nasa.gov
. Coherent Doppler lidars, by virtue of heterodyne (lock-in) detection, achieve shot-noise-limited sensitivity – recent systems reported wind measurements with high SNR even from molecular (Rayleigh) scattering, which is a very weak return​
pubmed.ncbi.nlm.nih.gov
.
Range Extension: Improving sensitivity directly translates to longer measurable range. The LED mini-lidar, using high-frequency modulation and lock-in-style detection, reached hundreds of meters (up to ~0.5 km) whereas an LED without such detection might only reach a few tens of meters​
colab.ws
. For Doppler lidars, the high SNR afforded by heterodyne/lock-in reception has extended wind profiling to higher altitudes and farther distances (e.g. up to 30 km for aerosol winds) and even enabled airborne and spaceborne wind lidars where every photon counts. In IPDA, lock-in detection made it feasible to measure a 10 km path to a target with minimal averaging, effectively extending the range of the DIAL technique​
pdfs.semanticscholar.org
​
pdfs.semanticscholar.org
.
Precision and Stability: Lock-in amplifiers also improve the precision and long-term stability of lidar measurements. By referencing a stable frequency source, LIAs remove low-frequency wander and baseline offsets. The multi-gas sensor by Liu et al. showed ppb-level stability over two days, thanks in part to digital lock-in processing​
pubmed.ncbi.nlm.nih.gov
. In the CO₂ IPDA, the lock-in approach (combined with a stable reference cell for wavelength locking) enabled multi-month deployment with minimal recalibration​
pdfs.semanticscholar.org
. In essence, the technique provides a built-in calibration to zero (since only AC signals are passed), which is invaluable for maintaining data quality over time.
In conclusion, the academic literature from 2015–2025 demonstrates that incorporating lock-in amplifiers in atmospheric lidar systems markedly boosts their performance. Whether it is a low-cost LED ceilometer or a sophisticated Doppler wind lidar, the ability to modulate and synchronously detect the return signal leads to cleaner data and often allows measurements that would not be feasible otherwise. As lidar technology progresses, we see a trend toward software-based lock-in implementations and multi-frequency modulation schemes, which offer flexibility and compactness. Nevertheless, the core principle remains the same as in classical lock-in detection. By marrying modern lidar designs with lock-in amplifier techniques, researchers have achieved significant noise suppression, higher SNR, extended range, and improved detection of atmospheric constituents. These advancements solidify the lock-in amplifier’s role as a critical component in the evolution of high-sensitivity atmospheric lidar over the past decade​
pdfs.semanticscholar.org
​
pubmed.ncbi.nlm.nih.gov
.

### References:

The references below include selected academic publications from 2015–2025 that illustrate the use of lock-in amplifiers in various lidar systems and the resulting performance improvements:
Shiina, T. et al. (2014). LED mini-lidar as minimum setup. Proc. SPIE 9246 – Demonstration of a high-frequency modulated LED lidar for near-range atmospheric monitoring​
colab.ws
​
colab.ws
.
Li, Y. & Wang, Z. (2024). A Method Combining Mobile Transmissometer and Lidar for High Precision Measurement of Visibility. IEEE Photonics J. 16(4): 6000110 – Describes a mobile transmissometer with chopper and lock-in detection to suppress background optical noise​
researchgate.net
.
Zhang, J. et al. (2020). Atmospheric N₂O gas detection based on an inter-band cascade laser around 3.939 µm. Chin. Phys. B 29(1): 010704 – Utilizes wavelength modulation (2f detection) with a LabVIEW lock-in for open-path N₂O sensing​
cpb.iphy.ac.cn
.
Liu, N. et al. (2020). Simultaneous Detection of Multiple Atmospheric Components Using an NIR and MIR Laser Hybrid Gas Sensing System. ACS Sensors 5(11): 3607-3616 – Demonstrates a multi-gas sensor with digital lock-in amplifiers achieving sub-ppb sensitivities​
pubmed.ncbi.nlm.nih.gov
.
Siozos, P. et al. (2022). Autonomous Differential Absorption Laser Device for Remote Sensing of Atmospheric Greenhouse Gases. Remote Sens. 14(3): 460 – Describes an IPDA lidar with a 400 Hz optical chopper and lock-in detection enabling daytime operation for CO₂/CH₄ measurements​
pdfs.semanticscholar.org
​
pdfs.semanticscholar.org
.
NASA/Chen, Y. et al. (2018). Measurements of Atmospheric Water Vapor by a 1.316 μm Optical Fiber Laser Heterodyne Radiometer. Front. Phys. 10:835189 – Includes a chopping and lock-in scheme in a laser heterodyne setup for trace gas (H₂O) measurement​
frontiersin.org
​
frontiersin.org
.
Baidar, S. et al. (2021). Detection of molecular backscattering with a tapered fiber amplifier in a coherent lidar. Opt. Express 29 – Shows that coherent (heterodyne) lidars can measure calibrated backscatter/extinction, highlighting the high sensitivity of lock-in-based detection​
pubmed.ncbi.nlm.nih.gov
.
Lombard, L. et al. (2023). Heterodyne coherent detection of phase modulation in a mid-infrared unipolar device. Optica (in press; arXiv:2501.13206) – Utilizes a high-speed lock-in amplifier to demodulate a 140 MHz beat signal, enabling simultaneous phase and amplitude measurement in a MIR lidar experiment​
arxiv.org
.

# Atmospheric Species Detection with 450 nm Laser Diode Lidar

Laser diode–based lidar operating at **450 nm (blue light)** enables detection of several atmospheric constituents. This wavelength is particularly effective for **elastic backscatter** applications and offers limited capabilities for **Raman scattering** and **differential absorption**.

---

## ✅ 1. Aerosols (Particulate Matter)

- **Primary application**: Characterization of **aerosol backscatter and extinction profiles**.
- **How**: Elastic backscatter at 450 nm is strongly affected by **aerosol size and composition**.
- **Advantage**: Shorter wavelengths like 450 nm scatter more strongly (Rayleigh ∝ 1/λ⁴), ideal for **PM₂.₅**, **urban haze**, **dust**, **smoke**.
- **Use cases**: Air quality monitoring, pollution transport, volcanic plumes.

---

## ✅ 2. Clouds and Fog

- Used to detect **cloud base**, **thickness**, and **optical depth**.
- High sensitivity to water droplets makes 450 nm suitable for detecting thin clouds and fog layers.

---

## ✅ 3. Atmospheric Boundary Layer (ABL) Structure

- Tracks **mixing layer height**, **turbulence**, and **diurnal changes**.
- Aerosol and water droplet scattering reveals boundary layer dynamics.

---

## ⚠️ 4. Atmospheric Molecules via Raman Scattering

450 nm can generate **Raman shifts**, but with weak signal intensity. Potential targets:

- **Nitrogen (N₂)** – Raman shift ~2331 cm⁻¹ → returns at ~491 nm.
- **Oxygen (O₂)** and **Water Vapor (H₂O)** – detectable with high-sensitivity and narrow-band filters.

> ⚠️ **Note**: Raman lidar at 450 nm is feasible but challenging due to low signal levels.

---

## ⚠️ 5. Trace Gases via Differential Absorption Lidar (DIAL)

- **NO₂**: Weak absorption bands around 400–450 nm.
- **O₃ (Ozone)**: Absorbs in UV, slight tail near 450 nm.
- DIAL at this wavelength **may** detect NO₂ or HCHO with precision optics.

> ⚠️ **Note**: Most DIAL systems use UV (e.g., 355 nm) or IR wavelengths for better sensitivity.

---

## ❌ Not Ideal For:

- **CO₂**, **CH₄**, **H₂O vapor (via DIAL)** — These gases require **infrared** or **near-infrared** wavelengths (e.g., 820–940 nm, 1.38 µm).

---

## 📊 Summary Table

| Atmospheric Species / Property | Detectable at 450 nm? | Detection Mode         |
|-------------------------------|------------------------|------------------------|
| Aerosols (PM, dust, smoke)    | ✅ Yes                 | Elastic backscatter    |
| Clouds and fog                | ✅ Yes                 | Elastic backscatter    |
| Boundary layer structure      | ✅ Yes                 | Elastic backscatter    |
| NO₂                           | ⚠️ Limited            | DIAL (weak absorption) |
| N₂, O₂, H₂O (Raman)           | ⚠️ Challenging         | Raman scattering       |
| CO₂, CH₄, H₂O (via DIAL)      | ❌ No                  | IR-based DIAL only     |

---

## 🔧 Conclusion

If you're building a **450 nm laser diode–based atmospheric lidar**, it's best suited for:

- **Aerosol and boundary layer studies**
- **Cloud and fog profiling**
- Potentially **NO₂ detection** with precision optics

For gas detection and Raman spectroscopy, you may need high-sensitivity detectors, narrowband filters, and possibly higher-power sources.

---


