# Which devices have an ANE?

### [A11 Bionic](https://en.wikipedia.org/wiki/Apple_A11) (APL1072 / APL1W72)

The first Neural Engine. It has 2 cores and can perform up to 600 billion operations per second. However, this version of the Neural Engine cannot be used by Core ML. It's only used for tasks such as Face ID and Animoji. 

Devices: 

- iPhone 8 (2017)
- iPhone 8 Plus (2017)
- iPhone X (2017)

### [A12 Bionic](https://en.wikipedia.org/wiki/Apple_A12) (APL1081 / APL1W81)

The second generation of the Neural Engine, but the first version that can be used by Core ML (on iOS 12 and up).

This ANE has 8 cores and can perform up to 5 trillion operations per second. Apple claims that Core ML on the A12 is 9 times faster at 1/10th the energy usage compared to the A11.

Devices: 

- iPhone XS (2018)
- iPhone XS Max (2018)
- iPhone XR (2018)
- iPad (8th gen, 2020)
- iPad Air (3rd gen, 2019)
- iPad Mini (5th gen, 2019)

### [A12X Bionic](https://en.wikipedia.org/wiki/Apple_A12X) (APL1083)

This has the same Neural Engine as the A12. 

Devices: 

- iPad Pro 11-inch (1st gen, 2018)
- iPad Pro 12.9-inch (3rd gen, 2018)

### [A12Z Bionic](https://en.wikipedia.org/wiki/Apple_A12Z) (APL1083)

This has the same Neural Engine as the A12X and A12. 
A12Z appears to be identical to A12X, but with newer Stepping.

Devices: 

- iPad Pro 11-inch (2nd gen, 2020)
- iPad Pro 12.9-inch (4th gen, 2020)

### [A13 Bionic](https://en.wikipedia.org/wiki/Apple_A13) (APL1085 / APL1W85)

This Neural Engine has 8 cores and is 20% faster and consumes 15% lower power than the A12.

Devices: 

- iPhone 11 (2019)
- iPhone 11 Pro (2019)
- iPhone 11 Pro Max (2019)
- iPhone SE (2nd gen, 2020)
- iPad (9th gen, 2021)
- Studio Display (2022)

The CPU in the A13 also has its own machine learning accelerators (AMX blocks) that do matrix multiplications up to 6x faster than the A12's CPU.

### [A14 Bionic](https://en.wikipedia.org/wiki/Apple_A14) (APL1001 / APL1W01)

The A14 has a 16-core Neural Engine that is twice as fast as the previous generation, and can perform 11 trillion operations per second.

Devices: 

- iPad Air (2020)
- iPhone 12 (2020)
- iPhone 12 Mini (2020)
- iPhone 12 Pro (2020)
- iPhone 12 Pro Max (2020)

The A14 also has second-generation "AMX blocks" for accelerating machine learning operations (matrix multiplications) on the CPU.

### [M1 (Family)](https://en.wikipedia.org/wiki/Apple_M1)

M1 chip family has four members: **M1(APL1102)**, **M1 Pro(APL1103)**, **M1 Max(APL1105)**, **M1 Ultra(APL1W06)**

The Neural Engine of M1, M1 Pro and M1 Max chips has the same scale, with 16 cores, which can perform up to 11 trillion operations per second.

M1 Ultra is actually connecting the grains of two M1 Max chips using an UltraFusion package architecture, but it will be treated as one chip by the software. M1 Ultra's Neural Engine has 32 cores and can perform up to 22 trillion operations per second.

They were the first neural engines available on macOS devices.

Their neural engine architecture is likely the same as that of the A14 Bionic.

M1 Devices: 

- MacBook Air (2020)
- MacBook Pro 13" with two Thunderbolt 3 ports (2020)
- Mac mini (2020)
- iPad Pro 11-inch (3rd gen, 2021)
- iPad Pro 12.9-inch (5th gen, 2021)
- iPad Air (5th gen, 2022)

M1 Pro Devices：

- MacBook Pro 14-inch (2021)
- MacBook Pro 16-inch (2021)

M1 Max Devices:

- MacBook Pro 14-inch (2021)
- MacBook Pro 16-inch (2021)
- Mac Studio (2022)

M1 Ultra Devices:

- Mac Studio (2022)

The Neural Engine is not available on Intel-based Macs, only on Macs with Apple Silicon.

### [A15 Bionic](https://en.wikipedia.org/wiki/Apple_A15)(APL1007 / APL1W07)

The A15 has a 16-core Neural Engine, with the same amount of cores it can perform 15.8 trillion operations per second (43% faster than the previous generation). 

Devices: 

- iPad Mini (6th gen, 2021)
- iPhone 13 (2021)
- iPhone 13 Mini (2021)
- iPhone 13 Pro (2021)
- iPhone 13 Pro Max (2021)
- iPhone SE (3rd gen, 2022)

## Recent devices without a Neural Engine

It's important to note that not *all* new devices have a Neural Engine. The A10 chipset does not have an ANE but is still being used in certain devices.

Devices with an A10 Fusion (APL1024 / APL1W24):

- iPhone 7, 7 Plus (2016)
- iPad (6th gen, 2018)
- iPad (7th gen, 2019)
- iPod touch (7th gen, 2019)

Devices with an A10X Fusion (APL1071 / APL1W71):

- iPad Pro 10.5-inch (2017)
- iPad Pro 12.9-inch (2nd gen, 2017)
- Apple TV 4K (5th gen, 2017)

Devices older than 2016 obviously do not have a Neural Engine.

There is currently no Apple Watch with an ANE.

Intel-based Macs do not have an ANE.
