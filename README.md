# Seedbox Installation Script
### !!! These scripts are only intended to run on freshly installed Debian 10
This script does not guarantee performance increase and might cause some serious bugs to your machine. The idiot that write this script literally has zero coding knowledge and probably fuck up somewhere. Please use with cautions

The Optimized BBR would increase packet retransmission rate and waste your bandwidth. On 10Gbps network, the waste is around 30% of your acutal upload ammount and around 10% on a 1Gbps. Please use with caution if you are on a metered network. (Or even on a unmetered network, since this is boarderline DDoS already)

I am not actively managing this script, please debug it yourself
## Usage
### Install.sh
`wget https://raw.githubusercontent.com/jerry048/Dedicated-Seedbox/main/Install.sh && chmod +x Install.sh`

`bash Install.sh <username> <password> <Cache Size(unit:GiB)>`

##### Run BBR Script after Reboot

`bash BBR.sh`

### Tuning.sh if you have already installed clients (Likely to break something, becareful)

`wget https://raw.githubusercontent.com/jerry048/Dedicated-Seedbox/main/Tune.sh && chmod +x Tune.sh`

`bash Tune.sh`
## Functions
### Install.sh
###### 1. Install Seedbox Environment
	BitTorrent Client
		1.qBittorrent with tune
	Autoremove-torrents
###### 2. Tweaking
	CPU Optimization
		1.Tuned
	Network Optimization
		1.NIC Config
		2.ifconfig
		3.ip route
	Kenel Values
		1./proc/sys/kernel/
		2./proc/sys/fs/
		3./proc/sys/vm
		4./proc/sys/net/core
		5./proc/sys/net/ipv4/
	Drive Optimization
		1.I/O Scheduler
		2.File Open Limit
	Optimizied BBR
### Tuning.sh
###### Tuning Options:
	1. Deluge Libtorrent tweaking (Only work on Libtorrent 1.1.14 with ltconfig plugins installed)
	2. System Tuning
		CPU Optimization
		Network Optimization
		sysctl values
		Drive Optimization
	3. Optimizied BBR Install
	4. Configuring Boot Script for certain tunings
### Fine Tunning Note
- The Cache size should be set to around 1/4 of the machine total available ram. In case you opt for qBittorrent 4.3.x, you need to take account into memory leakage and set it to 1/8. 

- aio_threads default setting is 4 and should be good for HDD. For SSD or even NVMe server, you might consider increase it to 8 or even 16. 
	- For qBittorrent 4.3.x you can change it in the advance setting tab. 
	- For qBittorrent 4.1.x, you can set it in /home/$username/.config/qBittorrent/qBittorrent.conf by adding Session\AsyncIOThreadsCount=8 under [BitTorrent] section

- TCP buffer size in /etc/sysctl.conf could be a little bit too high if you machine is low on ram. Please change it accordingly.
	- A little bit more fine tunning notes can also be found in /etc/sysctl.conf

- For file system, I highly recommend using XFS 
### Credit
qBittorrent Install - https://github.com/userdocs/qbittorrent-nox-static

qBittorrent Password Set - https://github.com/KozakaiAya/libqbpasswd & https://amefs.net/archives/2027.html

autoremove-torrents - https://github.com/jerrymakesjelly/autoremove-torrents

BBR Install - https://github.com/KozakaiAya/TCP_BBR
