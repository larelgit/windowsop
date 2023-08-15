# System Optimization 
Once you've reinstalled Windows and installed the necessary drivers, libraries, etc., you're ready to proceed with system optimization.
>As a safety measure, it's recommended to back up your system before making any changes. This could include screenshots, recovery points, or even photos taken with your phone – anything that could aid in system restoration if needed.
## 1. Disabling the HPET Timer

The High Precision Event Timer (HPET) can sometimes interfere with system performance. To disable it, follow these steps:

- Open the Command Prompt as an administrator.
- Copy and paste the following commands:
```
 bcdedit /set disabledynamictick yes
 bcdedit /set useplatformtick yes
 bcdedit /set hypervisorlaunchtype off
```

## 2. Device Manager Optimization

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

![Untitled-2](https://github.com/larelgit/windowsop/assets/67206438/db5d75fe-9238-42ad-a44b-3351fb280fec)

Bear in mind, this list is not exhaustive and the deactivation of hardware should be done judiciously, considering the unique needs and setup of your individual system. Always ensure to have a stable system backup to revert any changes, if necessary.

## 3. Removing Superfluous Programs

To enhance the efficiency of your Windows environment, it's beneficial to remove unnecessary programs.

You need to run PowerShell as an administrator.

Once you've opened PowerShell as an administrator, you can run the following commands. These commands use the `Get-AppxPackage` cmdlet to find packages for specific apps installed for all users (`-allusers`), then pipe (`|`) those packages to the `Remove-AppxPackage` cmdlet, which removes them:
```
Get-AppxPackage -allusers Disney.37853FC22B2CE | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.549981C3F5F10 | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.BingNews | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.BingWeather | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.GetHelp | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.Getstarted | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.MSPaint | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.Microsoft3DViewer | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.MicrosoftOfficeHub | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.MicrosoftSolitaireCollection | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.MicrosoftStickyNotes | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.MixedReality.Portal | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.Office.OneNote | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.OneDriveSync | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.People | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.PowerAutomateDesktop | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.ScreenSketch | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.SkypeApp | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.Todos | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.Wallet | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.WindowsAlarms | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.WindowsCalculator | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.WindowsCamera | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.WindowsFeedbackHub | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.WindowsMaps | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.WindowsSoundRecorder | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.YourPhone | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.ZuneMusic | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.ZuneVideo | Remove-AppxPackage
Get-AppxPackage -allusers MicrosoftCorporationII.QuickAssist | Remove-AppxPackage
Get-AppxPackage -allusers MicrosoftTeams | Remove-AppxPackage
Get-AppxPackage -allusers MicrosoftWindows.Client.WebExperience | Remove-AppxPackage
Get-AppxPackage -allusers SpotifyAB.SpotifyMusic | Remove-AppxPackage
Get-AppxPackage -allusers Microsoft.WindowsCommunicationsApps | Remove-AppxPackage
C:\Windows\SysWOW64\OneDriveSetup.exe -uninstall
C:\Users\Administrator\AppData\Local\Microsoft\OneDrive\22.012.0117.0003\OneDriveSetup.exe /uninstall
Get-WindowsPackage -Online | Where PackageName -like *Hello-Face* | Remove-WindowsPackage -Online -NoRestart
Get-WindowsPackage -Online | Where PackageName -like *QuickAssist* | Remove-WindowsPackage -Online -NoRestart
```

For ease of use, you can also download and run the file located in the Optimization folder. This file contains all these commands, allowing you to remove the programs with a single click.

## 4. Interrupt Affinity

Optimizing your Windows system involves manipulating the Interrupt Affinity of your drivers. This guide will take you through the process using Microsoft’s Interrupt-Affinity Policy Tool.

> **Note:** Be cautious not to overdo setting affinities, as it can degrade your system performance if done incorrectly. A good rule of thumb is to assign each device its own core, or leave them alone if your most important devices are already assigned to all available cores.

> **Warning:** Changing the interrupt affinity of some drivers may prevent your system from booting. If this happens, boot in recovery mode to revert to the last known good configuration.

### Installation

The default installation directory is: `C:\Program Files (x86)\Microsoft Corporation\Interrupt Affinity Policy Tool` (use the x64 executable).

1. Install the Interrupt-Affinity Policy Tool, then run as administrator.
2. Open Device Manager and navigate to `View > Devices by connection`. Expand all devices to see which devices are connected to which port/bridge.
3. For each device, open its properties to view the location in the format: `“PCI bus #, device #, function #”`. This information is crucial when dealing with devices that share the same name (e.g., two xHCI controllers, both named `“USB xHCI Compliant Host Controller”`).

### Setting Affinity

1. Select a driver and click `Set Mask`. This is for `IrqPolicySpecifiedProcessors`.
2. Select the core you want the driver to execute on.
3. If you have Hyper-Threading (HT) or Simultaneous Multithreading (SMT), use only one SMT sibling (i.e. CPUs 0/1 are SMT siblings, only use 0 or 1 but not both).
4. Press the `Advanced...` button for more options. This is not typically necessary unless you have drivers that use MSI-X or you have a multi-socket system.
5. Do not restart drivers for storage devices or root ports with storage devices attached. Instead, restart your PC to prevent the risk of data corruption.

### Special Cases

Non-MSI-X drivers perform best when their affinity is set to a single core (`IrqPolicySpecifiedProcessors`). If a device uses MSI-X, it will use `IRQPolicySpreadMessagesAcrossAllCores` by design, regardless of the affinity you set. To force an MSI-X device to a specific core, you must set its message limit to 1 via MSI Util. Remember to reset the affinity every time you update a driver (such as your GPU driver).

#### Examples of devices to change:

- **GPU**: Setting the graphics card to a single core gives the best performance, but setting it to a busy core will degrade performance. Determine the optimal core through benchmarking.
- **USB controllers (xHCI/EHCI)**
- **Audio controllers**: This does not apply to USB audio devices; change USB controller interrupt affinity instead.
- **Network controller**: When using RSS, set to `IrqPolicySpreadMessagesAcrossAllProcessors`. Also, change `RssBaseCpu` as interrupts will always land on the `RssBaseCpu` first, then each consecutive CPU (depending on how many RSS CPUs). You can change `RssBaseCpu` via the GUI from Device Manager under your network adapter’s properties. If the setting is unavailable, create a dword using `regedit` called `“RssBaseCpu" under `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Ndis\Parameters`, then enter the number for the corresponding CPU (e.g., 3).
  
![Untitled-1](https://github.com/larelgit/windowsop/assets/67206438/9f9c8eae-82be-4c5a-a3c4-3e1506f145f9)

## 5. Disabling Processor Idle States

By disabling idle, you can force your processor to run at maximum clocks. This is particularly helpful if you have a locked CPU that does not support overclocking (mostly Intel non-K SKUs). If you have a static all-core overclock, this step can be skipped. However, your CPU will only be running at C1 and not C0, which is the state where the CPU is fully responsive. Disabling idle helps minimize jitter and latency caused by your CPU constantly switching clocks and C-states. 

> **Note:** Disabling idle makes your processor run very warm, so it's essential to have adequate cooling. Do not disable idle if you have SMT/HT enabled as Windows puts the other logical processor of a core to sleep to prevent contention. On Windows 10, CPU usage will be displayed as 100% in Task Manager after disabling idle states.

### To do:
 - Run CMD as an administrator:

    ```
    powercfg -attributes SUB_PROCESSOR 5d76a2ca-e8c0-402f-a133-2158492d58ad -ATTRIB_HIDE
    ```

## 6. Disabling Hibernation

If the computer is stationary and hibernation mode will not be used, you can optimize disk space by disabling the hibernation file:
```
powercfg -h off
```

## 7. Intelligent standby list cleaner

### Configuration Steps

For proper configuration, set the following parameters:

- Start ISLC minimized and auto-Start monitoring: Enabled
- Launch ISLC on user login (TaskScheduler): Enabled
- Enable custom timer resolution: Enabled
- Wanted timer resolution: Set to 0.0ms
- Polling Rate (ms): 250

In ISLC, you can also configure system memory cache cleaning. To do this, adjust the parameter 'Free memory is lower than', which determines the minimum value of free memory. The optimal value is half the size of your system memory, after which the memory cache will be cleared. The parameter 'The list size is at least' determines the minimum size of cached memory. It's recommended to leave it at the default value of 1024MB.

> **Note:** To avoid additional micro-stutters when clearing the memory cache, especially if you have limited memory or if programs use it actively, it's recommended to test this setting with different parameters to find the optimal one for your specific use case.

After setting up, press 'Start' and verify whether the timer is fixed. The value of the 'Current timer resolution' should be strictly equal to 0.5ms and should not change. Note that the value may update with a delay!

![image](https://github.com/larelgit/windowsop/assets/67206438/0e8a98b0-1d6b-46ea-b7f0-39954f79a922)

> *Example of a correctly configured Intelligent Standby List Cleaner*
