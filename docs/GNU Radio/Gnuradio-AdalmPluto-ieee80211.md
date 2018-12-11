# Installation

**Step by Step installation of GNU radio > Adlam-Pluto > ieee820.11a/g/p**  

-----------------------------------------------------------------------------

## GNURadio

Debian/Ubuntu and derivates 

    apt install gnuradio
    
------------------------------------------------------------------------------    
    
## Adlam Pluto 


**Dependencies for Adlam Pluto**: for Gnuradio

 -------------------------------------------------------------------
 
Install GNU Radio and other dependencies

        apt-get -y install gnuradio-dev libxml2 libxml2-dev bison flex libcdk5-dev cmake git
        libaio-dev libboost-all-dev swig
        
But before we want to install `Analog Devices - Adlam Pluto` supported `libraries`
for `GNU RADIO`. we need some, depending on the backend (how you want to attach the IIO device),
you may need at least one of:

     sudo apt-get install libaio-dev libusb-1.0-0-dev libserialport-dev libxml2-dev libavahi-client-dev
     

Incase If libserialport is too old (e.g. on Ubuntu 16.04), you need to do the following to build libiio:


     sudo apt-get install autoconf
     git clone git://sigrok.org/libserialport
      pushd libserialport
     git checkout libserialport-0.1.1
     ./autogen.sh
     ./configure
     make
    sudo make install
    sudo ldconfig

Incase the `git clone git://sigrok.org/libserialport` is not responding, i.e server 
is down/busy or time, download them manually using the following details

1. Get [sigrok](https://packages.ubuntu.com/search?keywords=sigrok) deb package 
   for Ubuntu 16.04 and install it using `dpkg -i <Package_name.deb>`
2. Get [libserialport0](https://packages.ubuntu.com/xenial/libserialport0) and
  [libserialport-dev](https://packages.ubuntu.com/xenial/libserialport-dev) and 
  install them using `dpkg -i <Package_name.deb>` or you can search in 
  ubuntu software repository using `apt search Package_name`and install them using `apt install package_name`.
3. If there are dependency problems use `apt -f install` to get solve the dependency
   problem and again `install` above packages(2) using `dpkg -i <Package_name>`.

 ---------------------------------------------------------------------------------------
 
----------------------------------------------------------------------------------------------------------------------------------------------


The above are some of the drivers that is needed for `Adlam-pluto` gnuradio `libiio` library to interact with system through Serial usb.

-----------------------------------------------------------------

**AdlamPluto**: Actual blocks for `Gnu radio` after satisfying above `dependencies` .

 ---------------------------------------
 
Download and build libiio:

      git clone https://github.com/analogdevicesinc/libiio.git
      cd libiio
      cmake .
      make 
      sudo make install
      cd ..
      
Download and build libad9361-iio

     git clone https://github.com/analogdevicesinc/libad9361-iio.git
     cd libad9361-iio
     cmake .
     make 
      sudo make install
     cd ..

Download and build gr-iio

     git clone https://github.com/analogdevicesinc/gr-iio.git
     cd gr-iio
     cmake .
     
In your PYTHONPATH during installation. If this is not the case you will 
    need to modify the `cmake` command for the gr-iio configuration above with the
  following :

     cmake -DCMAKE_INSTALL_PREFIX=/usr .  
     make 
     sudo make install
     cd ..
     sudo ldconfig
     
     

GNURadio will recommend you include

      /usr/local/lib${type}/python${PYVER}/site-packages/gnuradio

or

     /usr/local/lib${type}/python${PYVER}/dist-packages/gnuradio
     

 For certain binary installs of GNU Radio, python binding are placed in a compet
 ing folder to GNU Radio's built-in blocks. This may require you to manualy copy
 blocks between the /usr/lib and /usr/local/lib. If you receive import error for
 iio_swig this is likely the case. To remedy this move the blocks between the ne
 cessary folders:

     cp -r /usr/local/lib/python2.7/dist-packages/gnuradio/iio/usr/lib/python2.7/dist-packages/gnuradio/

This is due to the iio python blocks being placed in the gnuradio subfolder. 
This is required since the iio language binding for python would overwrite these blocks.      


**References** : For more please visit https://wiki.analog.com/resources/tools-software/linux-software/gnuradio and/or 
https://www.plutosdr.com/viewtopic.php?t=5  and/or https://wiki.analog.com/resources/tools-software/linux-software/libiio 
and/or https://www.reddit.com/r/RTLSDR/comments/6t1wnz/they_finally_arrived/

-----------------------------------------------------------------------------------------------------------------------

## IEEE802.11/a/g/p Implementation

**IEEE802.11/a/g/p implementation in GNU radio:**

Get `gr-foo` >> `gr-ieee802.11`(ieee802.11/a/g/p) >> `gr-rftap`(Provides bridege 
between Gnu radio and Wireshark for Packte data intersecption such as SNR, MAc, etc... ) >> `wireshark`.

 -------------------------------------------------------------------------------------------------------
 
 Before installing, you may need `liblog4cpp5-dev` and/or `liblog4cpp`. Install them
 using
 
      sudo apt-get install liblog4cpp 
      sudo apt-get install liblog4cpp5-dev
      
If above is not exact package to be installed use `apt search <package_name>` and install it.
 
 
**Installing** `gr-foo` **from source** : After cloning, build in` master` branch :`git checkout master ` 
or else there may be error sinc `gnuradio` is build in its `master` branch

    git clone https://github.com/bastibl/gr-foo.git
    cd gr-foo
    git checkout master
    mkdir build
    cd build
    cmake ..
    make
    sudo make install
    sudo ldconfig
    

**Installing** `gr-ieee802.11` **from source** : After cloning, build in `master` 
branch :`git checkout master ` 
or else there may be error sinc `gnuradio` is build in its `master` branch

     git clone git://github.com/bastibl/gr-ieee802-11.git
     cd gr-ieee802-11
     mkdir build
     cd build
     cmake ..
     make
     sudo make install
     sudo ldconfig
     



**Adjust Maximum Shared Memory**

Since the transmitter is using the Tagged Stream blocks it has to store a complete
frame in the buffer before processing it. The default maximum shared memory might not be enough on most Linux systems. It can be increased with

    sudo sysctl -w kernel.shmmax=2147483648


**Some Documentation** below(preferebly follow it for reducing errors):

1. **OFDM PHY**:The physical layer is encapsulated in a hierarchical block to allow for a clearer
transceiver structure in GNU Radio Companion. This hierarchical block is not included
in the installation process. You have to open `/examples/wifi_phy_hier.grc` with GNU Radio 
Companion and build it. This will install the block in `~/.grc_gnuradio/`.

2. **Check message port connections** :Sometime the connections between the message
ports (the gray ones in GNU Radio Companion) break. Therefore, please open the 
flow graphs and assert that everything is connected. It should be pretty obvious 
how the blocks are supposed to be wired. Actually this should not happen anymore,
so if your ports are still unconnected please drop me a mail.

3. **Python OpenGL**: If you want to run the receive demo (the one that plots the 
subcarrier constellations), please assert that you have python-opengl installed.
The nongl version of the plot does not work for me.

4. **Run volk_profile**:volk_profile is part of GNU Radio. It benchmarks different 
SIMD implementations on your PC and creates a configuration file that stores the
fastest version of every function. This can speed up the computation considerably
and is required in order to deal with the high rate of incoming samples.
Calibrate your daughterboard

If you have a WBX, SBX, or CBX daughterboard you should calibrate it in order to 
minimize IQ imbalance and TX DC offsets. See the [application notes](http://files.ettus.com/manual/page_calibration.html).

**Checking your installation**:

As a first step I recommend to test the wifi_loopback.grc flow graph. This flow graph does not need any hardware and allows you to ensure that the software part is installed correctly. So open the flow graph and run it. If everything works as intended you should see some decoded 'Hello World' packets in the console.
Troubleshooting

If GRC complains that it can't find some blocks (other than performance counters and hierarchical blocks) like

    >>> Error: Block key "ieee802_11_ofdm_mac" not found in Platform - grc(GNU Radio Companion)
    >>> Error: Block key "foo_packet_pad" not found in Platform - grc(GNU Radio Companion)

Most likely you used a different `CMAKE_INSTALL_PREFIX `for the module than for GNU Radio.
Therefore, the blocks of the module ended up in a different directory and GRC can't find them.
You have to tell GRC where these blocks are by creating/adding to your `~/.gnuradio/config.conf` something like

    [grc]
    global_blocks_path = /opt/local/share/gnuradio/grc/blocks
    local_blocks_path = /Users/basti/usr/share/gnuradio/grc/blocks

But with the directories that match your installation.

**UsageSimulation**:

The loopback flow graph should give you an idea of how simulations can be conducted.
To ease use, most blocks have debugging and logging capabilities that can generate traces of the simulation.
You can read about the logging feature and how to use it on the GNU Radio Wiki.
Unidirectional communication

As first over the air test  recommend to try `wifi_rx.grc` and `wifi_tx.grc`. 
Just open the flow graphs in GNU Radio companion and execute them.
If it does not work out of the box, try to play around with the gain. 
If everything works as intended you should see similar output as in the `wifi_loopback.grc`(for this possible [erros and solution]() ) example.

**RX frames from a WiFi card** : TBD

**TX frames to a WiFi card** :TBD

**Transceiver (SDR <-> SDR)**: TBD

**Ad Hoc Network with WiFi card**:

    The transceiver is currently connected to a TAP device, i.e. is a virtual Ethernet interface. Therefore, we have no WiFi signaling like association requests and hence, the transceiver can not "join" an ad hoc network. You have to make some small changes to the kernel in order to convince you WiFi card to send to this hosts nevertheless.
    The transceiver can not respond to ACKs in time. This is kind of an architectural limitation of USRP + GNU Radio since Ethernet and computations on a normal CPU introduce some latency. You can set the number of ACK retries to zero and handle retransmits on higher layers (-> TCP).
    RTS/CTS is not working for the same reason. You can however just disable this mechanism.
    Currently, there is no CSMA/CA mechanism, but this can be implemented on the FPGA.

**Troubleshooting**:

    Please check compile and installation logs. They might contain interesting information.

    Did you calibrate your daughterboard?

    Did you run volk_profile?

    Did you try different gain settings?

    Did you close the case of the devices?

    Did you try real-time priority?

    Did you compile GNU Radio and gr-ieee802-11 in release mode?

    If you see warnings that blocks_ctrlport_monitor_performance is missing that 
    means that you installed GNU Radio without control port or performance counters.
    These blocks allow you to monitor the performance of the transceiver while it is 
    running, but are not required. You can just delete them from the flow graph.

    The message

    You must now use ifconfig to set its IP address. E.g., $ sudo ifconfig tap0 192.168.200.1
    is normal and is output by the TUN/Tap Block during startup. The configuration of 
    the TUN/TAP interface is handled by the scripts in the apps folder.

    Did you try to tune the RF frequency out of the band of interest (i.e. used the LO
    offset menu of the flow graphs)?
    If 'D's appear, it might be related to your Ethernet card. Assert that you made 
    the sysconf changes recommended by Ettus. Did you try to connect you PC directly
    to the USRP without a switch in between?


**For More about this please seek help from** https://github.com/bastibl/gr-ieee802-11

 ------------------------------------
 
 **After(or even before the above) this you actually needs** `gfortran`(GNU Fortran Compiler), `lapack` and `itpp` 
 (`lapack` and `itpp` are for numerical computation packages)
 
 1. Get [gfortran](https://packages.ubuntu.com/search?keywords=gfortran) here or install by `sudo apt-get install gfortran`
 2. Get [itpp](https://sourceforge.net/projects/itpp/files/). It is actually placed in sourforge, So I am not confident that it will maintain there, so I downloaded, you can get it 
 at [my git](https://gitlab.com/gorlapraveen/gnu_radio_localization/tree/master/itpp-4.3.1).
 3. Get by `sudo apt-get install libatlas-base-dev libblas-dev liblapack-dev`, Incase, if any dependency problem please refer https://askubuntu.com/questions/623578/installing-blas-and-lapack-packages
 

By now we have install compliers and numerical packages such as `gfortran`, `lapack` and `itpp`. We now install
`gr-rftap` and `wireshark`

 ----------------------------------
 
## Installing gr-rftap and Wireshark
 
### Installing `gr-rftap`:

 **Simple Installation of **`gr-rftap` **using Package Manager**

    pybombs install gr-rftap

**Manual Installation of** `gr-rftap` :To manually install the blocks do

    git clone https://github.com/rftap/gr-rftap
    cd gr-rftap
    mkdir build
    cd build
    cmake ..
    make
    sudo make install
    sudo ldconfig

**Usage, Demos and Further information**: See `RDS` and `Wi-Fi` flowgraphs in 
`examples/ directory`. See: https://rftap.github.io/

### Installation of `Wireshark`:

Install `wireshark` and its dependencies at

     sudo apt install wireshark*
    
In case, some times we also need `tshark` for commandline based processing so;

     sudo apt install tshark*


 ----------------------------------------------------------------------------
 Compiled by @gorlapraveen
 
 --------------------------------- End of File --------------------------------
 
 
 
------------------------------------------------------------------------------------------------------------------------------------------------
     
     