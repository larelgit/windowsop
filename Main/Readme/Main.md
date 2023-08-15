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

## Interrupt Affinity

Using Microsoft’s [Interrupt-Affinity Policy Tool](https://docs.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk) (backup link), you can set affinity for a driver’s interrupts. Do not go overboard as you can make the system perform worse if you randomly start changing affinities. Ideally, each device should have its own core or left alone if you have already dedicated your most important devices to every available core.

Changing the interrupt affinity of some drivers may prevent you from booting. If this is the case, use recovery mode to boot from the last known good configuration.

Default install dir: `“C:\Program Files (x86)\Microsoft Corporation\Interrupt Affinity Policy Tool”` (use the x64 executable)

### Steps to Configure Interrupt Affinity

1. Install Interrupt-Affinity Policy Tool, then run as an admin.
2. Open Device Manager and click “View” → ”Devices by connection”. Then expand all devices, as you will need this to see which devices are connected to which port/bridge.
3. If you open the properties of the device, it will show the location “PCI bus #, device #, function #,” you will need this in case multiple devices share the same name (e.g., two xHCI controllers, both named “USB xHCI Compliant Host Controller”)
4. Select a driver and click “Set Mask” (this is for `IrqPolicySpecifiedProcessors`).
5. Select the core you want the driver to be executed on.
6. If you have HT or SMT, use only one SMT sibling (i.e., CPUs 0/1 are SMT siblings, only use 0 or 1 but not both).
7. Press the “Advanced…” button for other choices (not useful unless you have drivers that use MSI-X or you have a multi-socket system).
8. Do not restart drivers for storage devices or root ports with storage devices attached, restart your PC instead to prevent the risk of data corruption.
9. Use xperf to see if the affinities have been set properly, see below for xperf script.
