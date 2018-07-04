# Resize ODROID Root Partition

After creating your img of Ubuntu for your Odroid (XU3 in my case) and starting it up for the first time, you will need to resize the root partition in order to utilise the full size of your eMMC or SDCard, otherwise you will experience disk full errors much sooner than you expected.

## Video Tutorial
[![Resize ODROID Root Partition](https://img.youtube.com/vi/syqErhQnFDg/0.jpg)](https://www.youtube.com/watch?v=syqErhQnFDg)

[Resize ODROID Root Partition](https://www.youtube.com/watch?v=syqErhQnFDg)

To do this, Odroid supply a quick and easy tool that does many useful things that is called odroid-utility.sh.
Get it by logging onto the console as root, and entering the commands below.

```
sudo -s

apt-get update

wget -O /usr/local/bin/odroid-utility.sh https://raw.githubusercontent.com/mdrjr/odroid-utility/master/odroid-utility.sh

chmod +x /usr/local/bin/odroid-utility.sh

odroid-utility.sh
```

Once the utility starts, select ‘Resize your root partition’,
When finished reboot,
This fixed many of my issues,
Good luck with your new mini super computer.