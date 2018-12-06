`gr-ieee802.11`: Installation should be done in `master` branch as GNU radio is installed as `master` branch.

-------------------------------------

Note : **For complete installation process of** `gr-ieee802.11`: please seek help at git [my repo](https://gitlab.com/gorlapraveen/gnu_radio_localization/blob/4ddcf0823f123496c95d53567037be65dee19a2f/README.md)
------------------------------------------

**Possible Errors:**

1. For using `gr-ieee802.11` :  with an example of `wifi_transceiver.grc` and its customization for other sdr: Possible erros would be 
```
   linux; GNU C++ version 6.2.0 20161027; Boost_106200; UHD_003.009.005-0-unknown

     MAPPER: encoding: 0
     set_min_output_buffer on block 9 to 397056
     set_min_output_buffer on block 11 to 397056
      set_min_output_buffer on block 13 to 397056
     set_min_output_buffer on block 14 to 397056
set_min_output_buffer on block 16 to 397056
set_min_output_buffer on block 40 to 100000
Traceback (most recent call last):
  File "/home/praveen-ubuntu-radio/Documents/Gnu_radio/Gnu_radio_programs/wifi_transceiver.py", line 326, in <module>
    main()
  File "/home/praveen-ubuntu-radio/Documents/Gnu_radio/Gnu_radio_programs/wifi_transceiver.py", line 314, in main
    tb = top_block_cls()
  File "/home/praveen-ubuntu-radio/Documents/Gnu_radio/Gnu_radio_programs/wifi_transceiver.py", line 219, in __init__
    self.blocks_tuntap_pdu_0 = blocks.tuntap_pdu('tap0', 440, False)
  File "/usr/lib/python2.7/dist-packages/gnuradio/blocks/blocks_swig5.py", line 2154, in make
    return _blocks_swig5.tuntap_pdu_make(dev, MTU, istunflag)
RuntimeError: gr::tuntap_pdu::make: tun_alloc failed (are you running as root?)

>>> Done
```


2. Solution: Simply disable `TUNTAP` in `wifi_transceiver.grc`
