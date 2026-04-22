### Testing Procedure
This guide provides a general outline of how testing should occur for the rail splitter, AB amplifier, and combination of the rail splitter and AB amplifier PCBs. 
The steps may vary depending on any modifications to the PCBs. No guide has been written for the rail follower at this point in time.

## Rail Splitter

# Setup
Prepare a variable DC power supply capable of 1V-95V which will be connected to input (Believed to be silkscreened J1/J3; confirm at meeting tmr)
Prepare an oscilloscope with standard probes and differential probe
Get a thermal camera

# Procedure
Connect the variable DC power supply to the main power input terminals, set to 1.0V with a strict current limit (100mA-500mA) to prevent failure if a short occurs
Connect channel 1 of the oscilloscope to the main control signal input (Probably TP5 or TP6, confirm at meeting)
Connect channel 2 and channel 3 to monitor the high side and the low side gate drive signals. Probe the test points directly next to the stitching ICs/MOSFETS (TP7, TP8, TP9, or TP10)
Connect the differential probe across the output rails of the splitter to measure the ripple
Probe TP12 (V+) and TP13(VCOM) to test the rail
Increase the voltage and check the control signals at the input stage to make sure they are stable
Verify the gate drive signals are clean and free of noise
Measure the ripple at different voltages (20V, 40V, etc.) and record the Vpp

## AB Amplifier

# Power Up
Setup
* Connect fixed supply rails, starting at 0V and slowly increasing
* Grounded input
* No load

1. Start supply rails at 0V and slowly increase to ±15 V
2. Measure quiescent supply current
3. Measure quiescent current at emitter resistors
4. Measure output DC offset with multimeter
5. Observe output on oscilloscope

Expected:
* Vout < 30 mV

# Small Signal Test
1. Apply 1 kHz sine wave, starting at 100mVpp
2. Observe output waveform on oscilloscope
3. Measure output amplitude
4. Vary rail voltage and record where clipping occurs
5. Change input to square wave
6. Check for crossover distortion, noise, etc.

Expected
* Clear sine waveform, clipping may occur at different rail voltages depending on the input
* No crossover distortion
* Minimal noise in square wave


# Frequency Response
Setup
* Fixed rails: ±10V
* Input: Sine wave
* No load, then 8Ω load

1. Apply sine wave with amplitude ~100 mV
2. Adjust input if needed
3. Sweep frequency at least 20 Hz - 20 kHz
4. At each frequency, measure Ratio FS 1->2 (RMS1/RMS2)
5. Calculate gain at each frequency
6. Generate a plot with data

Expected
* Gain around 26dB from 20 Hz to at least 20 kHz
* -3dB drop in gain some point after 20kHz (likely after 80kHz)

# Power Output
1. Set the power supply to ±20 V initially
2. Connect the 8Ω load to the output terminal
3. Apply 1 V amplitude sine wave
4. Gradually increase the power supply up to ± X V
5. Gradually increase amplitude, up to 2V if needed but ~100W should be achieved a little lower than that
6. Measure RMS output voltage on the oscilloscope
7. Measure output current

Expected
* ~100W with ±45 V rails at some input amplitude between XV and XV
* Stability


# Supply Rails
Setup
* Rails at ±15V, ±20V, ±25V, ±30V, ±45V
* Input: Sine wave initially at 1V amplitude
* 8Ω load

1. Set rails to starting level of ±15V
2. Apply sine wave, gradually increasing amplitude like test 3.4
3. Measure output voltage 
4. Record clipping if it occurs
5. Measure output power
6. Repeat for each rail level

Expected
* Clipping at lower rail voltages
* No clipping over 30 V rails


# Thermal
1. Connect the the output of the amplifier to 8Ω load
2. Supply ±V to rails
3. Configure input to sine wave, X Vpp, 1kHz frequency
4. Record temperatures of MJE and MJL transistors  after X minute with thermal camera
5. Repeat for different inputs and rails


# Total Harmonic Distortion
1. Connect the the output of the amplifier to 8Ω load
2. Supply  ±15 to rails
3. Configure input to sine wave, 0.5 Vpp, 1kHz frequency
4. Connect oscilloscope probe to output of amplifier
5. View FFT of output on oscilloscope
6. Use cursors to measure dBV at 1kHz, 2kHz, 3kHz, etc.
7. Record harmonic measurements and convert to VRMS
8. Calculate THD

Expected:
* THD < 5% if signal isn’t clipped
* Higher THD if signal is clipping
	

# Noise
1. Connect the the output of the amplifier to 8Ω load
2. Supply  ±15  to rails
3. Configure input to sine wave, 0.5 Vpp, 1kHz frequency
4. Select Limit Bandwidth on the oscilloscope
5. Measure RMS output voltage
6. Disconnect input signal
7. Measure RMS output voltage (noise) using AC coupling on oscilloscope
8. Calculate SNR
9. SNR = 20log10VsignalVnoise

Expected:
*SNR > 50 dB
*Noise on order of 3mV

# Efficiency
1. Measure supply power 
2. Measure output voltage (RMS)
3. Calculate output power:
		Pout= Vout(RMS)2/8 
4. Calculate input power:
    Pin= V+I++|V-||I-|
5. Calculate efficiency

## Rail Splitter and AB Amplifier Board

# Start Up
1. Set the DC power supply to 12 V
2. Set another power supply to 20V initially
3. Connect the 12 V supply to the + and GND terminals labeled 12V Input/Output
4. Connect the 20V supply to the + and - terminals labeled POWER INPUT
5. Connect an oscilloscope probe to the + of the OUTPUT terminal through the testpoint TP24 and connect the ground of the probe to TP25 (OUTPUT -).
6. Power on both power supplies
7. Observe the current draw from the supplies, very low current is expected (0.01 - 0.02 Amps)

# Low Rails, No Load
1. Keep the same setup as test 4.1, but additionally configure a signal generator to output a sine wave with 250 mVpp and 1kHz frequency
2. Connect the signal generator output to board
3. Turn on the power supplies
4. Turn on the output of the signal generator
5. Observe the current on the power supplies, it should still remain relatively low (<0.1A)
6. Lower the power supply for the rails until the output waveform no longer clips (~13-14V)
7. Measure the peak-to-peak voltage of the output waveform


## Full Class H Amplifier
Testing procedure will be similar to that of the AB amplifier but with differences in input connections. Details are not present due to lack of testing at this point in time.
