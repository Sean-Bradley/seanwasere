# Mount NTFS USB Portable Drive in Linux Ubuntu

Log onto console as root and install ntfs-3g so that you can read and write to ntfs using ubuntu without much hassle.

`apt-get install ntfs-3g`

list drives 1st with your new USB portable drive disconnected,

`ls /dev/sd*`

list again, with your new USB portable drive connected, and note the new drive entry.

`ls /dev/sd*`

Whenever I did this in the past, my USB drive always showed as /dev/sda1, but for you it may be different.

Open WinSCP as root in windows and navigate to /etc/ and open fstab.
add this line to the end of the file

`/dev/sda1  /mnt  ntfs-3g  users,defaults  0  0`

Save it and reboot.

Your USB drive is now visible and usable under the /mnt/ folder.

It also auto mounts upon reboot, and allows read/write access for all users.

