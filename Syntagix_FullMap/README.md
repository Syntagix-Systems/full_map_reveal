# Syntagix_FullMap

Created by **Syntagix Systems**

Hide the map fog without having to travel the entire map.

## How it works

Syntagix_FullMap hides the discovery fog on the GTA V Legacy map and radar. It makes the map visible without requiring you to visit every area. The plugin becomes active as soon as RAGE Plugin Hook loads it. No key press or LSPDFR duty status is required.

It reapplies `SET_MINIMAP_HIDE_FOW(true)` on every RPH tick, including while the pause menu is open, to maintain the effect after map resets. It does not edit save files, trigger a save, or call coordinate discovery functions. Normal exploration still progresses through gameplay; displaying the entire map does not grant 100% discovery progress.

The plugin does not unlock mission-related icons or add map textures for unsupported areas. No configuration file is required.

## Requirements

- **GTA V Legacy for 64-bit Windows PC**.
- A working installation of **RAGE Plugin Hook compatible with your game version**.
- **.NET Framework 4.7.2 or later**. This means .NET Framework, rather than .NET 8, 9, or 10.
- LSPDFR if you want to play with LSPDFR. This plugin itself does not depend on the LSPDFR API.

ScriptHookVDotNet and RAGENativeUI are not required. GTA V Enhanced has not been validated. Intended for Story Mode with RPH.

## Installation

1. Close GTA V.
2. If you installed the previous version, remove **FullMap.dll** from the Plugins folder and deselect its old startup entry in RPH. Keep only one version installed.
3. Extract the archive. Copy **Plugins\Syntagix_FullMap.dll** into the **Plugins** folder of your GTA V Legacy installation. The Plugins folder belongs in the game directory containing GTA5.exe and RagePluginHook.exe.

```text
GTA V Legacy\
  GTA5.exe
  RagePluginHook.exe
  Plugins\
    Syntagix_FullMap.dll
```

Do not place the DLL in Plugins\LSPDFR or scripts. If you use a separate mod staging folder or injection tool, make sure the DLL is ultimately deployed to the Plugins folder of the game installation you launch.

4. Open the RAGE Plugin Hook settings (hold Shift while launching RPH if needed).
5. Under **Plugins**, select **Syntagix_FullMap.dll** for loading at startup, keeping your other plugin selections.
6. Launch Story Mode through RagePluginHook.exe and open the map to check the result.

To load the plugin manually during a session, open the RPH console (F4 by default) and enter:

```text
LoadPlugin Syntagix_FullMap.dll
```

## Disabling and uninstalling

To disable the plugin during a session:

```text
UnloadPlugin Syntagix_FullMap.dll
```

Normal unloading sets the fog-hiding flag back to false. Fog may reappear over areas you have not actually explored. After a forced termination, quit and restart the game to reset the display.

To uninstall, close the game, deselect the plugin from RPH startup loading, and remove **Plugins\Syntagix_FullMap.dll**. No save restoration is needed.

## Troubleshooting

- **The plugin does not start:** check the Plugins folder of the game installation you actually launch and your RPH startup selection. RagePluginHook.log may contain `[Syntagix_FullMap] Active`.
- **Fog remains visible:** check that the plugin is loaded and that another mod is not controlling the same map flag.
- **Loading error:** check compatibility between GTA V and RPH, and make sure .NET Framework 4.7.2 or later is installed.
- **Conflict with another map mod:** avoid plugins that simultaneously force the opposite flag value. Unloading this plugin sets the flag to false; it does not restore another mod's previous state.

## Source code and compilation

Source files are included in **Source**. The supplied DLL was compiled successfully for **x64** against the **RagePluginHook 1.124.0 SDK reference**, using the available .NET Framework compiler. It has not been tested in game here. Technical references are listed in VERIFICATION.md.

To rebuild using Visual Studio 2022 or Build Tools 2022, install the **.NET desktop development** workload and the **.NET Framework 4.7.2 SDK and targeting pack**. Place the SDK reference RagePluginHook.dll in **Source\lib**. It is available through the [RagePluginHook 1.124.0 NuGet package](https://www.nuget.org/packages/RagePluginHook/1.124.0). This reference is not bundled with this release and does not need to be installed in the game.

From the Source folder, run the following in Developer PowerShell for VS 2022:

```powershell
msbuild .\Syntagix_FullMap.csproj /t:Rebuild /p:Configuration=Release /p:Platform=x64
```

Output: **Source\bin\Release\Syntagix_FullMap.dll**. Do not rename RagePluginHook.exe to create an SDK DLL reference.
