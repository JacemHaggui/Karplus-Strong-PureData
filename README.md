# Karplus Strong Algorithm Implementation in PureData
![Final Project Overview](resources/Final%20Project.png)


# Sound Production:
To produce the sounds i am using an ADSR envelope applied to white noise.

- ADSR envelope:

![ADSR Envelope](resources/Pasted%20image%2020241220113117.png)
- Applied to White noise:

![White Noise](resources/Pasted%20image%2020241220113336.png)

# Karplus Strong
This produces a sound burst which is then passed to the Karplus Strong Algorithm section of the patch.
![Karplus Strong](resources/Pasted%20image%2020241220113244.png)
The burst is written to a buffer using delwrite~ (KARP is the name of the delay and 1000 is the maximum delay amount).

We then use delread~ to output the signal stored in the buffer with the delay it receives from from the keyboard (we'll get back to that later).

**The amount of delay is what defines the Pitch of the sound produced by the Karplus Strong Algorithm.**

We then dampen and apply a low pass filter to the dampened signal.
**The user can control the value of damping with a slider next to the keyboard.**
We then feed the output back into the loop by inputting it to delwrite~.

The custom effect i am using is the flanger effect.

This section controls whether or not the effect is active:
![Flanger Control](resources/Pasted%20image%2020241220123945.png)

# The Flanger Effect:

The flanger effect works by duplicating the audio signal, applying a variable delay (usually a short time, like 1-10 milliseconds), and gradually changing the delay amount. The delayed signal is then mixed back with the original signal, creating a "swooshing" or "jet plane" sound as the phases of the signals interact, causing constructive and destructive interference.

![Flanger Diagram](resources/Pasted%20image%2020241220123033.png)
The implementation in PureData is as follows:
![Flanger Implementation](resources/Pasted%20image%2020241220130323.png)

The user can turn on and control the intensity of the effect using a toggle and a knob.
![Flanger Controls](resources/Pasted%20image%2020241220130027.png)

# The Keyboard:

![Keyboard Layout](resources/Pasted%20image%2020241220125304.png)
I created a piano keyboard in Pure Data where each key is linked to a "bang" corresponding to a specific MIDI number.
This MIDI number is then converted into a delay value that determines the pitch of the note.
![MIDI Conversion](resources/Pasted%20image%2020241220125912.png)

The delay is fed into the Karplus Strong algorithm, which simulates the sound of a plucked string by processing the delay with feedback and a short noise burst.

The keyboard can be controlled using the laptop's QWERTY keyboard, allowing for easy interaction. This setup generates the appropriate sound for each note.
