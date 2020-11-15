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
 Run these commands on your terminal. You can alternatively create a virtual environment and then install these packages if you are willing to install multiple versions of Cuda or TensorFlow.
 
 ### Step 1:
 Use these codes to remove any traces of previous Cuda installations on your system. These steps are needed only if you have installed Cuda versions before. This is necessary, as the Cuda versions can conflict and cause errors in the isntallation.
 
 <code>sudo rm /etc/apt/sources.list.d/cuda*</code>
 
 <code>sudo apt remove --autoremove nvidia-cuda-toolkit</code>
 
 <code>sudo apt remove --autoremove nvidia-*</code>

### Step 2:
Now let's set-up the necessary Presonal Package Archives (PPAs) needed for Cuda installation. This is the easiest way to get the packages.

<code>sudo apt update</code>

<code>sudo add-apt-repository ppa:graphics-drivers</code>

<code>sudo apt-key adv --fetch-keys  http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub</code>

<code>sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list'</code>

<code>sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda_learn.list'</code>

### Step 3:
Installing the Cuda 10.1 and cuDNN 7.6.5 (the latest version when I installed it)

<code>sudo apt update</code>

<code>sudo apt install cuda-10-1</code>

<code>sudo apt install libcudnn7</code>

### Step 4:
We need to set the path for Cuda. I will use vim here as the text editor to edit the '.profile' file. Vim (Vi IMproved) is a text editor that is upwards compatible to Vi. You can just go with Vi is you wish to edit using that.

<code>sudo apt update</code>

<code>sudo apt install vim</code>

<code>vim --version</code>

_Update the .profile file_

<code>sudo vi ~/.profile</code>

<code></code>
<code></code>
<code></code>

