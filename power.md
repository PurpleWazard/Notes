this file is going to have notes on how i reduce power consumption and prolong battery life.

--- 

first tool is intel-undervolt 

this is used to undervolt the cpu and have it use less power

this video does a good job explainng it https://www.youtube.com/watch?v=NYCgMqf_V9Y

the arch wiki also has a page https://wiki.archlinux.org/title/Undervolting_CPU

here is my config file `/etc/intel-undervolt.conf`
```
# Enable or Disable Triggers (elogind)
# Usage: enable [yes/no]

enable yes

# CPU Undervolting
# Usage: undervolt ${index} ${display_name} ${undervolt_value}
# Example: undervolt 2 'CPU Cache' -25.84

undervolt 0 'CPU' -200
undervolt 1 'GPU' -100
undervolt 2 'CPU Cache' -100
undervolt 3 'System Agent' -100
undervolt 4 'Analog I/O' -100

# Power Limits Alteration
# Usage: power ${domain} ${short_power_value} ${long_power_value}
# Power value: ${power}[/${time_window}][:enabled][:disabled]
# Domains: package
# Example: power package 45 35
# Example: power package 45/0.002 35/28
# Example: power package 45/0.002:disabled 35/28:enabled

# Critical Temperature Offset Alteration
# Usage: tjoffset ${temperature_offset}
# Example: tjoffset -20

# Energy Versus Performance Preference Switch
# Usage: hwphint ${mode} ${algorithm} ${load_hint} ${normal_hint}
# Hints: see energy_performance_available_preferences
# Modes: switch, force
# Load algorithm: load:${capture}:${threshold}
# Power algorithm: power[:${domain}:[gt/lt]:${value}[:[and/or]]...]
# Capture: single, multi
# Threshold: CPU usage threshold
# Domain: RAPL power domain, check with `intel-undervolt measure`
# Example: hwphint force load:single:0.8 performance balance_performance
# Example: hwphint switch power:core:gt:8 performance balance_performance

# Daemon Update Interval
# Usage: interval ${interval_in_milliseconds}

interval 5000

# Daemon Actions
# Usage: daemon action[:option...]
# Actions: undervolt, power, tjoffset
# Options: once

daemon undervolt:once
daemon power
daemon tjoffset
```

install it
```
sudo pacman -S intel-undervolt
```

commands

```
sudo intel-undervolt read
sudo intel-undervolt apply
sudo intel-undervolt measure
```

next tool is auto-cpufreq https://github.com/AdnanHodzic/auto-cpufreq

install it from github or the aur or what ever distro your using

this does a whole bunch so read the readme. 

```
yay -S auto-cpufreq
sudo auto-cpufrep --install
```

here is my config for auto-cpufreq 
/etc/auto-cpufreq.conf

```
# settings for when connected to a power source
[charger]
# see available governors by running: cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors
# preferred governor.
governor = performance

# EPP: see available preferences by running: cat /sys/devices/system/cpu/cpu0/cpufreq/energy_performance_available_preferences
energy_performance_preference = performance

# minimum cpu frequency (in kHz)
# example: for 800 MHz = 800000 kHz --> scaling_min_freq = 800000
# see conversion info: https://www.rapidtables.com/convert/frequency/mhz-to-hz.html
# to use this feature, uncomment the following line and set the value accordingly
# scaling_min_freq = 800000

# maximum cpu frequency (in kHz)
# example: for 1GHz = 1000 MHz = 1000000 kHz -> scaling_max_freq = 1000000
# see conversion info: https://www.rapidtables.com/convert/frequency/mhz-to-hz.html
# to use this feature, uncomment the following line and set the value accordingly
# scaling_max_freq = 1000000

# turbo boost setting. possible values: always, auto, never
turbo = auto

# settings for when using battery power
[battery]
# see available governors by running: cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors
# preferred governor
governor = powersave

# EPP: see available preferences by running: cat /sys/devices/system/cpu/cpu0/cpufreq/energy_performance_available_preferences
energy_performance_preference = power

# minimum cpu frequency (in kHz)
# example: for 800 MHz = 800000 kHz --> scaling_min_freq = 800000
# see conversion info: https://www.rapidtables.com/convert/frequency/mhz-to-hz.html
# to use this feature, uncomment the following line and set the value accordingly
# scaling_min_freq = 800000

# maximum cpu frequency (in kHz)
# see conversion info: https://www.rapidtables.com/convert/frequency/mhz-to-hz.html
# example: for 1GHz = 1000 MHz = 1000000 kHz -> scaling_max_freq = 1000000
# to use this feature, uncomment the following line and set the value accordingly
# scaling_max_freq = 1000000

# turbo boost setting. possible values: always, auto, never
turbo = auto

# experimental

# Add battery charging threshold (currently only available to Lenovo)
# checkout README.md for more info

# enable thresholds true or false
enable_thresholds = true
#
# start threshold (0 is off ) can be 0-99
start_threshold = 80
#
# stop threshold (100 is off) can be 1-100
stop_threshold = 90
```

since i have a thinkpad t480 auto-cpufreq supports battery charge thresholds (i added that feature)
