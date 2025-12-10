# Hybrid-Gpu-Battery-Fix
A guide on various methods that could be used to ensure the dedicated gpu is not running when non intensive tasks are running.
---

## Warning ⚠️
Some of these methods could genuinely brick your software and even worse, hardware permanently so please use it with caution as i am not responsible for any damage.
I have decided to use ⚠️ symbols in the name of the method which has a high chance to cause problem and i will try to explain the possibility that might occur.

---

## Disclaimer
I do not own any softwares, softwares present in the image or any external links mentioned in this page so the credits belong to their respective owners.
Some of the images present here are from the web and they are clickable links to it's source
---

## Context
- Many laptops nowadays come with discrete gpu along with igpu to make it ready to go for various usage like gaming, video editing, CAD softwares etc.
- Due to negligence of proper knowledge or glitchy software, there is a chance that your discrete gpu is running even on battery and light tasks like chrome is being run.
- The dGPU might not be continuously on throughout your session but the periodic turning on of it can consume anywhere from an average of 4w to the max tgp(Worst case mostly won't happen) the instance it is on which can have a noticeable negative impact on the battery.
- If your laptop battery suddenly went down at some point of time, it might be because of dGPU turning on rather than actual battery degradation.
- In early 2025 I for my first time in life, excitedly bought a gaming laptop but due to glitchy software and lack of nvidia advanced optimus there were many times the discrete gpu suddenly went on and caused my rather excellent battery life that i got after some tweaking to become average and sometimes even mediocre.
- I spent several months testing various methods and have compiled a list of methods which atleast one of it should fix it.
  
---

## Prerequisites
- A laptop with dGPU and iGPU(check the manufacturers website and find if your laptop has discrete gpu, also check if the processor has igpu model mentioned in the processor website.
  [intel](https://www.intel.com/content/www/us/en/products/details/processors/core.html)
  [AMD](https://www.amd.com/en/products/processors/laptop/ryzen.html#specs)
   eg:- Amd ryzen 7435HS doesn't have an igpu but has a dGPU
- [HWINFO](https://www.hwinfo.com/download/) not owned by me, the [credits](https://www.hwinfo.com/licenses/) goes to the hwinfo team, it is used to check whether the dGPU is turning on or not.

---

## Testing
- Install hwinfo(free for non commercial use)
- Open hwinfo
 ![hwinfo_start screen]()
- Select *sensors only* and press start
- scroll below till you find your graphics card
- Click on it's name if its details is not displayed immediately
 ![hwinfo_sensor]()
- Pay attention to **current** column and **Gpu power** row
  If your laptop has nvidia optimus then it would be in nvidia hybrid mode so the gpu will turn on when the hwinfo app is opened for a split second to check the sensors so the non zero values in the average and max columns of the gpu power row is fine
- If the value in the **current** column and **Gpu power** row turns non zero periodically within 20s- 1min or stays non zero then there is a problem.
- If all values of the **gpu power** row like current, average, min, max are 0 then your laptop is probably using advance optimus or is in igpu only mode of mux
- Pay attention to these values when applying the below mentioned methods
- Also try to test these while apps like chrome or spotify (light apps that u use) are open so it can be a test based on real scenarios
- Do not check for these values if u have opened nvidia app or nvidia control panel windows (both running as background tasks are fine)
- Unless said otherwise all the below methods are independent of each other and might interfere with each other so don't try to combine them


---

## Test bench

- Hp omen xd0015AX
  AMD ryzen 7840HS
  RTX 4050
- Note: Many of the methods are universally applicable and if other laptops are referred then it is either from my experience of using my friends laptop or info that i encountered while going through the web

---

## Note
- Some of these methods are nvidia specific
- Laptops with both amd dGPU and iGPU should be able to easily control this using amd control panel

## Method 1 - Nvidia Advanced Optimus laptops

- It is basically a improved version of mux switch which retains the convenience of normal hybrid(nvidia optimus) mode which doesn't require restart.
- Nvidia optimus laptops can fully shut down the nvidia gpu based on the setting in the laptop specific control panel.
- Open your laptop control panel(eg- armoury crate for asus, omen gaming hub for hp, lenovo vantage for lenovo)
Note - non gaming laptops probably don't have these control panels so you might not find them.
[![Nvidia optimus](aorus)](https://jarrods.tech/how-to-turn-off-optimus-on-your-gaming-laptop/)
- Go to your graphics settings and use hybrid igpu, igpu only mode(mux setting), gpu eco mode
- This should ensure only the igpu is running

## Method 2 - Lenovo advanced optimus gaming laptops

- Lenovo laptops have a extremly useful mode called **hybrid auto**
- Basically it ensures that only the igpu will ever run when it is on battery power and the dGPU will turn on when plugged in
- Open lenovo vantage software
- Go to gpu working mode
  [![vantage_gpu]()](
- Select Hybrid auto mode

## Method 3 - Mux switch

- It is a physical hardware which is present on laptop which ensures that the laptop display either receives it's output from igpu or dgpu
- Here only 1 is on at the same time
[![mux_switch]()](https://beebom.com/what-is-mux-switch/))
- Go to your laptop control panel
- Select igpu or dGPU based on your usecase
- It would either ask for restart or you would have to manually do it for the effects to apply

## Method 4 - Hybrid mode (only nvidia optimus)

- Some laptops only have hybrid mode because of a physically direct link between the display and the dGPU
- In these laptops the dGPU is connected to the display through the iGPU
- Also the dGPU can never be **properly off** using hardware mechanism in the above mentioned methods and is purely software controlled 
![hybrid_mode]()
- For some of these laptop they might have iGPU only mode but it works by changing the bios setting( some laptop control pannel settings might have it)
- Go to your bios( check the bios key of the manufacturer in the internet)
- Select the igpu mode

## Method 5 Rollback the driver ⚠️

- Sometimes the battery issue is due to updating the graphics driver
- This is because the way the laptop manufacturer driver might change by nvidia driver version
- To solve this u either have to rollback using device manager or clean install using [ddu](https://www.guru3d.com/download/display-driver-uninstaller-download/)
and reinstall both the igpu and dgpu drivers from the laptop manufacturers website(not intel,amd,nvidia site)
- All credit of ddu goes to their respective team
- Also try to ensure your laptop drivers are in the latest version
- Warning - reinstalling the driver has to be properly done or it might lead to errors

## Method 6 - Nvidia control panel

- Nvidia control panel also can be used to decide the graphics card usage
- It is however recommended to use the laptop control panel as it is device specific and both might interfere with each other
- Open the nvidia control panel
- Go to **Manage 3D settings**
- Click the drop down column and select integrated graphic
![nvidia_ctrl_panel]()
- This basically sets all the apps to only use integrated graphics
- However the apps might override due to windows setting or the laptop control panel

## Method 7 - Windows graphics settings

- From windows 11, windows is supposed to manage the gfx usage
- This is the reason nvidia control panel setting might be overriden
- open settings
- navigate System -> Display -> Graphics
- now click on these apps and select power saving graphics
- Also manually add apps by clicking add apps and select power saving graphics

## Method 8 - Win_Global_Gpu

- All credit goes to the contributors of [win_global_gpu](https://github.com/machineonamission/win_global_gpu)
- This app is supposed to simplify the windows graphics settings in Method 7 by automate it
- If this doesn't work, remember to use ```win_global_gpu.exe reset``` before fully deleting it

## Method 9 - Windows Advance Graphics Settings ⚠️

- Hardware accelerate graphics scheduling and variable refresh rate were mentioned to be reasons for the dGPU to wake up
- open settings
- navigate System -> Display -> Graphics -> Advance Graphics Settings
- disable Hardware accelerate graphics scheduling and variable refresh rate
- Warning - Hardware accelerate graphics scheduling is used to reduce the cpu load and variable refresh rate is used to prevent jitters in gameplay so it is not recommended to turn off
## Method 10 - Windows reset ⚠️

- Windows reset essentially reinstalls windows
- By doing it we can remove all bloat and faulty software which might be the reason for the dGPU to turn on
- Warning - windows reset essentially deletes all the files in **C** drive so, have a proper backup and ensure that you research the internet for all the required drivers and sometimes newer version of the dGPU and iGPU might be the reason so u would have to use the dGPU and iGPU drivers from the laptop manufacturer

## Method 11 - Install Linux ⚠️

- Installing linux is a sure way to solve the dGPU turning on problem in optimus laptops
- Use something like [envycontrol](https://github.com/bayasdev/envycontrol) or [supergfxctl](https://wiki.archlinux.org/title/Supergfxctl)
(All the credit goes to their respective teams)
- Both of these change the initramfs and ensures that the dedicated gpu never turns on
- Install them based on their github steps and remember to use `integrated mode`
- 
### Warning for linux

- Although 2025 saw many linux improvements and people switching, it may not be viable for u
- First ensure that all apps are available for linux eg- adobe doesn't work, whatsapp only has website clients without calling feature.
- Some people may run windows virtual machine in linux but it is not practical due to laptop battery
- Before installing, ensure that you know all the steps or you might delete all the drives
- There also laptop specific problems like audio poor quality/not working, fan control errors etc. some of them might be fixable but only to the most techiest of techies. Also some problems like fan control can damage the laptop as my fan used to run at absurdly low speeds which is impossible in windows and can do permanent damage.

## Method 12 Nvprofileinspector ⚠️

- It is basically a tool used to alter the nvidia driver settings
- All it's credit goes to [Nvprofileinspector](https://github.com/Orbmu2k/nvidiaProfileInspector/releases) and it's team
- It can be used to change the nvidia driver settings which can't be normally changed to ideal values
- Note - Do not change the below given settings on nvidia advance optimus or mux switch laptops.
- Open the app
![nvprofileinspector]()
- Navigate to below mentioned settings and change the values in the drop down menu
```
Power Management - Mode = Adaptive
Enable Application for Optimus = SHIM_RENDERINGMODE_INTEGRATED
Optimus Flags for enabled Applications= SHIM_MCCOMPAT_INTEGRATED
```
- Click apply settings
- Note - do not open nvidia control panel and click apply settings as it might override your configuration
- Restart your pc
- Also reapply these settings after every nvidia driver update
- Warning - many of these settings can cause issues so be careful

## Method 13 Registry changes 

- Use alongside method 12
- These registries are supposed to disable nvidia gpu from turning on and to let the laptop manufacturer drivers to control the dGPU instead of nvidia driver conflict 

- click start + r
- type regedit
- Go to the folders specified in the path and add the dword with their corresponding values

```
1)Disable D3D Kernel Telemetry Polling

Path:
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\NVHybrid

Add DWORD:
DisableDxgKrnlD3DPerfTelemetry = 1

2)Enable Manual Power-Control Logic

Path:
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\NVHybrid

Add DWORD:
NvEnablePowerManagementControl = 1

3)Disable Implicit Sync

Path:
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global

Add DWORD:
EnableImplicitSync = 0
```
- Restart after completion
- Warning- changing registries can cause system wide issues so please research and be careful  
  
## Conclusion

- The first 4 methods are safe and occur due to lack of user knowledge
- Most issues are resolved by installing the laptop manufacturer drivers but the problem arises due to random software updates and the fact that newer games/apps need updated drivers

