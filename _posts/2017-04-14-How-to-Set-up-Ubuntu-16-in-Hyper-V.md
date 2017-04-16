---
layout: post
title:  "How to Set up Ubuntu 16 in Hyper V"
date:   2017-04-14 00:15
categories: jekyll update
---

# Things you will need
* An iso of Ubuntu 16
* a computer with Hyper-V installed
* Powershell

# How to to begin
1. Set up your Virtual Switch
   * Choose either an internal switch or an external switch
2. Setting up your Hyper-V instance
   1. Name your instance and pick where you want to store your VM
   2. Select generation 2
   3. Choose start up memory
   4. Select your recently created Switch
   5. Create a hard disk
   6. Select your Ubuntu 16 IS
   7. Finish
3. Making sure It can Boot
   1. Open powershell
   2. `Set-VMFirmware -VMName "Your-Computer-Name-Here" -EnableSecureBoot off
4. Your Gen 2 Ubuntu 16 VM should boot now