> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [unix.stackexchange.com](https://unix.stackexchange.com/questions/117741/d-bus-library-appears-to-be-incorrectly-set-up)

I ran into the same issue and this command fixed it for me

```
`VLC media player 2.0.5 Twoflower (revision 2.0.5-0-g1661b7d)
 process 20124: D-Bus library appears to be incorrectly set up; failed to read      machine uuid: Failed to open "/var/lib/dbus/machine-id": No such file or directory
 See the manual page for dbus-uuidgen to correct this issue.
 D-Bus not built with -rdynamic so unable to print a backtrace
 Aborted
```

Source: [http://www.torkwrench.com/2011/12/16/d-bus-library-appears-to-be-incorrectly-set-up-failed-to-read-machine-uuid-failed-to-open-varlibdbusmachine-id/](http://www.torkwrench.com/2011/12/16/d-bus-library-appears-to-be-incorrectly-set-up-failed-to-read-machine-uuid-failed-to-open-varlibdbusmachine-id/)