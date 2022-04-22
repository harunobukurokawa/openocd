# OpenOCD 


## Build and install 

```
git clone git@github.com:harunobukurokawa/openocd.git -b sandbox/armv8r-aarch32-gen3gen4support
cd openocd/ 
./bootstrap
./configure
make
sudo make install
```

## Run OpenOCD

* In the case of "ARM-USB-OCD-H". if you use "ARM-USB-TINY-H" JTAG, please use "olimex-arm-usb-tiny-h.cfg" file instead of ocd-h.cfg.

Step1. Power On target board.
Step2. Run OpenOCD from Host PC
Step3. Run gdb via another terminal 

### for H3SK/M3SK

Boot for CA core
```
$ openocd -c "adapter speed 20000" \
    -f interface/ftdi/olimex-arm-usb-ocd-h.cfg \
    -f board/renesas_h3ulcb.cfg \
```

Boot from CR
```
$ openocd -c "adapter speed 20000" \
    -f interface/ftdi/olimex-arm-usb-ocd-h.cfg \
    -f board/renesas_h3ulcb.cfg \
    -c "bindto 0.0.0.0" \
    -c init \
    -c "r8a77950.r7 arp_examine"
```

# -c "bindto 0.0.0.0" is required if you connect from another PC.

### for Spider (not tested)

```
$ openocd -c "adapter speed 20000" \
    -f interface/ftdi/olimex-arm-usb-ocd-h.cfg \
    -f board/renesas_spider.cfg \
```

```
$ openocd -c "adapter speed 20000" \
    -f interface/ftdi/olimex-arm-usb-ocd-h.cfg \
    -f board/renesas_spider.cfg \
    -c init \
    -c "r8a779a0.r52 arp_examine"
```

## Connect GDB 

## from Host PC (localhost)

```
$ gdb-multiarch binary.elf

# connect gdb session via port3333 or 3334
(gdb) target remote localhost:3333 (for CA core)
(gdb) target remote localhost:3334 (for CR core)

(gdb) load

# check reading register 
(gdb) info register
```

### Connect GDB from other host PC (T.B.D) 

<comment>

```
$ gdb-multiarch binary.elf

# connect gdb session via port3333 or 3334
(gdb) target remote 192.168.20.XXX:3333 (for CA core)


```
