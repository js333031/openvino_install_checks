# openvino_install_checks

Add user to render group and video groups. Also set the driver name env variable:
```
# vainfo results in errors.
$ id student
uid=1001(student) gid=1001(student) groups=1001(student)

sudo usermod -a -G render student

$ id student
uid=1001(student) gid=1001(student) groups=1001(student),110(render)

~$ id
uid=1001(student) gid=1001(student) groups=1001(student),110(render)
student@nuc21:~$ vainfo
Trying display: wayland
Trying display: x11
libva info: VA-API version 1.20.0
libva error: vaGetDriverNames() failed with unknown libva error
vaInitialize failed with error code -1 (unknown libva error),exit
student@nuc21:~$

$ id
uid=1001(student) gid=1001(student) groups=1001(student),44(video),110(render)

< still get the vainfo errors >

export LIBVA_DRIVER_NAME=iHD

Now, vainfo is successful.

```
System information:
```
student@nuc21:~$ cat /etc/issue.net
Ubuntu 22.04.4 LTS
student@nuc21:~$

$ cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-6.2.8-060208-generic root=UUID=8fd72d1d-2a9a-4a32-b8ba-3d561569fc6d ro text i915.force_probe=5690

```

Verify Install:
https://dgpu-docs.intel.com/driver/installation.html#verify-install

Working kernel:
```
student@nuc21:~$ cat /etc/issue.net
Ubuntu 22.04.4 LTS

student@nuc21:~$ clinfo -l
Platform #0: Intel(R) OpenCL Graphics
 `-- Device #0: Intel(R) Arc(TM) A770M Graphics
Platform #1: Intel(R) OpenCL Graphics
 `-- Device #0: Intel(R) Iris(R) Xe Graphics
Platform #2: Intel(R) OpenCL
 `-- Device #0: 12th Gen Intel(R) Core(TM) i7-12700H
Platform #3: Intel(R) FPGA Emulation Platform for OpenCL(TM)
 `-- Device #0: Intel(R) FPGA Emulation Device
student@nuc21:~$


student@nuc21:~$ cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-6.2.8-060208-generic root=UUID=8fd72d1d-2a9a-4a32-b8ba-3d561569fc6d ro text i915.force_probe=5690

student@nuc21:~$ inxi -G
Graphics:
  Device-1: Intel Alder Lake-P Integrated Graphics driver: i915 v: kernel
  Device-2: Intel driver: i915 v: kernel
  Display: server: X.org v: 1.21.1.4 driver: X: loaded: vesa
    unloaded: fbdev,modesetting gpu: i915,i915 resolution: 1: 1920x1080~60Hz
    2: 1920x1080~60Hz
  OpenGL: renderer: llvmpipe (LLVM 15.0.7 256 bits)
    v: 4.5 Mesa 24.1.0-devel (git-0fcdf7bf33)
student@nuc21:~$

student@nuc21:~$ vainfo
Trying display: wayland
Trying display: x11
libva info: VA-API version 1.20.0
libva error: vaGetDriverNames() failed with unknown libva error
libva info: User environment variable requested driver 'iHD'
libva info: Trying to open /usr/lib/x86_64-linux-gnu/dri/iHD_drv_video.so
libva info: Found init function __vaDriverInit_1_20
libva info: va_openDriver() returns 0
vainfo: VA-API version: 1.20 (libva 2.20.0)
vainfo: Driver version: Intel iHD driver for Intel(R) Gen Graphics - 23.4.3 ()
vainfo: Supported profile and entrypoints
      VAProfileNone                   : VAEntrypointVideoProc
      VAProfileNone                   : VAEntrypointStats
      VAProfileMPEG2Simple            : VAEntrypointVLD
      VAProfileMPEG2Simple            : VAEntrypointEncSlice
      VAProfileMPEG2Main              : VAEntrypointVLD
      VAProfileMPEG2Main              : VAEntrypointEncSlice
      VAProfileH264Main               : VAEntrypointVLD
      VAProfileH264Main               : VAEntrypointEncSlice
      VAProfileH264Main               : VAEntrypointFEI
      VAProfileH264Main               : VAEntrypointEncSliceLP
      VAProfileH264High               : VAEntrypointVLD
      VAProfileH264High               : VAEntrypointEncSlice
      VAProfileH264High               : VAEntrypointFEI
      VAProfileH264High               : VAEntrypointEncSliceLP
      VAProfileVC1Simple              : VAEntrypointVLD
      VAProfileVC1Main                : VAEntrypointVLD
      VAProfileVC1Advanced            : VAEntrypointVLD
      VAProfileJPEGBaseline           : VAEntrypointVLD
      VAProfileJPEGBaseline           : VAEntrypointEncPicture
      VAProfileH264ConstrainedBaseline: VAEntrypointVLD
      VAProfileH264ConstrainedBaseline: VAEntrypointEncSlice
      VAProfileH264ConstrainedBaseline: VAEntrypointFEI
      VAProfileH264ConstrainedBaseline: VAEntrypointEncSliceLP
      VAProfileVP8Version0_3          : VAEntrypointVLD
      VAProfileHEVCMain               : VAEntrypointVLD
      VAProfileHEVCMain               : VAEntrypointEncSlice
      VAProfileHEVCMain               : VAEntrypointFEI
      VAProfileHEVCMain               : VAEntrypointEncSliceLP
      VAProfileHEVCMain10             : VAEntrypointVLD
      VAProfileHEVCMain10             : VAEntrypointEncSlice
      VAProfileHEVCMain10             : VAEntrypointEncSliceLP
      VAProfileVP9Profile0            : VAEntrypointVLD
      VAProfileVP9Profile0            : VAEntrypointEncSliceLP
      VAProfileVP9Profile1            : VAEntrypointVLD
      VAProfileVP9Profile1            : VAEntrypointEncSliceLP
      VAProfileVP9Profile2            : VAEntrypointVLD
      VAProfileVP9Profile2            : VAEntrypointEncSliceLP
      VAProfileVP9Profile3            : VAEntrypointVLD
      VAProfileVP9Profile3            : VAEntrypointEncSliceLP
      VAProfileHEVCMain12             : VAEntrypointVLD
      VAProfileHEVCMain12             : VAEntrypointEncSlice
      VAProfileHEVCMain422_10         : VAEntrypointVLD
      VAProfileHEVCMain422_10         : VAEntrypointEncSlice
      VAProfileHEVCMain422_12         : VAEntrypointVLD
      VAProfileHEVCMain422_12         : VAEntrypointEncSlice
      VAProfileHEVCMain444            : VAEntrypointVLD
      VAProfileHEVCMain444            : VAEntrypointEncSliceLP
      VAProfileHEVCMain444_10         : VAEntrypointVLD
      VAProfileHEVCMain444_10         : VAEntrypointEncSliceLP
      VAProfileHEVCMain444_12         : VAEntrypointVLD
      VAProfileHEVCSccMain            : VAEntrypointVLD
      VAProfileHEVCSccMain            : VAEntrypointEncSliceLP
      VAProfileHEVCSccMain10          : VAEntrypointVLD
      VAProfileHEVCSccMain10          : VAEntrypointEncSliceLP
      VAProfileHEVCSccMain444         : VAEntrypointVLD
      VAProfileHEVCSccMain444         : VAEntrypointEncSliceLP
      VAProfileAV1Profile0            : VAEntrypointVLD
      VAProfileHEVCSccMain444_10      : VAEntrypointVLD
      VAProfileHEVCSccMain444_10      : VAEntrypointEncSliceLP
student@nuc21:~$

vainfo from specific device:

student@nuc21:~$ vainfo --display drm --device /dev/dri/renderD128
Trying display: drm
libva info: VA-API version 1.20.0
libva info: User environment variable requested driver 'iHD'
libva info: Trying to open /usr/lib/x86_64-linux-gnu/dri/iHD_drv_video.so
libva info: Found init function __vaDriverInit_1_20
libva info: va_openDriver() returns 0
vainfo: VA-API version: 1.20 (libva 2.20.0)
vainfo: Driver version: Intel iHD driver for Intel(R) Gen Graphics - 23.4.3 ()
vainfo: Supported profile and entrypoints
      VAProfileNone                   : VAEntrypointVideoProc
<snip>
      VAProfileHEVCSccMain444_10      : VAEntrypointEncSliceLP
student@nuc21:~$

student@nuc21:~$ vainfo --display drm --device /dev/dri/renderD129
Trying display: drm
libva info: VA-API version 1.20.0
libva info: User environment variable requested driver 'iHD'
libva info: Trying to open /usr/lib/x86_64-linux-gnu/dri/iHD_drv_video.so
libva info: Found init function __vaDriverInit_1_20
libva info: va_openDriver() returns 0
vainfo: VA-API version: 1.20 (libva 2.20.0)
vainfo: Driver version: Intel iHD driver for Intel(R) Gen Graphics - 23.4.3 ()
vainfo: Supported profile and entrypoints
      VAProfileNone                   : VAEntrypointVideoProc
      VAProfileNone                   : VAEntrypointStats
      VAProfileMPEG2Simple            : VAEntrypointVLD
<snip>
      VAProfileHEVCSccMain444         : VAEntrypointEncSliceLP
      VAProfileAV1Profile0            : VAEntrypointVLD
      VAProfileAV1Profile0            : VAEntrypointEncSliceLP
      VAProfileHEVCSccMain444_10      : VAEntrypointVLD
      VAProfileHEVCSccMain444_10      : VAEntrypointEncSliceLP
student@nuc21:~$
```

Wrong kernel:
```
$ uname -a
Linux nuc21 6.5.0-26-generic #26~22.04.1-Ubuntu SMP PREEMPT_DYNAMIC Tue Mar 12 10:22:43 UTC 2 x86_64 x86_64 x86_64 GNU/Linux


$ hwinfo --display
07: PCI 300.0: 0300 VGA compatible controller (VGA)
  [Created at pci.386]
  Unique ID: svHJ.77hoq_qsqUD
  Parent ID: GA8e.mr2N3fBJq5F
  SysFS ID: /devices/pci0000:00/0000:00:01.0/0000:01:00.0/0000:02:01.0/0000:03:00.0
  SysFS BusID: 0000:03:00.0
  Hardware Class: graphics card
  Device Name: "dGPU"
  Model: "Intel VGA compatible controller"
  Vendor: pci 0x8086 "Intel Corporation"
  Device: pci 0x5690
  SubVendor: pci 0x8086 "Intel Corporation"
  SubDevice: pci 0x3026
  Revision: 0x08
  Driver: "i915"
  Driver Modules: "i915"
  Memory Range: 0x6b000000-0x6bffffff (rw,non-prefetchable)
  Memory Range: 0x6000000000-0x63ffffffff (ro,non-prefetchable)
  Memory Range: 0x6c000000-0x6c1fffff (ro,non-prefetchable,disabled)
  IRQ: 204 (1410 events)
  Module Alias: "pci:v00008086d00005690sv00008086sd00003026bc03sc00i00"
  Driver Info #0:
    Driver Status: i915 is active
    Driver Activation Cmd: "modprobe i915"
  Config Status: cfg=new, avail=yes, need=no, active=unknown
  Attached to: #30 (PCI bridge)

31: PCI 02.0: 0300 VGA compatible controller (VGA)
  [Created at pci.386]
  Unique ID: _Znp.HMLUX1zIkGC
  SysFS ID: /devices/pci0000:00/0000:00:02.0
  SysFS BusID: 0000:00:02.0
  Hardware Class: graphics card
  Device Name: "GPU"
  Model: "Intel VGA compatible controller"
  Vendor: pci 0x8086 "Intel Corporation"
  Device: pci 0x46a6
  SubVendor: pci 0x8086 "Intel Corporation"
  SubDevice: pci 0x3026
  Revision: 0x0c
  Driver: "i915"
  Driver Modules: "i915"
  Memory Range: 0x644c000000-0x644cffffff (rw,non-prefetchable)
  Memory Range: 0x4000000000-0x400fffffff (ro,non-prefetchable)
  I/O Ports: 0x4000-0x403f (rw)
  Memory Range: 0x000c0000-0x000dffff (rw,non-prefetchable,disabled)
  IRQ: 203 (80 events)
  Module Alias: "pci:v00008086d000046A6sv00008086sd00003026bc03sc00i00"
  Driver Info #0:
    Driver Status: i915 is active
    Driver Activation Cmd: "modprobe i915"
  Config Status: cfg=new, avail=yes, need=no, active=unknown

Primary display adapter: #7
$

$ uname -a
Linux nuc21 6.5.0-26-generic #26~22.04.1-Ubuntu SMP PREEMPT_DYNAMIC Tue Mar 12 10:22:43 UTC 2 x86_64 x86_64 x86_64 GNU/Linux
$ clinfo | head -n 5
Number of platforms                               2
  Platform Name                                   Intel(R) OpenCL
  Platform Vendor                                 Intel(R) Corporation
  Platform Version                                OpenCL 3.0 LINUX
  Platform Profile                                FULL_PROFILE
$

$ vainfo
Trying display: wayland
Trying display: x11
libva info: VA-API version 1.20.0
libva error: vaGetDriverNames() failed with unknown libva error
vaInitialize failed with error code -1 (unknown libva error),exit
$

$ inxi -G
Graphics:
  Device-1: Intel Alder Lake-P Integrated Graphics driver: i915 v: backported
    to 6.5.0-26 from (b204f78969214) using backports I915_24.1.11_PSB_240117.14
  Device-2: Intel driver: i915 v: backported to 6.5.0-26 from
    (b204f78969214) using backports I915_24.1.11_PSB_240117.14
  Display: server: X.org v: 1.21.1.4 driver: X: loaded: vesa
    unloaded: fbdev,modesetting gpu: i915,i915 resolution: 1: 1920x1080~60Hz
    2: 1920x1080~60Hz
  OpenGL: renderer: llvmpipe (LLVM 15.0.7 256 bits)
    v: 4.5 Mesa 24.1.0-devel (git-0fcdf7bf33)
$
$ cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-6.5.0-26-generic root=UUID=8fd72d1d-2a9a-4a32-b8ba-3d561569fc6d ro text i915.force_probe=5690
$

```
References:
https://dgpu-docs.intel.com/driver/installation.html

