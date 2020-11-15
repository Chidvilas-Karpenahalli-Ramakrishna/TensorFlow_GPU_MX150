## TensorFlow-GPU 2.2.0 for Nvidia MX150 in Ubuntu 18.04 operating system.

### Overview:
I couldn't find a lot of support for installing TensorFlow-GPU >2.0 for MX150 graphics card and hence, I am documenting this for anyone who wishes to do the same. This will be a step-by-step procedure and I will try my best to explain all the steps in detail. 

### Specifications:
1.) ___Operating system:___ Ubuntu 18.04.5 LTS

2.) ___Graphics card:___ Nvidia GeForce MX150/PCIe/SSE2, 4GB dedicated GDDR5 memory

3.) ___TensorFlow-GPU version:___ 2.2.0

4.) ___Cuda version:___ 10.1

5.) ___cuDNN version:___ 7.6.5

 ## Steps:
 
 ### Step 1:
 Use these codes to remove any traces of previous Cuda installations on your system. These steps are needed only if you have installed Cuda versions before. This is necessary, as the Cuda versions can conflict and cause errors in the isntallation.
 
 <code>sudo rm /etc/apt/sources.list.d/cuda*</code>
 
 <code>sudo apt remove --autoremove nvidia-cuda-toolkit</code>
 
 <code>sudo apt remove --autoremove nvidia-*</code>


