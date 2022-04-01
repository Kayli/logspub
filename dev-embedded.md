# embedded development notes

## basics

- bus interfaces
  - i2c
  - can (controller area network bus)



## linux drivers
- gpio drivers and library allow not to write kernel drivers in most cases [^7]
  - allows you to control general-purpose io interfaces, e.g. sending 1 or 0 to dedicated pin
  - you write your device 'drivers' in userspace instead

- sysfs interface
- allows to control pulse-width modulation with most modern system-on-a-chip (socs)
    - duty cycle (pulse width), period (how often pulses are emitted)

- i2c

[^1]: https://www.youtube.com/watch?v=QIO2pJqMxjE
