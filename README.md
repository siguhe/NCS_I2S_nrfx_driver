# NCS I2S nrfx driver example
NCS tag: v1.3.0
Mostly tested on nRF5340DK.

Inspiration from this Devzone comment: https://devzone.nordicsemi.com/f/nordic-q-a/60444/adafruit-i2s-mems-microphone-breakout-with-the-nrf9160-dk/251321#251321.


## NCS
The Secure Partition Manager(SPM) does not have I2S enabled as of 27 July 2020. Therefore, we must add it manually. The process is from [DevZone](https://devzone.nordicsemi.com/f/nordic-q-a/60444/adafruit-i2s-mems-microphone-breakout-with-the-nrf9160-dk/249997#249997), and explained, slightly different, below: 

Add to nrf/subsys/spm/Kconfig, inside the menu "Configure Non-Secure peripherals":
```
config SPM_NRF_I2S0_NS
	bool "I2S0 is Non-Secure"
	default y
```
Add to nrf/subsys/spm/spm.c:
```
#ifdef NRF_I2S0
        PERIPH("NRF_I2S0", NRF_I2S0, CONFIG_SPM_NRF_I2S0_NS),
#endif
```
