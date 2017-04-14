---
layout: post
title:  "How to Set up Ubuntu 16 in Hyper V"
---

# Things you will need
* An iso of Ubuntu 16
* a computer with Hyper-V installed
* Powershell

# How to to begin
1. Set up your Virtual Switch
    1.1 Choose either an internal switch or an external switch
2. Setting up your Hyper-V instance
    2.1 Name your instance and pick where you want to store your VM
    2.2 Select generation 2
    2.3 Choose start up memory
    2.4 Select your recently created Switch
    2.5 Create a hard disk
    2.6 Select your Ubuntu 16 ISO
    2.7 Finish
3. Making sure It can Boot
    3.1 Open powershell
    3.2 `Set-VMFirmware -VMName "Your-Computer-Name-Here" -EnableSecureBoot off
4. Your Gen 2 Ubuntu 16 VM should boot now