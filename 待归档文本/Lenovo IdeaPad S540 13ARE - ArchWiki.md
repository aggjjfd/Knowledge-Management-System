> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [wiki.archlinux.org](https://wiki.archlinux.org/title/Lenovo_IdeaPad_S540_13ARE)

Tips and tricks
---------------

### System Performance Mode

There are 3 modes available: _Intelligent Cooling_, _Extreme Performance_ and _Battery Saving_. To toggle it, you need to call some ACPI methods.

First install [kernels](https://archlinux.org/packages/?>acpi_call</a> (or <a rel=)) and load the [kernel module](/title/Kernel_module "Kernel module"):

```
 # modprobe acpi_call


```

Set it to _Intelligent Cooling_ mode:

```
 # echo '\_SB.PCI0.LPC0.EC0.VPC0.DYTC 0x000FB001' > /proc/acpi/call


```

Set it to _Extreme Performance_ mode:

```
 # echo '\_SB.PCI0.LPC0.EC0.VPC0.DYTC 0x0012B001' > /proc/acpi/call


```

Set it to _Battery Saving_ mode:

```
 # echo '\_SB.PCI0.LPC0.EC0.VPC0.DYTC 0x0013B001' > /proc/acpi/call


```

To verify your setting:

```
 # echo '\_SB.PCI0.LPC0.EC0.FCMO' > /proc/acpi/call
 # cat /proc/acpi/call | cut -d '' -f1


```

where `0x0` stands for _Intelligent Cooling_, `0x1` stands for _Extreme Performance_ and `0x2` stands for _Battery Saving_.

### Rapid Charge

Make sure you have set up [USB-C port failure](https://archlinux.org/packages/?>acpi_call</a>.
</p><p>Turn on:
</p><p></p><pre> #echo '\_SB.PCI0.LPC0.EC0.VPC0.SBMC 0x07' > /proc/acpi/call

</pre><p></p><p>Turn off:
</p><p></p><pre># echo '\_SB.PCI0.LPC0.EC0.VPC0.SBMC 0x08' > /proc/acpi/call

</pre><p></p><p>To verify your setting:
</p><p></p><pre># echo '\_SB.PCI0.LPC0.EC0.QCHO' > /proc/acpi/call
# cat /proc/acpi/call | cut -d '' -f1

</pre><p></p><p>where <code>0x0</code> stands for <i>off</i> and <code>0x1</code> stands for <i>on</i>.
</p><p></p>

Sometimes after hibernate or reboot, you might find that the USB typeC port cannot function normally. Charging, video output, data transmision all failed.  
This is a common issue for Lenovo Xiaoxin laptop, see [1](https://club.lenovo.com.cn/thread-5850476-1-1.html).

</p><p>Turn on:
</p><p></p><pre> #echo '\_SB.PCI0.LPC0.EC0.VPC0.SBMC 0x07' > /proc/acpi/call

</pre><p></p><p>Turn off:
</p><p></p><pre># echo '\_SB.PCI0.LPC0.EC0.VPC0.SBMC 0x08' > /proc/acpi/call

</pre><p></p><p>To verify your setting:
</p><p></p><pre># echo '\_SB.PCI0.LPC0.EC0.QCHO' > /proc/acpi/call
# cat /proc/acpi/call | cut -d '' -f1

</pre><p></p><p>where <code>0x0</code> stands for <i>off</i> and <code>0x1</code> stands for <i>on</i>.
</p><p></p>[[1]](https://club.lenovo.com.cn/thread-5850476-1-1.html) (written in chinese).

To fix this problem:

1.  remove _all_ the devices pluged to USB ports or 3.5mm headphone jack.
2.  Then poweroff your laptop, _make sure that the machine is not being charged_ .
3.  Press **fn+s+v**, hold it for a while to enable **battery shipping mode**.
4.  Now the computer should not be able to boot without AC power.
5.  Finally, connect the laptop to AC power and start it.

The USB-C port should now function normally, or you should ask for technical support from lenovo.
