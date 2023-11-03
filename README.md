# Digital-Comm-Lab-5
## Introduction
In this lab the emona-tims hardware and free online software that simulates the hardware were used to create three simulations of BPSK (Binary Phase Shift Keying), QPSK (Quadrature Phase Shift Keying), and QAM (Quadrature Amplitude Modulation). The BPSK uses two symbols each on the real axis to send information while the QPSK is a step up using four symbols on the real and imaginary axis (This can also be shifted by 45 degrees) thus sending more information at once. Taking even another step up to the QAM messing with the amplitudes of the symbols it is possible to densely pack information into a square with symbols taking up the area of that square with 16, 32, 64, etc. symbols. The best way to space these symbols for all of these modulation techniques is to make their phases equal thus spacing them the farthest apart from one another while keeping symmetry which allows the reciever to find only one symbol and sync the rest of them using the predetermined phase.

## BPSK (Binary Phase Shift Keying)
### Part A - Generating a BPSK Signal
![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/596e63be-35fb-405c-8bb4-42a88f3f52d2)

This is the block diagram used to generate a BPSK signal with the digital signal going to channel one of the oscilliscope and the BPSK signal going to channel two. The master signal inputs a 8kHz clock to the sequence generator and a 100kHz carrier signal that gets multiplied with this clock or digital signal to create the BPSK.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/f74d75b1-4815-4311-b4f9-9a16b931ffff)

This is the BPSK signal in the frequency spectrum in blue compared to the original digital signal in orange.

Question 1: What happens to the BPSK signal on the data stream's logic transitions?

The BPSK signal has a rippling effect on the data stream's logic transitions.

Question 2: What feature of the BPSK signal suggests that it's a DSBSC (Double Side Band Suppressed Carrier) signal?

Looking at the frequency spectrum the carriers have lower spikes than the sidebands indicating that the carrier is suppressed.

### Part B - Demodulating a BPSK signal using a product detector
![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/061f1ce9-1c6f-4737-9a8b-eb915f2bd700)

This is the block diagram used to recover the digital signal from the BPSK signal. This uses the generated BPSK signal multiplied with the "Stolen" local carrier and then gets passed through a low pass filter.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/9872f8bf-8182-4dd8-a839-f9c51b64bdc3)

This is the signal generated which is shown in blue compared to the original signal shown in orange. In the frequency spectrum it is visible where the low pass filter's cutoff frequency starts cutting off the square waves harmonics.

Question 3: Why is the recovered digital signal not a perfect copy of the original?

This is because of the aforementioned frequency spectrum where the cut off frequency is cutting off many of the original square waves harmonics.

Question 4: What can be used to "clean-up" the recovered digital signal?

Similar to the previous lab 4 the Schmitt trigger or in this case a comparator block.

### Part C - Restoring the recovered data using a comparator
![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/56a9d38a-b64d-4cc7-9dd8-def94ba62916)

This is the block diagram used clean up the recovered digital signal from the BPSK signal. This uses a comparater with a DC voltage as a reference set around the middle point of the square wave. This makes the transitions from digital 0-1 or vice versa much smoother.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/54fdd039-df24-4707-b093-4b19db97004e)

This is the recovered and cleaned up signal that is very similar to the original digital signal in both the time and frequency domains.

Question 5: Why does varying the DC voltage on the comparator's input change the shape of the digital signal?

This is because the DC voltage is used as a reference for when to change from a digital 0-1 or vice versa. Changing this voltage causes the transition to either happen too early or too late causing the signal to look different from the original which is why the DC voltage was set to around half of the square wave's amplitude.

### Part D - Adding Noise to the system
![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/e288c8f9-0faf-4d40-ace0-78e820274fa0)

This is the block diagram for adding noise into the system which replaces the multiplier module. This adds noise of either -20dBs, -6dBs, and 0dBs with 0dBs being the most amount of noise that can be added. All three of these noise levels were tested but only the 0dBs showed any significant change to the system showing that the BPSK is extremely immune to noise.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/59e33cbb-3ddb-47d0-b819-56566341276e)

This is the signal with -20dBs of noise which shows exactly the same waveform as in part C.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/12eaeb62-1ac0-4a00-84c0-d634d944a287)

This is the signal with -6dBs of noise which also shows the exact same waveform as in part C and with -20dBs of noise added.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/2caeea61-f56c-4e57-b45c-09d0b7edbec5)

This is the signal with 0dBs of noise which finally starts to show some spikes where there shouldn't be due to the amound of noise added.

## QPSK (Quadrature Phase Shift Keying)
### Part A - Generating a QPSK signal
![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/57a0ae66-a0eb-4e32-a54a-27e0d38482a4)

This is the block diagram for generating a QPSK signal with four symbols. Similar to the BPSK the Master Signals feeds an 8kHz wave to the clock of the sequence generator. The bit splitter splits the bits into even and odd bits each with two symbols for a total of four. The two channels are connected to the even and odd bit outputs to see the Q and the I waveforms separately.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/3c56388b-71a6-4e42-a50b-6a2a4fbab799)

This is the waveforms the the Q and I that were randomly generated by the sequency generator at a 8kHz clock. They are both square waves as shown in the time and frequency domains. The high and low of the I and Q each generate a symbol thus creating two symbols for the I and two symbols for the Q for a total of four symbols.

Question 1: What is the relationship between the bit rate of these two digital signals and the bit rate of the Sequence Generator module's output?

The data was put through a bit splitter thus halving the bit rate of the I and Q waves compared to the bit rate of the Sequence Generator module's output.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/c39c93ae-f995-4486-be5f-2e05af7098e8)

This is the block diagram used to modulate the data with a 100kHz carrier and shows the even bits on the first channel with the modulated output on the second channel. This same block diagram is used to see the odd bits on the first channel with the modulated output on the second channel.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/ad5f826f-1dae-43ee-a551-f2e1b19f9586)

This shows the original waveform for the even bits as the orange square wave and the modulated signal as the blue wave. It is visible that the blue wave's phase changes with reference to when the square wave changes from 0-1. The same can be done for the odd bits which will give a similar output showing the waveform's phase being changed with respect to the original square wave.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/a1afa23a-0ca5-40e0-a372-be47a6213132)

This shows a clearer picture of the frequency spectrum for this modulation which shows the carrier frequency around 100kHz with the side bands around it.

Question 2: What feature of the Multiplier's output suggests that it's a BPSK signal?

Similar to the BPSK example done previously in this lab the waveform is changing phase in accordance to when the square wave changes from 0-1 vice versa.

Question 3: What type of signal is present on the Multiplier's output?

It is either a sine or cosine wave depending on the whether it is the odd or even bit. This wave is not a normal sine/cosine wave because the phase is getting modulated with respect to the original square wave.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/0e8ab348-24c3-4777-b447-2cdb44a4738c)

This is the block diatram of the two modulated I and Q waveforms being added together to get a complete IQ waveform.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/db5e34c8-5994-4ca2-9a2e-4fd982bdc42d)

This shows the completely added IQ waveform which has a near constant envelope making it very good at negating the effects of noise.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/74db6b76-7ec8-4634-819f-3c7e6076865f)

This is another close up of the frequency spectrum which shows the carrier of the added signal around 100kHz similar to the previous waveform.

Question 4: According to the theory, what type of digital signal transmission is now present on the Adder's output?

The Adder's output is a complete IQ waveform that provides information for the real and imaginary parts of the message while still transmitting a completely real signal.

Question 5: Why is there only one sinewave when the QPSK signal is made up of two BPSK signals?

This is because both the I and Q waveforms are running at the same carrier frequency just out of phase with each other to make them orthogonal.

### Part B - Using phase discrimination to pick-out one of the QPSK signal's BPSK signals
![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/9d8c58cb-fd00-468f-89f4-c5670f8e59b3)

This is the block diagram which demodulates the signal. This block diagram was later replicated to see both the I and Q elements at the same time instead of doing them separately.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/58ce47ec-ac7a-4b0c-ba13-cf5ba2f2ba22)

This is the signal when the phase splitter's adjustable phase is set so that the output signal matches the best with the input signal.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/deea1823-70de-4f97-ad3a-5aa1d5d1dd40)

This is the signal when the phase splitter's adjustable phase is set so that the output signal has more levels than the input signal.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/013a4e23-4010-4e4d-a61b-e47d2a5021ec)

As mentioned previously this is the signal that shows both the I and Q elements and also shows the symbols in the constellation. Playing with the gains of the low-pass filters makes the symbols of each BPSK move closer and farther away from each other while playing with the cut off frequency changes the shape of the QPSK.

Question 6: What is the cause of the 3 and 4 level signals out of the Tuneable LPF during the phase adjustments above? How many different Phase Adjust control positions will give you a bipolar signal?

The cause of the 3 and 4 level signals is because there are mutliple symbols in the waveform. The different levels of voltage represent the different symbols of the I and Q. When there are only two levels is the signal a bipolar signal.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/6dadba7a-56c3-4390-8c6b-bc7a1d3395c2)

This is a slightly modified block diagram just adding a utilities module right after the low pass filter which is like the previous example of using a comparator to clean up the signal.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/d732df06-5f46-44c2-8d03-0b5b27e13ce7)

This is the output after the signal passes through the comparator which significantly cleans up the signal to look almost identical to the original input signal.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/4e45e33d-cc01-4d50-a0b1-873f5eae3071)

This is the output using the same block diagram but with the phase splitter shifting the phase so the output wave is 180 degrees out of phase.

Question 7: What is the present phase relationship between the local carrier and the carrier signals used to generate the PSK_I and PSK_Q signals?

Setting the phase shifter's phase change control to the 0 degree position gets the phase of the output to match the phase of the input.

Question 8: What is the new phase relationship between the local carrier and the carrier signals used to generate the PSK_I and the PSK_Q signals?

Setting the phase shifter's phase change control to the 180 degree position gets the phase of the output to be 180 degrees out of phase compared to the input.

Question 9: Why is your demodulator considered to be only one half of a full QPSK receiver?

This is because the current set up is only receiving either the I or the Q input and not both but the modules were later replicated and shown with noise in the system.

### Part C - Adding Noise into the system

This is not a part of the original lab and was done just to see how noise resistant the QPSK is compared to the BPSK and in the near future the QAM.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/f9c28980-a032-43a2-ab7f-7627b67dbdeb)

This is the system with -20dB's of noise and as shown this is not enough noise to disrupt the waveforms or the symbols generated.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/8f62807e-fe2f-4bcc-8d82-7054cff0b27f)

This is the system with -6dB's of noise and the waveform is starting to get noisy but the four symbols are still distinguishable.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/21291616-06e4-4e7a-b5c6-c55c6173e74c)

This is the system with 0dB's of noise and the waveform is very noisy and while the symbols are getting much noisier they are still distinguishable.

## QAM (Quadrature Amplitude Modulation)
### Part A - Generating a QAM signal
![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/db942883-f208-4d61-b575-6a99e3e1c737)

This is the block diagram used to generate a QAM signal. The top multiplier gives the I value and the bottom gives the Q value similar to the QPSK. The first channel is connected to the first message to compare to the first output.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/ee640585-0887-453d-8c74-254eff5978ad)

This is the output that shows the DSBSC of the first signal. The frequency domain shows that the carrier is suppressed more clearly than the time domain.

Question 1: What feature of the Multiplier module's output indicates that the signal is a DSBSC?

As noted above the frequency domain shows that the carrier spike is lower than the sidebands thus it is a DSBSC.

Question 2: Given the Multipliier module's inputs, how many significatn spectral components are there in the DSBSC_I signal and what are their frequencies?

The carrier frequency should be at 100kHz which is shown in the picture above and the sidbands should each be 1kHz away from the carrier.

Afterwards the same block diagram is used with the channel probes changing from the top blocks to the bottom.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/ececb03a-5637-407c-9aa2-7f093cef8204)

This is the waveform generated by the Q part of the QAM. This shows the carrier at 100kHz and the sidebands should be at 2kHz.

Question 3: Given the Multiplier module's inputs, how many significant spectral components are there in the DSBSC_Q signal and what are their frequencies?

As mentioned above the carrier frequency shoudl be around 100kHz and the sidebands should be 2kHz away.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/25b1f845-2c15-4a99-b181-a4ed44fbca80)

This is the new block diagram just adding the two I and Q components together to get one wave instead of two separate waves.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/483fda2d-deee-4e04-acd2-58688061ffd4)

This is the output of the two waves added together which is a mix of a 1kHz and a 2kHz wave.

Question 4: According to the theory, what type of signal is now present on the Adder's output?

According to the theory this waveform should be a amplitude modulated waveform or an AM signal.

Question 5: Given the spectral composition of the two DSBSC signals on the Adder module's inputs. what are the significant spectral components in the signal on its output?

The carrier frequency is the same for both at 100kHz and there should now be sidebands at 1kHz away and 2kHz away.

### Part B - Using phase discrimination to recover demodulate the QAM signal

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/9978a71e-f418-4284-b889-d17c23e1115d)

This is the block diagram used to recover one of the messages while rejecting the other message depending on the phase splitter and low pass filter's adjustable components.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/d68145f9-084f-4f80-b7c9-7c7fc605933d)

This is the recovered signal of the first message at 2kHz frequency. As shown in the picture the time domain shows the same 2kHz frequency as the original message.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/ed1f020d-915d-4dfd-bb9d-a067a05993e7)

This is the same waveform but the frequency spectrum is more visible showing that the 2kHz spikes are higher than the 1kHz spikes.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/c1826a9d-8581-462d-8e0c-f561a4346051)

This is the recovered signal of the second message at 1kHz frequency. As shown in the picture the time domain shows the 1kHz frequency as opposed to the orange 2kHz frequency waveform.

![image](https://github.com/blee0730/Digital-Comm-Lab-5/assets/130094173/2fe58532-10e5-4107-b3fe-39377f83a78f)

This is the same waveform but the frequency spectrum is more visible showing that the 1kHz spikes are higher than the 2kHz spikes.

Unfortunately due to the lack of proper modules it was not possible to see the QAM using constellations which would have shown multiple symbols with their amplitudes being modulated to create a square of symbols.
