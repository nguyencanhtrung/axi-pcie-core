# axi-pcie-core

<!--- ######################################################## -->

# Before you clone the GIT repository

1) Create a github account:
> https://github.com/

2) On the Linux machine that you will clone the github from, generate a SSH key (if not already done)
> https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

3) Add a new SSH key to your GitHub account
> https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

4) Setup for large filesystems on github
``` $ git lfs install```

<!--- ######################################################## -->

# Clone the GIT repository (however, this git repo intended to be a submodule of another project)
``` $ git clone --recursive git@github.com:slaclab/axi-pcie-core```

<!--- ######################################################## -->

# How to load the driver

```
# Confirm that you have the board the computer with VID=1a4a ("SLAC") and PID=2030 ("AXI Stream DAQ")
$ lspci -nn | grep SLAC
04:00.0 Signal processing controller [1180]: SLAC National Accelerator Lab TID-AIR AXI Stream DAQ PCIe card [1a4a:2030]

# Clone the driver github repo:
$ git clone --recursive https://github.com/slaclab/aes-stream-drivers

# Go to the driver directory
$ cd aes-stream-drivers/data_dev/driver/

# Build the driver
$ make

# Example of loading driver with 2MB DMA buffers
$ sudo /sbin/insmod ./datadev.ko cfgSize=0x200000 cfgRxCount=256 cfgTxCount=16

# Give appropriate group/permissions
$ sudo chmod 666 /dev/data_dev*

# Check for the loaded device
$ cat /proc/data_dev0
```

<!--- ######################################################## -->

# How to install the Rogue With Anaconda

> https://slaclab.github.io/rogue/installing/anaconda.html

<!--- ######################################################## -->

# How to reprogram the PCIe firmware via Rogue software

1) Setup the rogue environment
```
$ source /path/to/my/anaconda3/etc/profile.d/conda.sh
$ conda activate rogue_env
```

2) Run the PCIe firmware update script:
```
$ python axi-pcie-core/python/updatePcieFpga.py --path <PATH_TO_IMAGE_DIR>
```
where <PATH_TO_IMAGE_DIR> is path to .MCS image directory

3) Reboot the computer
```
sudo reboot
```

<!--- ######################################################## -->
