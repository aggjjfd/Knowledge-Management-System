> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [wiki.archlinux.org](https://wiki.archlinux.org/title/Hardware_video_acceleration#Intel)

> Hardware video acceleration makes it possible for the video card to decode/encode video, thus offload......

[Hardware video acceleration](https://en.wikipedia.org/wiki/Graphics_processing_unit#GPU_accelerated_video_decoding "wikipedia:Graphics processing unit") makes it possible for the video card to decode/encode video, thus offloading the CPU and saving power.

There are several ways to achieve this on Linux:

*   [Video Acceleration API](https://www.freedesktop.org/wiki/Software/vaapi/) (VA-API) is a specification and open source library to provide both hardware accelerated video encoding and decoding, developed by Intel.
*   [Video Decode and Presentation API for Unix](https://www.freedesktop.org/wiki/Software/VDPAU/) (VDPAU) is an open source library and API to offload portions of the video decoding process and video post-processing to the GPU video-hardware, developed by NVIDIA.
*   [NVDECODE/NVENCODE](https://developer.nvidia.com/nvidia-video-codec-sdk) - NVIDIA's proprietary APIs for hardware video acceleration, used by NVIDIA GPUs from Fermi onwards.

For pre-2007 video cards see [XvMC](https://wiki.archlinux.org/title/XvMC "XvMC"). For comprehensive overview of driver and application support see [#Comparison tables](#Comparison_tables).

Installation
------------

### Intel

[Intel graphics](https://wiki.archlinux.org/title/Intel_graphics "Intel graphics") open-source drivers support VA-API:

*   HD Graphics series starting from [Broadwell](https://github.com/intel/media-driver/#supported-platforms) [(2014)](https://en.wikipedia.org/wiki/Template:Intel_processor_roadmap "wikipedia:Template:Intel processor roadmap") and newer are supported by [Coffee Lake](https://archlinux.org/packages/?>intel-media-driver</a>.</li>
    <li>GMA 4500 (2008) and newer GPUs, including HD Graphics up to <a href= "wikipedia:Coffee Lake") (2017) are supported by [libva-intel-driver-g45-h264](https://archlinux.org/packages/?>libva-intel-driver</a>.</li>
    <li>GMA 4500 H.264 decoding is supported by <a rel=)AUR, see [Intel#Hardware accelerated H.264 decoding on GMA 4500](https://wiki.archlinux.org/title/Intel#Hardware_accelerated_H.264_decoding_on_GMA_4500 "Intel").
*   Haswell refresh to Skylake VP9 decoding and Broadwell to Skylake hybrid VP8 encoding is supported by [intel-hybrid-codec-driver](https://aur.archlinux.org/packages/intel-hybrid-codec-driver/)AUR.
*   Skylake or later also need [VAAPI supported hardware and features](https://archlinux.org/packages/?>linux-firmware</a>.</li></ul>
    <p>Also see <a rel=).
    
    ### NVIDIA
    
    [Nouveau](https://wiki.archlinux.org/title/Nouveau "Nouveau") open-source driver supports both VA-API and VDPAU:
    
    *   GeForce 8 series and newer GPUs up until GeForce GTX 750 are supported by [Requires](https://archlinux.org/packages/?>libva-mesa-driver</a> and <a rel=) [nouveau-fw](https://aur.archlinux.org/packages/nouveau-fw/)AUR firmware package, presently extracted from the NVIDIA binary driver.
    
    [NVIDIA](https://wiki.archlinux.org/title/NVIDIA "NVIDIA") proprietary driver supports via [GeForce 8 series](https://archlinux.org/packages/?>nvidia-utils</a>:
    </p>
    <ul><li>VDPAU on <a href= "wikipedia:GeForce 8 series") and newer GPUs;
    
*   NVDECODE on [Fermi](https://en.wikipedia.org/wiki/Fermi_(microarchitecture) "wikipedia:Fermi (microarchitecture)") and newer GPUs [[1]](https://developer.download.nvidia.com/assets/cuda/files/NVIDIA_Video_Decoder.pdf);
*   NVENCODE on [Kepler](https://en.wikipedia.org/wiki/Kepler_(microarchitecture) "wikipedia:Kepler (microarchitecture)") and newer GPUs.

### ATI/AMD

[ATI](https://wiki.archlinux.org/title/ATI "ATI") and [AMDGPU](https://wiki.archlinux.org/title/AMDGPU "AMDGPU") open-source drivers support both VA-API and VDPAU:

*   VA-API on Radeon HD 2000 and newer GPUs is supported by [AMDGPU PRO](https://archlinux.org/packages/?>libva-mesa-driver</a>.</li>
    <li>VDPAU on Radeon R300 and newer GPUs is supported by <a rel=) proprietary driver is built on top of AMDGPU driver and supports both VA-API and VDPAU.
    
    ### Translation layers
    
    *   **libva-vdpau-driver** — A VDPAU-based backend for VA-API.
    
    [https://cgit.freedesktop.org/vaapi/vdpau-driver](https://cgit.freedesktop.org/vaapi/vdpau-driver) || [libva-vdpau-driver-chromium](https://archlinux.org/packages/?>libva-vdpau-driver</a>, <a rel=)AUR, [libva-vdpau-driver-vp9-git](https://aur.archlinux.org/packages/libva-vdpau-driver-vp9-git/)AUR
    
    *   **libvdpau-va-gl** — VDPAU driver with OpenGL/VAAPI backend. H.264 only.
    
    [https://github.com/i-rinat/libvdpau-va-gl](https://github.com/i-rinat/libvdpau-va-gl) || [CUDA](https://archlinux.org/packages/?>libvdpau-va-gl</a></dd></dl>
    <ul><li><b>nvidia-vaapi-driver</b> — A <a href=) NVDECODE based backend for VA-API.
    

[https://github.com/elFarto/nvidia-vaapi-driver/](https://github.com/elFarto/nvidia-vaapi-driver/) || [libva-nvidia-driver](https://aur.archlinux.org/packages/libva-nvidia-driver/)AUR

Verification
------------

Your system may work perfectly out-of-the-box without needing any configuration. Therefore it is a good idea to start with this section to see that it is the case.

**Tip:**

*   [mpv](https://wiki.archlinux.org/title/Mpv#Hardware_video_acceleration "Mpv") with its command-line support is great for testing hardware acceleration. Look at the log of `mpv --hwdec=auto _video_filename_` and see [hwdec](https://mpv.io/manual/stable/#options-hwdec) for more details.
*   For Intel GPU, use [[2]](https://archlinux.org/packages/?>intel-gpu-tools</a> and run <code>intel_gpu_top</code> as root to monitor the GPU activity during video playback for example. The video bar being above 0% indicates GPU video decoder/encoder usage.</li>
    <li>For AMD GPU, use <a rel=).
*   For any GPU, you can compare CPU usage with a tool like [Verifying VA-API](https://archlinux.org/packages/?>htop</a>. Especially for higher resolution videos (4k+), CPU usage when VA-API is enabled and working should be dramatically lower on laptops and other relatively low-power devices.</li></ul>
    
    <h3 id=)
    
    [Verify the settings for VA-API by running `vainfo`, which is provided by](https://archlinux.org/packages/?>htop</a>. Especially for higher resolution videos (4k+), CPU usage when VA-API is enabled and working should be dramatically lower on laptops and other relatively low-power devices.</li></ul>
    
    <h3 id=) [$ vainfo](https://archlinux.org/packages/?>libva-utils</a>:
    </p>
    <pre data-darkreader-inline-border-bottom=)
    
    ```
    [libva info: VA-API version 0.39.4
    libva info: va_getDriverName() returns 0
    libva info: Trying to open /usr/lib/dri/i965_drv_video.so
    libva info: Found init function __vaDriverInit_0_39
    libva info: va_openDriver() returns 0
    vainfo: VA-API version: 0.39 (libva 1.7.3)
    vainfo: Driver version: Intel i965 driver for Intel(R) Skylake - 1.7.3
    vainfo: Supported profile and entrypoints
          VAProfileMPEG2Simple            :	VAEntrypointVLD
          VAProfileMPEG2Simple            :	VAEntrypointEncSlice
          VAProfileMPEG2Main              :	VAEntrypointVLD
          VAProfileMPEG2Main              :	VAEntrypointEncSlice
          VAProfileH264ConstrainedBaseline:	VAEntrypointVLD
          VAProfileH264ConstrainedBaseline:	VAEntrypointEncSlice
          VAProfileH264ConstrainedBaseline:	VAEntrypointEncSliceLP
          VAProfileH264Main               :	VAEntrypointVLD
          VAProfileH264Main               :	VAEntrypointEncSlice
          VAProfileH264Main               :	VAEntrypointEncSliceLP
          VAProfileH264High               :	VAEntrypointVLD
          VAProfileH264High               :	VAEntrypointEncSlice
          VAProfileH264High               :	VAEntrypointEncSliceLP
          VAProfileH264MultiviewHigh      :	VAEntrypointVLD
          VAProfileH264MultiviewHigh      :	VAEntrypointEncSlice
          VAProfileH264StereoHigh         :	VAEntrypointVLD
          VAProfileH264StereoHigh         :	VAEntrypointEncSlice
          VAProfileVC1Simple              :	VAEntrypointVLD
          VAProfileVC1Main                :	VAEntrypointVLD
          VAProfileVC1Advanced            :	VAEntrypointVLD
          VAProfileNone                   :	VAEntrypointVideoProc
          VAProfileJPEGBaseline           :	VAEntrypointVLD
          VAProfileJPEGBaseline           :	VAEntrypointEncPicture
          VAProfileVP8Version0_3          :	VAEntrypointVLD
          VAProfileVP8Version0_3          :	VAEntrypointEncSlice
          VAProfileHEVCMain               :	VAEntrypointVLD
          VAProfileHEVCMain               :	VAEntrypointEncSlice](https://archlinux.org/packages/?>libva-utils</a>:
    </p>
    <pre data-darkreader-inline-border-bottom=) 
    ```
    
    [`VAEntrypointVLD` means that your card is capable to decode this format, `VAEntrypointEncSlice` means that you can encode to this format.
    
    In this example the `i965` driver is used, as you can see in this line:
    
    ```
    vainfo: Driver version: Intel i965 driver for Intel(R) Skylake - 1.7.3
    
    
    ```
    
    If the following error is displayed when running `vainfo`:
    
    ```
    libva info: va_openDriver() returns -1
    vaInitialize failed with error code -1 (unknown libva error),exit
    
    
    ```](https://archlinux.org/packages/?>libva-utils</a>:
    </p>
    <pre data-darkreader-inline-border-bottom=) 
    
    [You need to configure the correct driver, see](https://archlinux.org/packages/?>libva-utils</a>:
    </p>
    <pre data-darkreader-inline-border-bottom=) [#Configuring VA-API](#Configuring_VA-API).
    
    ### Verifying VDPAU
    
    Install [$ vdpauinfo](https://archlinux.org/packages/?>vdpauinfo</a> to verify if the VDPAU driver is loaded correctly and retrieve a full report of the configuration:
    </p>
    <pre data-darkreader-inline-border-bottom=)
    
    ```
    [display: :0   screen: 0
    API version: 1
    Information string: G3DVL VDPAU Driver Shared Library version 1.0
    
    Video surface:
    
    name   width height types
    -------------------------------------------
    420    16384 16384  NV12 YV12 
    422    16384 16384  UYVY YUYV 
    444    16384 16384  Y8U8V8A8 V8U8Y8A8 
    
    Decoder capabilities:
    
    name                        level macbs width height
    ----------------------------------------------------
    MPEG1                          --- not supported ---
    MPEG2_SIMPLE                    3  9216  2048  1152
    MPEG2_MAIN                      3  9216  2048  1152
    H264_BASELINE                  41  9216  2048  1152
    H264_MAIN                      41  9216  2048  1152
    H264_HIGH                      41  9216  2048  1152
    VC1_SIMPLE                      1  9216  2048  1152
    VC1_MAIN                        2  9216  2048  1152
    VC1_ADVANCED                    4  9216  2048  1152
    ...](https://archlinux.org/packages/?>vdpauinfo</a> to verify if the VDPAU driver is loaded correctly and retrieve a full report of the configuration:
    </p>
    <pre data-darkreader-inline-border-bottom=) 
    ```
    
    [
    
    Configuration
    -------------
    
    ](https://archlinux.org/packages/?>vdpauinfo</a> to verify if the VDPAU driver is loaded correctly and retrieve a full report of the configuration:
    </p>
    <pre data-darkreader-inline-border-bottom=)
    
    [Although the video driver should automatically enable hardware video acceleration support for both VA-API and VDPAU, it may be needed to configure VA-API/VDPAU manually. Only continue to this section if you went through](https://archlinux.org/packages/?>vdpauinfo</a> to verify if the VDPAU driver is loaded correctly and retrieve a full report of the configuration:
    </p>
    <pre data-darkreader-inline-border-bottom=) [#Verification](#Verification).
    
    The default driver names, used if there is no other configuration present, are guess by the system. However, they are often hacked together and may not work. You can see the guessed values by running:
    
    ```
    $ grep -iE 'vdpau | dri driver' /var/log/Xorg.0.log
    
    ```
    
    ```
    (II) RADEON(0): [DRI2] DRI driver: radeonsi
    (II) RADEON(0): [DRI2] VDPAU driver: radeonsi
    
    
    ```
    
    In this case `radeonsi` is the default for both VA-API and VDPAU.
    
    **Note:** If you use [GDM](https://wiki.archlinux.org/title/GDM "GDM"), run `journalctl -b --grep='vdpau | dri driver'` as root instead.
    
    This does not represent the _configuration_ however. The values above will not change even if you override them.
    
    ### Configuring VA-API
    
    You can override the [driver](https://www.freedesktop.org/wiki/Software/vaapi/#driversback-endsthatimplementva-api) for VA-API by using the `LIBVA_DRIVER_NAME` [environment variable](https://wiki.archlinux.org/title/Environment_variable "Environment variable"):
    
    *   [Intel graphics](https://wiki.archlinux.org/title/Intel_graphics "Intel graphics"):
        *   For [Nouveau](https://archlinux.org/packages/?>libva-intel-driver</a> use <code>i965</code>.</li>
            <li>For <a rel=) use `nouveau`.
        *   For [NVIDIA](https://wiki.archlinux.org/title/NVIDIA "NVIDIA") VDPAU use `vdpau`.
        *   For [NVIDIA](https://wiki.archlinux.org/title/NVIDIA "NVIDIA") NVDECODE use `nvidia`.
    *   AMD:
        *   For [AMDGPU](https://wiki.archlinux.org/title/AMDGPU "AMDGPU") driver use `radeonsi`.
    
    **Note:**
    
    *   You can find the installed drivers in `/usr/lib/dri/`. They are used as `/usr/lib/dri/**${LIBVA_DRIVER_NAME}**_drv_video.so`.
    *   Some drivers are installed several times under different names for compatibility reasons. You can see which by running `sha1sum /usr/lib/dri/* | sort`.
    *   `LIBVA_DRIVERS_PATH` can be used to overrule the VA-API drivers location.
    *   Since version 12.0.1 [Configuring VDPAU](https://archlinux.org/packages/?>libva-mesa-driver</a> provides <code>radeonsi</code> instead of <code>gallium</code>.</li></ul>
        
        <h3 id=)
        
        [You can override the driver for VDPAU by using the `VDPAU_DRIVER`](https://archlinux.org/packages/?>libva-mesa-driver</a> provides <code>radeonsi</code> instead of <code>gallium</code>.</li></ul>
        
        <h3 id=) [environment variable](https://wiki.archlinux.org/title/Environment_variable "Environment variable").
        
        The correct driver name depends on your setup:
        
        *   For Intel graphics you [need](#Failed_to_open_VDPAU_backend) to set it to `va_gl`.
        *   For the open source AMD driver set it to the proper driver version depending on your GPU, see [#Verification](#Verification).
        *   For the open source Nouveau driver set it to `nouveau`.
        *   For NVIDIA's proprietary version set it to `nvidia`.
        
        **Note:**
        
        *   You can find the installed drivers in `/usr/lib/vdpau/`. They are used as `/usr/lib/vdpau/libvdpau_**${VDPAU_DRIVER}**.so`.
        *   Some drivers are installed several times under different names for compatibility reasons. You can see which by running `sha1sum /usr/lib/vdpau/*`.
        *   For hybrid setups (both NVIDIA and AMD), it may be necessary to set the `DRI_PRIME` [environment variable](https://wiki.archlinux.org/title/Environment_variable "Environment variable"). For more information see [PRIME](https://wiki.archlinux.org/title/PRIME "PRIME").
        
        ### Configuring applications
        
        Multimedia frameworks:
        
        *   [FFmpeg#Hardware video acceleration](https://wiki.archlinux.org/title/FFmpeg#Hardware_video_acceleration "FFmpeg")
        *   [GStreamer#Hardware video acceleration](https://wiki.archlinux.org/title/GStreamer#Hardware_video_acceleration "GStreamer")
        
        Video players:
        
        *   [Browser plugins#Adobe Flash Player](https://wiki.archlinux.org/title/Browser_plugins#Adobe_Flash_Player "Browser plugins")
        *   [Kodi#Hardware video acceleration](https://wiki.archlinux.org/title/Kodi#Hardware_video_acceleration "Kodi")
        *   [MPlayer#Hardware video acceleration](https://wiki.archlinux.org/title/MPlayer#Hardware_video_acceleration "MPlayer")
        *   [mpv#Hardware video acceleration](https://wiki.archlinux.org/title/Mpv#Hardware_video_acceleration "Mpv")
        *   [VLC media player#Hardware video acceleration](https://wiki.archlinux.org/title/VLC_media_player#Hardware_video_acceleration "VLC media player")
        
        Web browsers:
        
        *   [Chromium#Hardware video acceleration](https://wiki.archlinux.org/title/Chromium#Hardware_video_acceleration "Chromium")
        *   [Firefox#Hardware video acceleration](https://wiki.archlinux.org/title/Firefox#Hardware_video_acceleration "Firefox")
        *   [GNOME/Web#Video](https://wiki.archlinux.org/title/GNOME/Web#Video "GNOME/Web")
        
        Troubleshooting
        ---------------
        
        ### Failed to open VDPAU backend
        
        You need to set `VDPAU_DRIVER` variable to point to correct driver. See [#Configuring VDPAU](#Configuring_VDPAU).
        
        ### VAAPI init failed
        
        An error along the lines of `libva: /usr/lib/dri/i965_drv_video.so init failed` is encountered. This can happen because of improper detection of Wayland. One solution is to unset `$DISPLAY` so that mpv, MPlayer, VLC, etc. do not assume it is X11. Another mpv-specific solution is to add the parameter `--gpu-context=wayland`.
        
        ### Video decoding corruption or distortion with AMDGPU driver
        
        When experiencing video decoding corruption or distortion with [AMDGPU](https://wiki.archlinux.org/title/AMDGPU "AMDGPU") driver, set `allow_rgb10_configs=false` as [environment variable](https://wiki.archlinux.org/title/Environment_variable "Environment variable") or `driconf`. [[3]](https://bugs.freedesktop.org/show_bug.cgi?id=106490)
        
        Comparison tables
        -----------------
        
        ### VA-API drivers
        
        <table><tbody><tr><th>Codec</th><th><a rel="nofollow" href="https://archlinux.org/packages/?>libva-intel-driver</a> <a rel=" nofollow"="">[4]</a></th><th><a rel="nofollow" href="https://archlinux.org/packages/?>intel-media-driver</a> <a rel=" nofollow"="">[5]</a></th><th><a rel="nofollow" href="https://archlinux.org/packages/?>libva-mesa-driver</a> <a rel=" nofollow"="">[6]</a> <a rel="nofollow" href="https://nouveau.freedesktop.org/wiki/VideoAcceleration/">[7]</a></th><th><a rel="nofollow" href="https://archlinux.org/packages/?>libva-vdpau-driver</a> <br> (VDPAU adapter)
        </th>
        <th><a rel=" nofollow"="">libva-nvidia-driver</a><sup><small>AUR</small></sup><br>(NVDECODE adapter)</th></tr><tr><th colspan="6">Decoding</th></tr><tr><th>MPEG-2</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GMA 4500 and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broadwell and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon HD 6000 and newer<br>GeForce 8 and newer<sup>1</sup></td><td rowspan="6">See <a href="#VDPAU_drivers">#VDPAU drivers</a></td><td>See <a href="#NVIDIA_driver_only">#NVIDIA driver only</a></td></tr><tr><th>H.263/MPEG-4 Visual<sup>4</sup></th><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon HD 6000 and newer</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No<sup>6</sup></td></tr><tr><th>VC-1</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Sandy Bridge and newer</td><td rowspan="2" data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broadwell and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon HD 2000 and newer<br>GeForce 9300 and newer<sup>1</sup></td><td rowspan="3">See <a href="#NVIDIA_driver_only">#NVIDIA driver only</a></td></tr><tr><th>H.264/MPEG-4 AVC</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GMA 4500<sup>2</sup>, Ironlake and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon HD 2000 and newer<br>GeForce 8 and newer<sup>1</sup></td></tr><tr><th>H.265/HEVC 8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Cherryview/Braswell and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Skylake and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon R9 Fury and newer</td></tr><tr><th>H.265/HEVC 10bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broxton and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broxton/Apollo Lake and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon 400 and newer</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No<sup>6</sup></td></tr><tr><th>VP8</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broadwell and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broadwell and newer</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td rowspan="2">See <a href="#NVIDIA_driver_only">#NVIDIA driver only</a></td></tr><tr><th>VP9 8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broxton and newer<br>Hybrid: Haswell refresh to Skylake<sup>3</sup></td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broxton/Apollo Lake and newer</td><td rowspan="2" data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Raven Ridge and newer</td><td>See <a href="#VDPAU_drivers">#VDPAU drivers</a><sup>5</sup></td></tr><tr><th>VP9 10bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Kaby Lake and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Kaby Lake and newer</td><td rowspan="2" data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td rowspan="2" data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No<sup>6</sup></td></tr><tr><th>AV1 8-bit &amp; 10-bit</th><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Tiger Lake and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon RX 6000 and newer</td></tr><tr><th colspan="6">Encoding</th></tr><tr><th>MPEG-2</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Ivy Bridge and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broadwell and newer<br>except Broxton/Apollo Lake</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td rowspan="7" data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td rowspan="7" data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No<sup>6</sup></td></tr><tr><th>H.264/MPEG-4 AVC</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Sandy Bridge and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Broadwell and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon HD 7000 and newer</td></tr><tr><th>H.265/HEVC 8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Skylake and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Skylake and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon 400 and newer</td></tr><tr><th>H.265/HEVC 10bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Kaby Lake and newer</td><td rowspan="2" data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Kaby Lake and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Raven Ridge and newer</td></tr><tr><th>VP8</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Cherryview/Braswell and newer<br>Hybrid: Haswell to Skylake<sup>3</sup></td><td rowspan="3" data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td></tr><tr><th>VP9 8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Kaby Lake and newer</td><td rowspan="2" data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Icelake and newer</td></tr><tr><th>VP9 10bit</th><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td></tr></tbody></table>
        
        *   1 Up until GeForce GTX 750.
        *   2 Supported by [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/)AUR instead.
        *   3 Hybrid VP8 encoder and VP9 decoder supported by [intel-hybrid-codec-driver](https://aur.archlinux.org/packages/intel-hybrid-codec-driver/)AUR.
        *   4 MPEG-4 Part 2 is disabled by default due to VAAPI limitations. Set the [environment variable](https://wiki.archlinux.org/title/Environment_variable "Environment variable") `VAAPI_MPEG4_ENABLED=true` to try to use it anyway.
        *   5 Experimental VP9 support provided by [libva-vdpau-driver-vp9-git](https://aur.archlinux.org/packages/libva-vdpau-driver-vp9-git/)AUR instead.
        *   6 NVIDIA CUDA adapter codec support is in active development and susceptible to change [[8]](https://github.com/elFarto/nvidia-vaapi-driver/#codec-support).
        
        ### VDPAU drivers
        
        <table><tbody><tr><th>Codec</th><th>Color<br>depth</th><th><a rel="nofollow" href="https://archlinux.org/packages/?>mesa-vdpau</a> <a rel=" nofollow"="">[9]</a> <a rel="nofollow" href="https://nouveau.freedesktop.org/wiki/VideoAcceleration/">[10]</a></th><th><a rel="nofollow" href="https://archlinux.org/packages/?>nvidia-utils</a>
        </th>
        <th><a rel=" nofollow"="" 5"="">Decoding</a></th></tr><tr><th>MPEG-2</th><th>8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon R300 and newer<br>GeForce 8 and newer<sup>1</sup></td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GeForce 8 and newer</td><td rowspan="3" data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td></tr><tr><th>H.263/MPEG-4 Visual</th><th>8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon HD 6000 and newer<br>GeForce 200 and newer<sup>1</sup></td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GeForce 200 and newer</td></tr><tr><th>VC-1</th><th>8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon HD 2000 and newer<br>GeForce 9300 and newer<sup>1</sup></td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GeForce 8 and newer<sup>2</sup></td></tr><tr><th>H.264/MPEG-4 AVC</th><th>8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon HD 2000 and newer<br>GeForce 8 and newer<sup>1</sup></td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GeForce 8 and newer</td><td>See <a href="#VA-API_drivers">#VA-API drivers</a></td></tr><tr><th rowspan="2">H.265/HEVC</th><th>8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon R9 Fury and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GeForce 900 and newer<sup>3</sup></td><td rowspan="6" data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td></tr><tr><th>10bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Radeon 400 and newer</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No<sup>4</sup></td></tr><tr><th rowspan="2">VP9</th><th>8bit</th><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GeForce 900 and newer<sup>3</sup></td></tr><tr><th>10bit</th><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No<sup>4</sup></td></tr><tr><th rowspan="2">AV1</th><th>8bit</th><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GeForce 30 and newer<sup>5</sup></td></tr><tr><th>10bit</th><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No<sup>4</sup></td></tr></tbody></table>
        
        *   1 Up until GeForce GTX 750.
        *   2 [Except](https://en.wikipedia.org/wiki/Nvidia_PureVideo "wikipedia:Nvidia PureVideo") GeForce 8800 Ultra, 8800 GTX, 8800 GTS (320/640 MB).
        *   3 Except GeForce GTX 970 and GTX 980.
        *   4 NVIDIA implementation is limited to 8-bit streams [[11]](https://forums.developer.nvidia.com/t/vdpau-expose-hevc-main10-support-where-available-on-die/43163) [[12]](https://us.download.nvidia.com/XFree86/Linux-x86_64/410.57/README/vdpausupport.html#vdpau-implementation-limits).
        *   5 Starting with driver version 510.[[13]](https://www.phoronix.com/scan.php?page=news_item&px=NVIDIA-510-Linux-Beta)
        
        ### NVIDIA driver only
        
        <table><tbody><tr><th rowspan="2">Codec</th><th colspan="2"><a rel="nofollow" href="https://archlinux.org/packages/?>nvidia-utils</a> <a rel=" nofollow"="">[14]</a></th></tr><tr><th>NVDECODE</th><th>NVENCODE</th></tr><tr><th>MPEG-2</th><td rowspan="3" data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Fermi and newer<sup>1</sup></td><td rowspan="2" data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td></tr><tr><th>VC-1</th></tr><tr><th>H.264/MPEG-4 AVC</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Kepler and newer<sup>2</sup></td></tr><tr><th>H.265/HEVC 8bit</th><td rowspan="2" data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Maxwell (GM206) and newer</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Maxwell (2nd Gen) and newer</td></tr><tr><th>H.265/HEVC 10bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Pascal and newer</td></tr><tr><th>VP8</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Maxwell (2nd Gen) and newer</td><td rowspan="4" data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td></tr><tr><th>VP9 8bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Maxwell (GM206) and newer</td></tr><tr><th>VP9 10bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Pascal and newer</td></tr><tr><th>AV1 8bit &amp; 10bit</th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Ampere and newer<sup>3</sup></td></tr></tbody></table>
        
        *   1 Except GM108 (not supported)
        *   2 Except GM108 and GP108 (not supported)
        *   3 Except A100 (not supported)
        
        ### Application support
        
        <table><tbody><tr><th rowspan="2">Application</th><th colspan="3">Decoding</th><th colspan="2">Encoding</th><th rowspan="2">Documentation</th></tr><tr><th>VA-API</th><th>VDPAU</th><th>NVDECODE</th><th>VA-API</th><th>NVENCODE</th></tr><tr><th><a href="https://wiki.archlinux.org/title/FFmpeg" title="FFmpeg">FFmpeg</a></th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td><a href="https://wiki.archlinux.org/title/FFmpeg#Hardware_video_acceleration" title="FFmpeg">FFmpeg#Hardware video acceleration</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/GStreamer" title="GStreamer">GStreamer</a></th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes<sup>1</sup></td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes<sup>1</sup></td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td><a href="https://wiki.archlinux.org/title/GStreamer#Hardware_video_acceleration" title="GStreamer">GStreamer#Hardware video acceleration</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/Kodi" title="Kodi">Kodi</a></th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td><a href="https://wiki.archlinux.org/title/Kodi#Hardware_video_acceleration" title="Kodi">Kodi#Hardware video acceleration</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/Mpv" title="Mpv">mpv</a></th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td><a href="https://wiki.archlinux.org/title/Mpv#Hardware_video_acceleration" title="Mpv">mpv#Hardware video acceleration</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/VLC_media_player" title="VLC media player">VLC media player</a></th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td><a href="https://wiki.archlinux.org/title/VLC_media_player#Hardware_video_acceleration" title="VLC media player">VLC media player#Hardware video acceleration</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/MPlayer" title="MPlayer">MPlayer</a></th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes<sup>2</sup></td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td><a href="https://wiki.archlinux.org/title/MPlayer#Hardware_video_acceleration" title="MPlayer">MPlayer#Hardware video acceleration</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/Flash" title="Flash">Flash</a></th><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No<sup>3</sup></td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes<sup>3</sup></td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">–</td><td><a href="https://wiki.archlinux.org/title/Browser_plugins#Adobe_Flash_Player" title="Browser plugins">Browser plugins#Adobe Flash Player</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/Chromium" title="Chromium">Chromium</a></th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes<sup>4</sup></td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes<sup>4</sup></td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td><a href="https://wiki.archlinux.org/title/Chromium#Hardware_video_acceleration" title="Chromium">Chromium#Hardware video acceleration</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/Firefox" title="Firefox">Firefox</a></th><td data-sort-value="5" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">Yes</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color=""><a rel="nofollow" href="https://bugzilla.mozilla.org/show_bug.cgi?id=1658900">No</a></td><td data-sort-value="1" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">No</td><td><a href="https://wiki.archlinux.org/title/Firefox#Hardware_video_acceleration" title="Firefox">Firefox#Hardware video acceleration</a></td></tr><tr><th><a href="https://wiki.archlinux.org/title/GNOME/Web" title="GNOME/Web">GNOME/Web</a></th><td colspan="3" data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">GStreamer</td><td data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">?</td><td data-darkreader-inline-bgimage="" data-darkreader-inline-bgcolor="" data-darkreader-inline-color="">?</td><td><a href="https://wiki.archlinux.org/title/GNOME/Web#Video" title="GNOME/Web">GNOME/Web#Video</a></td></tr></tbody></table>
        
        *   1 GStreamer [uses a whitelist](https://blogs.igalia.com/vjaquez/2018/03/28/gstreamer-va-api-troubleshooting/) of VA-API drivers. To ignore the whitelist, see [GStreamer#Ignore driver whitelist](https://wiki.archlinux.org/title/GStreamer#Ignore_driver_whitelist "GStreamer").
        *   2 VA-API support provided by [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/)AUR instead.
        *   3 VDPAU is supported only by NPAPI plugin. PPAPI plugin to NPAPI browser experimental adapter is available that provides partial VA-API and VDPAU acceleration.
        *   4 Xorg only. Wayland is not supported. XWayland exhibits choppiness [FS#67035](https://bugs.archlinux.org/task/67035).