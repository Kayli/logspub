# embedded development notes

## basics

- bit vs baud [^2]
  - bit means logical level
  - baud means symbol on a physical level
    - e.g, physical signals that is transferred over the physical medium to convey the data bits
    - symbol can be one of several: voltage, frequency, or phase changes
    - symbol is decided by the physical nature of the medium
    - often used to quantify transmission speed, e.g 9600 bauds per second

- serial bus interfaces
  - i2c (eye-squared-c)
    - 2+1 wire
    - has a 7-bit address space (with a rarely used 10-bit extension)
    - speeds from arbitrary low to up to 5 Mbit/s in ultra-fast mode
    - max length: about 2 meters max

  - uart (universal async reciever transmitter)
    - 1+1 wire
  
  - rs232

  - can (controller area network bus)
    - max length 40 meters at 1 mbit/sec speed


## linux kernel embedded drivers [^1]

- gpio drivers and library allow not to write kernel drivers in most cases
  - allows you to control general-purpose io interfaces, e.g. sending 1 or 0 to dedicated pin
  - you write your device 'drivers' in userspace instead

- i2c-dev driver

- sysfs interface (deprecated)
  - makes information about various kernel subsystems, hardware devices, and device drivers 
    available in user space through virtual files
  - sysfs is a pseudo filesystem provided by the kernel 
    - is mounted under the /sys mount point
    - if it is not mounted during initialization, you can always mount it using the command
      > mount -t sysfs sysfs /sys
  - GPIO devices appear as part of sysfs
  - allows to control pulse-width modulation with most modern system-on-a-chip (socs)
    - duty cycle (pulse width), period (how often pulses are emitted)


## references

[^1]: https://www.youtube.com/watch?v=QIO2pJqMxjE
[^2]: https://stackoverflow.com/questions/20534417/what-is-the-difference-between-baud-rate-and-bit-rate
