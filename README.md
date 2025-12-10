# Hybrid-Gpu-Battery-Fix
A guide on various methods that could be used to ensure the dedicated gpu is not running when non intensive tasks are running.
---

## Warning ⚠️
Some of these methods could genuinely brick your software and even worse, hardware permanently so please use it with caution as i am not responsible for any damage.
I have decided to use ⚠️ symbols in the name of the method which has a high chance to cause problem and i will try to explain the possibility that might occur.

---

## Disclaimer
I do not own any softwares or any external links mentioned in this page so the credits belong to their respective owners.

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
- ![hwinfo start screen]()
- Select *sensors only* and press start
- scroll below till you find your graphics card
- Click on it's name if its details is not displayed immediately
- ![hwinfo sensor]()
- 


