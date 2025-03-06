

# Sound Production:
To produce the sounds i am using an [[ADSR]]  envelope applied to [[white noise]].

- ADSR envelope:

![[Pasted image 20241220113117.png]]
- Applied to White noise:
- 
![[Pasted image 20241220113336.png]]

# Karplus Strong
This produces a sound burst which is then passed to the [[Karplus Strong Algorithm]] section of the patch.
![[Pasted image 20241220113244.png]]
The burst is written to a buffer using [[delwrite~]] (KARP is the name of the delay and 1000 is the maximum delay amount).

We then use [[delread~]] to output the signal stored in the buffer with the delay it receives from from the keyboard (we'll get back to that later).

==The amount of delay is what defines the [[Pitch]] of the sound produced by the [[Karplus Strong Algorithm]].==

We then dampen and apply a low pass filter to the dampened signal.
==The user can control the value of damping with a slider next to the keyboard.==
 We then feed the output back into the loop by inputting it to [[delwrite~]] .

The custom effect i am using is the [[Flanger|flanger]] effect.

This section controls wether or not the effect is active:
![[Pasted image 20241220123945.png]]


# The Flanger Effect:

The [[Flanger|flanger]] effect works by duplicating the audio signal, applying a variable delay (usually a short time, like 1-10 milliseconds), and gradually changing the delay amount. The delayed signal is then mixed back with the original signal, creating a “swooshing” or “jet plane” sound as the phases of the signals interact, causing constructive and destructive interference.

![[Pasted image 20241220123033.png]]
The implementation in PureData is as follows:
![[Pasted image 20241220130323.png]]

The user can turn on and control the intensity of the effect using a toggle and a knob.
![[Pasted image 20241220130027.png]]

# The Keyboard:

![[Pasted image 20241220125304.png]]
I created a piano keyboard in Pure Data where each key is linked to a “bang” corresponding to a specific [[MIDI]] number.
This MIDI number is then converted into a delay value that determines the pitch of the note.
![[Pasted image 20241220125912.png]]

The delay is fed into the Karplus Strong algorithm, which simulates the sound of a plucked string by processing the delay with feedback and a short noise burst.

The keyboard can be controlled using the laptop’s QWERTY keyboard, allowing for easy interaction. This setup generates the appropriate sound for each note.
