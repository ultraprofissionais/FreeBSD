FREEBSD Netflow

This script was built to meet the demand for netflow export to FreeBSD based on interfaces, to send data to an Andrisoft Wanguard server to aid in DDOS analysis and detection.

After several tutorials and readings based on the FreeBSD manual and the article by C6H12O6 on https://blog.c6h12o6.org/post/freebsd-netflow-exporter/#%E8%87%AA%E5%8B%95%E8%B5%B7%E5%8B%95%E3%81%AE%E8%A8%AD%E5%AE%9A, I was able to implement netflow on FreeBSD and from that I built this netflow management script which consists of:
- /etc/netflow.conf configuration file that will indicate the server and interfaces to have netflow exported
- /usr/local/sbin/netflow management script to start or stop the FreeBSD service
- /usr/local/etc/rc.d FreeBSD startup script

To use these files, just place them in their respective locations and give execution permission.

First, we need to load some kernel modules at boot time – to do this we need to add the following lines to your /boot/loader.conf file:
```
netgraph_load="YES"  
ng_ether_load="YES"  
ng_socket_load="YES"  
ng_ksocket_load="YES"  
ng_tee_load="YES"  
ng_netflow_load="YES"  
```

You can load these now without having to reboot by typing:  

kldload netgraph ng_ether ng_socket ng_ksocket ng_tee ng_netflow  

Step-by-step:  
1) Download the files  

2) Move etc/netflow.conf to /etc/netflow  
```
mv etc/netflow.conf /etc/netflow  
```
   
3) Move sbin/netflow to /usr/local/sbin/netflow   
```
mv sbin/netflow /usr/local/sbin/netflow   
```
   
4) Move rc.d/netflow to /usr/local/etc/rc.d   
```
mv rc.d/netflow /usr/local/etc/rc.d/netflow   
```
   
5) Give execution permission   
```
chmod +x /usr/local/sbin/netflow    
chmod +x /usr/local/etc/rc.d/netflow    
```
   
6) Include netflow_enable="YES" in rc.conf   
    
7) Edit /etc/netflow.conf with the desired configurations   
   
8) To execute, use    
```
netflow help   
service netflow start | stop   
```
   
Any questions, please contact atendimento@ultra.pro.br.   
   
