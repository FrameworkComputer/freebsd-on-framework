# Hardware Interaction

## Battery Info

```
> acpiconf -i 0
Design capacity:        3572 mAh
Last full capacity:     2973 mAh
Technology:             secondary (rechargeable)
Design voltage:         15400 mV
Capacity (warn):        290 mAh
Capacity (low):         87 mAh
Cycle Count:            240
Measurement Accuracy:   0%
Max Sampling Time:      0 ms
Min Sampling Time:      0 ms
Max Average Interval:   0 ms
Min Average Interval:   0 ms
Low/warn granularity:   264 mAh
Warn/full granularity:  3780 mAh
Model number:           Framewo
Serial number:          027B
Type:                   LION
OEM info:               NVT
State:                  discharging
Remaining capacity:     59%
Remaining time:         1:32
Present rate:           1141 mA (17238 mW)
Present voltage:        15108 mV
```

## Lid, power button and suspending

```
# Current lid state
> sysctl dev.acpi_lid.0.state
dev.acpi_lid.0.state: 1

# Make system power off when pressing power button
> sudo sysctl hw.acpi.power_button_state S5

# Make system sleep when pressing power button
> sudo sysctl hw.acpi.power_button_state S3

# Ignore lid event (might be overridden by 
> sudo sysctl hw.acpi.power_button_state None

# Suspend via zzz
> zzz

# Manually suspend to S3 via acpiconf
> acpiconf -s 3
```

Custom actions on lid close: https://hauweele.net/~gawen/blog/?p=1420

## Temperature Sensors

```
> sysctl -a | grep temperature
hw.acpi.thermal.tz4.temperature: 38.9C
hw.acpi.thermal.tz3.temperature: 52.9C
hw.acpi.thermal.tz2.temperature: 57.9C
hw.acpi.thermal.tz1.temperature: 54.9C
hw.acpi.thermal.tz0.temperature: 64.9C
dev.cpu.19.temperature: 56.0C
dev.cpu.18.temperature: 58.0C
dev.cpu.17.temperature: 59.0C
dev.cpu.16.temperature: 59.0C
dev.cpu.15.temperature: 60.0C
dev.cpu.14.temperature: 61.0C
dev.cpu.13.temperature: 60.0C
dev.cpu.12.temperature: 62.0C
dev.cpu.11.temperature: 56.0C
dev.cpu.10.temperature: 57.0C
dev.cpu.9.temperature: 66.0C
dev.cpu.8.temperature: 66.0C
dev.cpu.7.temperature: 56.0C
dev.cpu.6.temperature: 57.0C
dev.cpu.5.temperature: 64.0C
dev.cpu.4.temperature: 62.0C
dev.cpu.3.temperature: 59.0C
dev.cpu.2.temperature: 58.0C
dev.cpu.1.temperature: 56.0C
dev.cpu.0.temperature: 57.0C
```
