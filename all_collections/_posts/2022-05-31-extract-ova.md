---
layout: post
title:  "Digital Forensics - Export OVA"
image: /assets/img/exova/3.PNG
categories: [ova, export, modprobe, qemu]
---

## Necessary tools

```javascript
sudo apt-get install qemu-utils
```

#### Extracting the OVA

```javascript
cp /media/sf_Downloads/system.ova /home/kali/Desktop
tar -xvf system.ova
```

![image]( /assets/img/exova/1.PNG)

#### Forward the partition of the ova to our machine

```javascript
sudo modprobe nbd
sudo qemu-nbd -r -c /dev/nbd1 /home/kali/Desktop/system-disk001.vmdk
```

![image]( /assets/img/exova/2.PNG)


#### Proof of Concept

![image]( /assets/img/exova/3.PNG)

