# GPD Win Max 2 2023: System Hang Troubleshooting and Resolution

I recently encountered a series of intermittent system hangs on my GPD Win Max 2 2023. These freezes occurred regardless of the operating system installed or its installation state. Interestingly, the system tended to lock up when powered on with a charger connected, and more often during idle periods rather than under load. This issue persisted across multiple operating systems, including Windows, Ubuntu, Debian, and Deepin.

## Initial Troubleshooting Steps

I initially attempted to resolve the issue by resetting the BIOS to default settings multiple times, both through the GUI and via the CMOS clear button. However, these actions had no effect. 

Suspecting a memory issue, I ran memtestx86+ several times at different frequencies. However, this also failed to resolve the problem. (Note: A frequency of 7500MT/s would cause the machine to lock up, so I avoided this setting.)

After contacting Support, I was advised to update the firmware. Consequently, I reinstalled the 0.35 BIOS version (the version originally installed on the system). Despite flashing the BIOS and the controller firmware, the system continued to lock up after rebooting.

## Further Troubleshooting and Resolution

At this juncture, I was considering requesting a manufacturer warranty replacement. However, I decided to experiment with the BIOS power configurations first, to rule out any software issues that I might be able to rectify.

After unsuccessfully adjusting the CPU power settings, I decided to change several settings simultaneously as a last resort. To my surprise, this resolved the issue, and I no longer experienced system hangs.

Here are the configurations I modified:

```
Advanced (Standard advanced tab)
- GFX Configuration
  - iGPU Configuration: [UMA_SPECIFIED]
  - UMA Frame buffer Size: [6G]
- OCU Link Configuration
  - OCU Link Speed: [GEN4]

Advanced (Actual advance mode tab)
- PCI Devices Common Settings
  - PCI Express Settings
    - Relaxed Ordering: [Disabled] - This has since been reverted to Enabled, the system appears to be stable.
    - Extended Tag: [Enabled]
    - Extended Synch: [Enabled]
    - Unpopulated Links: [Disabled]
  - PCI Hot-Plug Settings
    - BIOS Hot-Plug Support: [Disabled]
```

I have yet to isolate the specific setting responsible for the issue. However, I can confirm that disabling 'Unpopulated Links' alone did not resolve the problem.

## Additional Benefits

An unexpected benefit of this solution was that it also resolved the s2idle sleep issues I was experiencing with Linux. Following the application of this solution and a fresh installation of Debian, the system now enters and exits sleep mode as expected, without any interruptions.
