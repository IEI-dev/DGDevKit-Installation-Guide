# DGDevKit Installation Guide

Tank-XM811 + A40
HW: https://www.ieiworld.com/en/product-ns/model.php?II=2

OS(ubuntu-iot 22.04 desktop):
link: https://ubuntu.com/download/iot/intel-iot
    
GPU Driver:   
link: https://github.com/intel/edge-insights-vision
   
OpenVINO tutorials:   
link: https://github.com/openvinotoolkit/openvino_notebooks
   
# Flash OS   
1. Download below iso file and flash OS(ubuntu-iot 22.04 desktop) images onto pen drive    
link: https://ubuntu.com/download/iot/intel-iot    
      ![image](/uploads/813652a90b8d228340d24fe902a0e4eb/image.png)
2. insert the pen drive into the USB port    
3. press 'del' and power-on, will boot BIOS  
4. make sure display is IGFX(HDMI), BIOS setting -> primary display -> IGFX  
![image](/uploads/b1c842edc8cfd61eb94401b4afbd0142/image.png)
![image](/uploads/360b35931cffb30d31788192f53cc1d4/image.png)
5. setup boot priority, BIOS setting -> boot -> boot1-USB(UEFI...)   
![image](/uploads/1a1892961a50c7532120edd306121ebb/image.png)
![DSC_0452](/uploads/f3e2dfaaeabe8d57aa03d1551e48968c/DSC_0452.JPG)
![DSC_0453](/uploads/425ab80b89b2797c30b2efd7a36f8951/DSC_0453.JPG)
6. save and reboot, install ubuntu    
7. when install finish, you can use below command to validate ubuntu version
```shell
lsb_release -a
#Description:  Ubuntu 22.04.02 LTS
   
uname -a   
#5.15.0-1026-intel-iotg 
   
```
![image](/uploads/d6dca4ff50b35d462e6e72b0b70af55d/image.png)
   
# Install GPU Driver   
1. GPU Driver(EIV):    
link: https://github.com/intel/edge-insights-vision
2. After Ubuntu has been successfully installed, install git and git clone the EIV repository into your Ubuntu system.   
```shell
sudo apt -y install git
git clone https://github.com/intel/edge-insights-vision.git
```
3. Update the package on the system.
```shell
sudo apt-get update
```
4. Install python3-pip.
```shell
sudo apt-get -y install python3-pip
```
4. Change the directory into edge-insights-vision and install the requirements package.
```shell
cd edge-insights-vision
pip3 install -r requirements.txt
```
![image](/uploads/873ab1e7df6e3b60725da29a788964a2/image.png)  
![image](/uploads/e5d83c6af242acb6cf254aec94cc6a0e/image.png)  
![image](/uploads/b3653e6f9157778620fa566f7790d686/image.png)   
5. Install EIV. If your system has a dGPU, it will upgrade your kernel to 6.2.8 and your system will reboot during installation.
Please save your work before starting the installation.   
```shell
python3 eiv_install.py
```   
![image](/uploads/26c506f6f81b63623b375dc9ef1e1ba0/image.png)   
6. make sure you were upgrade to kernel 6.2.8    
```shell
uname -a
#Linux iei-SJB8 6.2.8-060208-generic #202303220943 SMP PREEMPT_DYNAMIC Wed Mar 22 13:50:04 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```
![image](/uploads/0ea16756409c83dbe9b5a7050b973965/image.png)   
7. Restart your system after the installation is complete.     
*it will stop on install process 57% a long time for download example model.  
base on your status, you also need to enter root password again.    
```shell
python3 eiv_install.py
```   
![image](/uploads/7275a342a7e6e8339957813cf5800183/image.png)   
8. when install finish, you will see three modules success information on status    
![image](/uploads/5babc22e933bb26d2a7dce7528bc7e29/image.png)   
9. validate dGPU driver is work, and resize bar support memory 8G  
```shell
clinfo | grep 'Driver Version'
#Driver Version: 23.17.26241.21
    
lspci -v

#04:00.0 VGA compatible controller: Intel Corporation Device 56b1 (rev 05) (prog-if 00 [VGA controller])
#        Subsystem: Intel Corporation Device 1211
#        Flags: bus master, fast devsel, latency 0, IRQ 141
#        Memory at 81000000 (64-bit, non-prefetchable) [size=16M]
#        Memory at 6000000000 (64-bit, prefetchable) [size=8G]
#        Expansion ROM at 82000000 [disabled] [size=2M]
#        Capabilities: <access denied>
#        Kernel driver in use: i915
#        Kernel modules: i915

```   
![image](/uploads/2f716425034a6241d02dd96e54406444/image.png)
![image](/uploads/5dccb179a1ab85771eb8e222f42e790b/image.png)
![image](/uploads/4101fda085946191a502dca840d6007d/image.png)
  
  
# Run Jupyter Notebook Tutorials   
1. After successful installation, change the launch_notebooks.sh script to executable and run the launcher script as shown here:   
```shell
cd edge-insights-vision
chmod +x launch_notebooks.sh
./launch_notebooks.sh
```   
![image](/uploads/c8a46549e596b1ac3a25408a6739c244/image.png)   
2. Open your browser and paste the URL with token    
![image](/uploads/df288a87c4829fe2e46fc95a52cd2f14/image.png)   
3. you can try tutorials 001-hello-world and 108-gpu-device      
      
# Tutorials 001-hello-world   
tutorial step   
![image](/uploads/694fcef5fe0cc5d935c593c6dd72a503/image.png)   
![image](/uploads/d11b8c94939eb58317cd4d101aa1036f/image.png)   
![image](/uploads/3cf04180936d65cb16b999ff8cb096f6/image.png)   
you also can modify and try to run this tutorial on GPU.1(ARC-A40)   
![image](/uploads/2f4abb6e52dd39638bfb6378e9121d54/image.png)   
   
# Tutorials 108-gpu-device   
![image](/uploads/2a7d06f77fc0e777cc47d7fff78ea330/image.png)   
It seems have error on 66%, but it still can be work in next step   
![image](/uploads/fe24917207cf70186dfec9c60047c9a0/image.png)   
CPU performance   
![image](/uploads/dc2f6b75cc5e62815e06436fc49aba12/image.png)   
GPU.0 Performance(iGPU)   
![image](/uploads/74dd032537a4934952b1b6d6b9dfbd72/image.png)   
GPU.1Performance(dGPU)   
![image](/uploads/230c32d703bf8448ab5fcf4e21af2748/image.png)   
result   
![image](/uploads/bfca1ee1c5ea5921a09ed2cb2c507c97/image.png)   