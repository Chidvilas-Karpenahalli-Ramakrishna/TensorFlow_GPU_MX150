## TensorFlow-GPU for Nvidia GeForce MX150 in Ubuntu 18.04 operating system

### Overview:
I couldn't find a lot of support for installing TensorFlow-GPU >2.0 for MX150 graphics card and hence, I am documenting this for anyone who wishes to do the same. This will be a step-by-step procedure and I will try my best to explain all the steps in detail. It starts from installing Cuda, cuDNN, Anaconda and TensorFlow GPU. It also includes a cute code at the end to see if TensorFlow is working fine.

### Specifications:
1.) ___Operating system:___ Ubuntu 18.04.5 LTS

2.) ___Graphics card:___ Nvidia GeForce MX150/PCIe/SSE2 4GB dedicated GDDR5 memory

3.) ___TensorFlow-GPU version:___ 2.2.0

4.) ___Cuda version:___ 10.1

5.) ___cuDNN version:___ 7.6.5

 ## Steps to install Cuda:
Run these commands on your terminal. You can alternatively create a virtual environment and then install these packages if you wish to install multiple versions of Cuda or TensorFlow.
 
 ### Step 1:
Use these codes to remove any traces of previous Cuda installations on your system. These steps are needed only if you have installed Cuda versions before. This is necessary, as the Cuda versions can conflict and cause errors in the installation.
 
<code>sudo rm /etc/apt/sources.list.d/cuda*</code>
 
<code>sudo apt remove --autoremove nvidia-cuda-toolkit</code>
 
<code>sudo apt remove --autoremove nvidia-*</code>

### Step 2:
Now let's set-up the necessary Personal Package Archives (PPAs) needed for Cuda installation. This is the easiest way to get the packages.

<code>sudo apt update</code>

<code>sudo add-apt-repository ppa:graphics-drivers</code>

<code>sudo apt-key adv --fetch-keys  http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub</code>

<code>sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list'</code>

<code>sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda_learn.list'</code>

### Step 3:
Installing the Cuda 10.1 and cuDNN 7.6.5 (it's the latest version when I installed it)

<code>sudo apt update</code>

<code>sudo apt install cuda-10-1</code>

<code>sudo apt install libcudnn7</code>

### Step 4:
We need to set the path for Cuda. I will use vim here as the text editor to edit the '.profile' file. Vim (Vi IMproved) is a text editor that is upwards compatible to Vi. You can just go with Vi if you wish to edit using that, I will use Vim.

<code>sudo apt update</code>

<code>sudo apt install vim</code>

<code>vim --version</code>

Update the '.profile' file. First open the '.profile' file using the below code.

<code>sudo vim ~/.profile</code>

The '.profile' file opens. Press <code>i</code> key from your keyboard to enter insert mode. Once you press <code>i</code> you can see -- INSERT -- at the bottom of the terminal which means you are in insert mode. Now copy paste the below code in the same format.

 <pre><code>
 # set PATH for cuda 10.1 installation
 if [ -d "/usr/local/cuda-10.1/bin/" ]; then
    export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
 fi</code></pre>

Once done, press <code>esc</code> key to go out of the insert mode. Type <code>:wq</code> to write the changes and quit. If you feel you have done some mistake press <code>:q</code> to simply quit without writing the changes. You can open again and make changes. 

If you haven't done this properly, the terminal will throw an error saying that there is an error in so-and-so line of '.profile' file. Open the '.profile' file again using vim and make necessary changes.

### Step 5:
close the terminal. Restart the system and check the installations. 

<code>nvcc --version</code>

___Output:___ nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2019 NVIDIA Corporation
Built on Sun_Jul_28_19:07:16_PDT_2019
Cuda compilation tools, release 10.1, V10.1.243

<code>/sbin/ldconfig -N -v $(sed ‘s/:/ /’ <<< $LD_LIBRARY_PATH) 2>/dev/null | grep libcudnn</code>
 
 ___Output:___ libcudnn.so.7 -> libcudnn.so.7.6.5

You should see something similar to the above outputs. Use the following code to see the overall GPU stats.

<code>nvidia-smi</code>

__NOTE:__ nvidia-smi might not work as many people complain. Please remove 'secure boot' from your Ubuntu system and it will start working fine.

Alternatively, I would like to use 'gpustat' as it is more concise than nvidia-smi output and serves my purpose to see the GPU usage. Install it using the following code and run to see if it works fine.

<code>pip3 install gpustat</code> 

<code>gpustat</code>

### Cuda has been installed! yay!

## Steps to configure Anaconda and TensorFlow-GPU 2.2.0:
Now that we have Cuda up and running, let's install TensorFlow-GPU version 2.2.0 on our system.

### Step 1:
First let's install Anaconda. Download Anaconda for linux from here;

https://www.anaconda.com/products/individual

Download 64-Bit (x86) Installer which should be about 550 MB and is a '.sh' file.

Navigate to the folder containing the '.sh' file and right click and open terminal and enter the below code.

__Note:__ In my case the download file was _Anaconda3-2020.07-Linux-x86_64.sh_. So, I have edited the below code accordingly. When you download the Anaconda file, the name will be different as the version will be different. Replace the file name with your '.sh' file name.

<code>bash Anaconda3-2020.07-Linux-x86_64.sh</code>

This will be followed by a promt to press 'Enter'. Then read the License Terms and Conditions (Which I am sure you won't). Scroll down and type 'yes' to continue with the installation. 

You will get one more promt asking to confirm the default location. This should be fine for most users. Press <code>Enter</code> to continue the installation.

After this you will get one more promt _Do you wish the installer to prepend the Anaconda3 install location to PATH:_. Type 'yes' here and <code>Enter</code>. 

After this you will get another promt to install VSCode editor. Since, I wish to use Pycharm, I typed 'no'. If you wish to use VSCode then type 'yes' and follow the instructions. 

### Step 2:
Check the installation. Type the below code in the terminal.

<code>conda info</code>

You will get detailed specifications of the conda version etc.

<code>conda list</code>

You will see a list of all the packages isntalled under Anaconda alphabetically. As you can see, TensorFlow doesn't come pre-installed.

So, now that Anaconda is working fine. Let's install TensroFlow GPU.

### Step 3:
Installing TensorFlow GPU version. Type the following code;

<code>conda install -c anaconda tensorflow-gpu</code>

In my case the latest version was TensorFlow GPU 2.2.0. It might change in your case. If you need a specific version of TensorFlow then type == and the version for example: <code>conda install -c anaconda tensorflow-gpu==2.4.0</code>

### Step 4: 
Checking TensorFlow installation.

Go to the terminal and open juypter notebook.

<code>jupyter notebook</code>

Now, check if TensorFlow is using the GPU. There are multiple ways of doing this, I am going to list many methods here. Everything should return the same result.

<code>import tensorflow as tf</code>

<code>print(tf.__version__)</code>

__Output:__ 2.2.0, (In your case it will show your TensorFlow GPU version.)

<code>tf.test.is_gpu_available(cuda_only=False, min_cuda_compute_capability=None)</code>

__Output:__ True, (Ignore the warning. Here if you get False, then there is something wrong with the installation.)

<code>tf.config.list_physical_devices('GPU')</code>

__Output:__ [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')], 
(Here, GPU:0 means your GPU is the default device and TensorFlow is using GPU.)

<code>if tf.test.gpu_device_name():
    print('Default GPU Device: {}'.format(tf.test.gpu_device_name()))
else:
    print("Please install GPU version of TF")</code>

__Output:__ Default GPU Device: /device:GPU:0, (As, you can see all the outputs point to the fact that TensorFlow is now using GPU.)


### Step 5: [Optional]
Let's write a "Hello world" program for Machine Learning. When you are running this code, you can open terminal and see the gpustat and nvidia-smi output to see the performance of your GPU.

<code>import tensorflow as tf</code>

<code>import numpy as np</code>

<code>X = [1,2,3,4,5,6,7,8,9]</code>

<code>Y = [2,4,6,8,10,12,14,16,18]</code>

<code>model = tf.keras.Sequential([tf.keras.layers.Dense(1, input_shape=[1])])</code>

<code>model.compile(optimizer='sgd', loss='mean_squared_error')</code>

<code>model.fit(X, Y, epochs=500)</code>

<code>print(model.predict([20.0]))</code>

__Output:__ I got an output of 39.845165, while the expeced output was 40.0. This is due to lack of data. You get the drill!

## TensorFlow GPU is working fine. Enjoy coding!
