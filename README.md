# ssacli-exporter For HP RAID Controllers
This exporter for the Prometheus monitoring system calls into the ssacli utility to provide metrics for errors reported by HP RAID hardware. Under the hood, it invokes the following command when being scraped:

```
ssacli ctrl slot=0 physicaldrive all show detail
```

# Try it

```
ssacli_exporter -Port 9060 (default port 9109 - /metrics )
```
# Grafana Dashboard 

![plot](./Dashboard.png)



Example metrics output:

```
# HELP disk_current_temperature Disk Current Temperature
# TYPE disk_current_temperature gauge
disk_current_temperature{physicaldrive="box 3 bay 1 type SAS"} 46
disk_current_temperature{physicaldrive="box 3 bay 2 type SAS"} 51
disk_current_temperature{physicaldrive="box 3 bay 3 type SAS"} 48
disk_current_temperature{physicaldrive="box 3 bay 4 type SAS"} 44
# HELP disk_maximum_temperature Disk Maximum Temperature
# TYPE disk_maximum_temperature gauge
disk_maximum_temperature{physicaldrive="box 3 bay 1 type SAS"} 50
disk_maximum_temperature{physicaldrive="box 3 bay 2 type SAS"} 58
disk_maximum_temperature{physicaldrive="box 3 bay 3 type SAS"} 58
disk_maximum_temperature{physicaldrive="box 3 bay 4 type SAS"} 55
# HELP disk_status Disk Status (OK = 1)
# TYPE disk_status gauge
disk_status{physicaldrive="box 3 bay 1 type none"} 1
disk_status{physicaldrive="box 3 bay 2 type SAS"} 1
disk_status{physicaldrive="box 3 bay 3 type SAS"} 1
disk_status{physicaldrive="box 3 bay 4 type SAS"} 1
```
# Install ssacli_exporter
```
cp ssacli_exporter /usr/local/bin/
cp ssacli_exporter.service /etc/systemd/system/
systemctl daemon-reload
systemctl enable ssacli_exporter.service
systemctl start ssacli_exporter.service
```
# Install HP Raid HPSA ssacli on Ubuntu

```
wget https://downloads.linux.hpe.com/SDR/repo/mcp/ubuntu/pool/non-free/ssacli-6.45-8.0_amd64.deb (probably check for updates) 
apt install ./ssacli-6.45-8.0_amd64.deb
```

More Info 

https://downloads.linux.hpe.com/SDR/project/mcp/

https://downloads.linux.hpe.com/SDR/keys.html

https://support.hpe.com/hpsc/swd/public/detail?swItemId=MTX-f8f30da26d6749499adec36f8b#tab3
