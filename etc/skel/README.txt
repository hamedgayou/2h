----------------------------------------------------------------

= APPLICATION USAGE HOW-TO =

Terminal gestures:

 - Pinch-zooming: resize console text.
 - Short tap: left mouse button click in compatible programs.
 - Long tap: open context menu.

Why console text can get messed up: due to serial console
nature, text resize actually does not change size of terminal
and interface could get messed up. Use command resize after
changing text size.

Preventing host sleep mode: if you need to run the virtual
machine while device screen is off, a wake lock should be
enabled. You can toggle it through the notification. Disabled
wake lock can lead to system clock appearing to be out-of-sync
or pausing of the whole VM.

Key shortcuts: application supports combinations of keys from
touch keyboard and Volume-Up/Volume-Down buttons. Volume-Down
emulates the Ctrl key and Volume-Up can be used to produce
special input:

 +====================+================================+
 | Key combination    | Produced input                 |
 +====================+================================+
 | Volume-Up .        | Ctrl \                         |
 | Volume-Up <1..9>   | F1, F2, ..., F9 keys           |
 | Volume-Up 0        | F10                            |
 | Volume-Up A        | Left arrow key                 |
 | Volume-Up B        | Alt B                          |
 | Volume-Up D        | Right arrow key                |
 | Volume-Up E        | Escape                         |
 | Volume-Up F        | Alt F                          |
 | Volume-Up H        | ~ the tilde character          |
 | Volume-Up K        | Toggle extra keys row          |
 | Volume-Up L        | | the pipe character           |
 | Volume-Up N        | Page down key                  |
 | Volume-Up P        | Page up key                    |
 | Volume-Up S        | Down arrow key                 |
 | Volume-Up T        | Tab key                        |
 | Volume-Up U        | _ the underscore character     |
 | Volume-Up V        | Show the volume control        |
 | Volume-Up W        | Up arrow key                   |
 | Volume-Up X        | Alt X                          |
 |____________________|________________________________|

Note that Volume-Up does not represent the Alt key even though
it is being used to emulate certain its combinations.

These key combinations can be used on a hardware keyboard to
trigger certain actions of the application:

 +=================+===============================+
 | Key combination | Action                        |
 +=================+===============================+
 | Ctrl Alt +      | Increase text size            |
 | Ctrl Alt -      | Reduce text size              |
 | Ctrl Alt K      | Toggle the touch keyboard     |
 | Ctrl Alt M      | Open context menu             |
 | Ctrl Alt U      | Open URL selector             |
 | Ctrl Alt V      | Paste clipboard               |
 |_________________|_______________________________|

Port forwarding: VM is configured to forward ports of SSH (22),
HTTP (80) and HTTPS (443) services. These guest ports are
forwarded to 16022, 16080 and 16443 respectively when possible.
On allocation failure the VM will use random port numbers as
fallback.

The forwarded services will be accessible within your LAN. Be
careful when running services with no authentication.

You can view the host ports through the context menu. They are
shown on tabs "Open SSH", "Open HTTP" and "Open HTTPS". Click
on the tab will result in attempt of launching the client for
selected service, for example ConnectBot for SSH or Chrome for
HTTP.

----------------------------------------------------------------

Shared storage volume:

  mount -t 9p host_storage /mnt

The shared storage volume is a directory shared between host
OS and VM. Use it to transfer files between vmConsole and
other applications.

You can access this directory by using any file manager that
supports Storage Access Framework. You can open a standard
file manager by pressing "Open File Manager" button in the
context menu of vmConsole. In this case the shared volume
should be shown as a tab named "vmConsole" in the drawer.

----------------------------------------------------------------

= INSTALLING SYSTEM ON DISK =

Default installation is diskless and files are stored on tmpfs.
All changes like configuration or your files are discarded once
the virtual machine was rebooted or shut down. There is a limit
on size of temporary file system, which significantly limits
the packages you can install.

Alpine Linux can be installed on persistent disk using the
utility setup-disk. An example command is shown below.

  export ROOT_SIZE=4096
  setup-disk -m sys -s 0 /dev/sda

This command installs the system on 4 GiB root parition and
disables swap. The variable ROOT_SIZE specified root partition
size in MiB. Note that size of persistent disk is 32 GiB, but
actual used size must be below available free space on host.

It is recommended that after installation you will edit the
bootloader configuration file (extlinux.conf) and add these
parameters to kernel command line:

  console=ttyS0,115200 tsc=unstable nowatchdog

Additionally you may want to remove option "quiet" to have the
boot logs shown on console.

----------------------------------------------------------------

= GETTING HELP FOR ALPINE LINUX =

Bundled offline tutorials about Bash and Linux system usage can
be found at ~/guides. They are plain-text editions of certain
books from TLDP.

Alpine Linux uses apk as package manager. Here are some most
used commands:

 - Search package:  apk search <query>
 - Install package: apk add <pkg-name>
 - Remove package:  apk del <pkg-name>
 - Upgrade system:  apk upgrade

Comprehensive tutorials specific to Alpine Linux system usage
can be found on its official Wiki.

Visit Alpine Wiki: https://wiki.alpinelinux.org/wiki/Main_Page

WARNING: vmConsole application requires proper skills of Linux
administration in order to be useful. And considering that
interface is only text-based terminal, you also need to read
the printed text carefully in order to not miss important
notice. This message is not exception. Good luck :)

----------------------------------------------------------------
