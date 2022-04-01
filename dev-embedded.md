# embedded development notes

## basics

- bus interfaces
  - i2c: simple two wire serial bus
  - can (controller area network bus)



## linux kernel embedded drivers

- gpio drivers and library allow not to write kernel drivers in most cases [^7]
  - allows you to control general-purpose io interfaces, e.g. sending 1 or 0 to dedicated pin
  - you write your device 'drivers' in userspace instead

- i2c-dev driver

- sysfs interface (deprecated)
  - sysfs is a pseudo filesystem provided by the kernel 
  - makes information about various kernel subsystems, hardware devices, and device drivers 
    available in user space through virtual files
  - GPIO devices appear as part of sysfs
  - allows to control pulse-width modulation with most modern system-on-a-chip (socs)
    - duty cycle (pulse width), period (how often pulses are emitted)



## references

[^1]: https://www.youtube.com/watch?v=QIO2pJqMxjE
