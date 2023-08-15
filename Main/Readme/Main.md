# System Optimization 
Once you've reinstalled Windows and installed the necessary drivers, libraries, etc., you're ready to proceed with system optimization.
>As a safety measure, it's recommended to back up your system before making any changes. This could include screenshots, recovery points, or even photos taken with your phone – anything that could aid in system restoration if needed.
## 1. Disabling the HPET Timer

The High Precision Event Timer (HPET) can sometimes interfere with system performance. To disable it, follow these steps:

- Open the Command Prompt as an administrator.
- Copy and paste the following commands:
- `bcdedit /set disabledynamictick yes`
- `bcdedit /set useplatformtick yes`
- `bcdedit /set hypervisorlaunchtype off`

## 2. Optimizing Device Manager

The Device Manager is a useful tool for managing the hardware devices installed on your system. Here are some tips to optimize its use:

- Open the Device Manager by typing `devmgmt.msc` into the Run dialog box (Win + R).
- Carefully disable any hardware you're not currently using. Be cautious not to disable devices you need.
- Note: Uninstalling a driver via Device Manager usually results in it being reinstalled after a reboot. To completely disable a driver, it's better to disable it rather than uninstall it.
- When you disable a device in Device Manager, its driver is unloaded. This can free up CPU time as drivers can interrupt the CPU, causing potential system halts (stutters), especially with poorly programmed drivers.
- What to disable:
Display adapters:
Intel graphics (if you don’t use it, ideally should be disabled in the BIOS)
Network adapters:
All WAN miniports
Microsoft ISATAP Adapter
	Storage controllers:
Microsoft iSCSI Initiator
	System devices:
Composite Bus Enumerator
Intel Management Engine / AMD PSP
Intel SPI (flash) Controller
Microsoft GS Wavetable Synth
Microsoft Virtual Drive Enumerator (if not using virtual drives)
NDIS Virtual Network Adapter Enumerator
Remote Desktop Device Redirector Bus
SMBus
System speaker
Terminal Server Mouse/Keyboard drivers
UMBus
