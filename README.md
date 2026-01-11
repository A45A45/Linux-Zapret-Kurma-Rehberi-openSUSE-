# Linux Zapret Kurma Rehberi (openSUSE)
Ben openSUSE kullanıyorum farklı bir distro kullanıyorsanız benim komutların denklerini kullanarak takip edebilirisiniz (msl. zypper = apt)

##Prereq indir
`sudo zypper -n install curl bind-utils unzip nftables`
##DNS Kurallarını Değiştir
`sudo systemctl enable systemd-resolved`
`sudo systemctl start systemd-resolved`

nano /etc/systemd/resolved.conf

