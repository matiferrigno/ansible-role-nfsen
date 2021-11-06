net.netflow.promisc=1
net.netflow.protocol=9
net.netflow.hashsize=32768
net.netflow.natevents=1


[Unit]
Description=Bring up an interface in promiscuous mode during boot
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/sbin/ip link set dev ens224 promisc on up
TimeoutStartSec=0
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target


nfexpire
