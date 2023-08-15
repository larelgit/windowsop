# System Optimization 
Once you've reinstalled Windows and installed the necessary drivers, libraries, etc., you're ready to proceed with system optimization.
>As a safety measure, it's recommended to back up your system before making any changes. This could include screenshots, recovery points, or even photos taken with your phone – anything that could aid in system restoration if needed.
## 1. Disabling the HPET Timer

The High Precision Event Timer (HPET) can sometimes interfere with system performance. To disable it, follow these steps:

- Open the Command Prompt as an administrator.
- Copy and paste the following commands:
 `bcdedit /set disabledynamictick yes`
 `bcdedit /set useplatformtick yes`
 `bcdedit /set hypervisorlaunchtype off`

# 2. Device Manager Optimization

The Device Manager, a potent tool for supervising the hardware devices installed on your Windows system, can be wielded effectively for optimization. The following tips offer guidance on its optimal utilization:

1. Initiate the Device Manager by entering `devmgmt.msc` into the Run dialog box (accessed with `Win + R`).

2. Wield caution as you deactivate any hardware currently idle. It is vital to ensure you don't inadvertently disable devices essential to your system's operation.

   > **Note:** Uninstalling a driver via Device Manager typically prompts its reinstallation post-reboot. To ensure its comprehensive deactivation, it is more efficacious to disable the driver rather than uninstalling it.

3. The deactivation of a device in Device Manager results in the unloading of its corresponding driver. This action potentially liberates CPU time, as drivers can interrupt CPU functionality resulting in prospective system pauses (designated as stutters), especially prevalent with poorly coded drivers.

Consider the following hardware for deactivation:

- Composite Bus Enumerator
- Intel Management Engine / AMD PSP
- Intel SPI (flash) Controller
- Microsoft GS Wavetable Synth
- Microsoft Virtual Drive Enumerator (deactivate only if virtual drives are unused)
- NDIS Virtual Network Adapter Enumerator
- Remote Desktop Device Redirector Bus
- SMBus
- System speaker
- Terminal Server Mouse/Keyboard drivers
- UMBus
- Intel Graphics

Bear in mind, this list is not exhaustive and the deactivation of hardware should be done judiciously, considering the unique needs and setup of your individual system. Always ensure to have a stable system backup to revert any changes, if necessary.
