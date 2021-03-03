# Ubuntu File System Root Directory in Windows Subsystem

For Ubuntu installed from the Windows store:

Each distribution you install through the store is installed to that application's appdata directory.
For example: `C:\Users\<username>\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState`.

For WSL2 you can access to home directory from windows (Windows 10 build 18342) like this: `\\wsl$`

In earlier iterations of Windows Subsystem for Linux, the Ubuntu file system was at `%localappdata%\Lxss` (e.g., `C:\Users\Username\AppData\Local\Lxss` - replace the Username with your Username on Windows).
See [the WSL blog post on File System Support](https://blogs.msdn.microsoft.com/wsl/2016/06/15/wsl-file-system-support/):

> The primary file system used by WSL is VolFs. It is used to store the Linux system files, as well as the content of your Linux home directory. As such, VolFs supports most features the Linux VFS provides, including Linux permissions, symbolic links, FIFOs, sockets, and device files.
>
> VolFs is used to mount the VFS root directory, using `%LocalAppData%\lxss\rootfs` as the backing storage. In addition, a few additional VolFs mount points exist, most notably `/root` and `/home` which are mounted using `%LocalAppData%\lxss\root` and `%LocalAppData%\lxss\home` respectively. The reason for these separate mounts is that when you uninstall WSL, the home directories are not removed by default, so any personal files stored there will be preserved.


## Reference

- https://askubuntu.com/questions/759880/where-is-the-ubuntu-file-system-root-directory-in-windows-subsystem-for-linux-an

