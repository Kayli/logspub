# taking notes as i'm learning more about music synthesis

## basics

- oscillators
  - abbreviations: osc, vco, dco
  - parameters
    - waveform
    - pulse width
    - pulse width modulation (pwm)
  - main oscillator can have sub-oscillator

- filters

- envelopes
  - asdr
    - attack: time taken for initial run-up of level from nil to peak, beginning when the key is pressed
    - decay: time taken for the subsequent run down from the attack level to the designated sustain level
    - sustain: level during the main sequence of the sound's duration, until the key is released
    - release: time taken for the level to decay from the sustain level to zero after the key is released

- voltage controlled amplifier (VCA) 
  - used to creatively modulate signal's amplitude with some lfo/envelope

- wavetable sythesis
  - allows to morph between different single cycle waveforms
  - vector synthesis
    - morphing along multiple dimensions

- granular synthesis
  - short waveform sampled from longer sample
    - where its length is called 'grain window'
  - grain polyphony
    - number of grains instrument can play simultaneously
  - grain spray
    - how much you let the start point of a particular grain drift randomly 
      forwards and backward from the sample position
  - typical use
    - small amount of grain spray will freeze a single note in the pattern
    - large spray spread can reconstruct and freeze an entire chord

- direct box (di box) 
  - takes an unbalanced signal and turns it into a balanced one


## roland jd-xi synthesizer

- "legato switch" functionality removes "attack" from the second and following notes played legato style
- "portamento switch" pitch slides into the next note
  - mode "normal" pitch-slides from last played note into currently played one
  - mode "legato" pitch-slides from last legato-played note into currently played one

- glitchy behavior observed
  - noticed that portamento and legato were not working as expected
  - fixed by power-cycling synth


## interesting devices to consider

- zynthian [^1]
  - raspberrypi-based opensource synthesizer
- dart one [^2]
  - arduino-based opensource midi controller
  - there are nice demos on youtube [^3]


## references

[^1]: https://zynthian.org
[^2]: https://dartmobo.com 
[^3]: https://www.youtube.com/watch?v=xdUC7AnDaSQ
