# Linux Zapret Kurma Rehberi (openSUSE)
Ben openSUSE kullanıyorum farklı bir distro kullanıyorsanız benim komutların denklerini kullanarak takip edebilirsiniz (msl. zypper = apt)

## Prereq indir

`sudo zypper -n install curl bind-utils unzip nftables`

## DNS Kurallarını Değiştir

`sudo systemctl enable systemd-resolved`

`sudo systemctl start systemd-resolved`


`nano /etc/systemd/resolved.conf`
### Aşağıdaki komutları dosyaya yapıştırın
`[Resolve]`

`DNS=77.88.8.8 77.88.8.1 2a02:6b8::feed:0ff 2a02:6b8:0:1::feed:0ff`

`DNSOverTLS=yes`

CTRL + S, CTRL + X ile kayıt edip çıkın

`sudo ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf`

`sudo systemctl restart systemd-resolved`

## Zapret indirme öncesi

`git clone https://github.com/bol-van/zapret.git`

`~/zapret/install_prereq.sh`

Firewall type: nftables

`~/zapret/install_bin.sh`

## Blockcheck

`~/zapret/blockcheck.sh`

>specify domain(s) to test. multiple domains are space separated.
domain(s) (default: rutracker.org)

Herhangi bir engellenmiş website girin (örnek: discord.com). Geri kalan soruları boş bırakın. Test birkaç dakika sürebilir, test bittikten sonra en sonda;

`ipv4 discord.com curl_test_https_tls12 : nfqws --dpi-desync=fakeddisorder --dpi-desync-ttl=1 --dpi-desync-autottl=-5 --dpi-desync-split-pos=1`

gibi bir sonuç çıkacak, sizdeki farklı olabilir, nfqws yazısı sonrasını kaydedin. 

## Zapret indir

`~/zapret/install_easy.sh`

>do you want the installer to copy it for you (default : N) (Y/N) ?

Y 

>select firewall type :
1 : iptables
2 : nftables
your choice (default : nftables) :

nftables

>enable ipv6 support (default : N) (Y/N) ?

N

>select flow offloading :
1 : none
2 : software
3 : hardware
your choice (default : none) :

none

>select filtering :
1 : none
2 : ipset
3 : hostlist
4 : autohostlist
your choice (default : none) :

none

>enable tpws socks mode on port 987 ? (default : N) (Y/N) ?

N

>enable tpws transparent mode ? (default : N) (Y/N) ?

N

>enable nfqws ? (default : N) (Y/N) ?

Y

>do you want to edit the options (default : N) (Y/N) ?

Y

Bundan sonra, önceden kayıt ettiğiniz ayarı NFQWS_OPT ta bulunan yazıyı silip yapıştırın ve CTRL + S, CTRL + X ile çıkın 

>do you want to edit the options (default : N) (Y/N) ?

N

>LAN interface :
1 : NONE
2 : lo
3 : wlp0s20f3
your choice (default : NONE) :

NONE

>WAN interface :
1 : ANY
2 : lo
3 : wlp0s20f3
your choice (default : ANY) :

ANY

Kurma tamamlanmıştır. Özgürlüğünüzü geri kazandığınızda uninstall_easy.sh dosyası ile kaldırabilirsiniz.



