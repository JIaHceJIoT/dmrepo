---
order: 1
title: DM repo
---

4 коммутация

tcpdump -i eth0 -e vlan -c 4

<table header="row">
<tr>
<td align="left">

**Префикс**

</td>
<td align="left">

**Маска подсети**

</td>
<td align="left">

**Количество хостов**

</td>
</tr>
<tr>
<td align="left">

/24

</td>
<td align="left">

255\.255.255.0

</td>
<td align="left">

256

</td>
</tr>
<tr>
<td align="left">

/25

</td>
<td align="left">

255\.255.255.128

</td>
<td align="left">

128

</td>
</tr>
<tr>
<td align="left">

/26

</td>
<td align="left">

255\.255.255.192

</td>
<td align="left">

64

</td>
</tr>
<tr>
<td align="left">

/27

</td>
<td align="left">

255\.255.255.224

</td>
<td align="left">

32

</td>
</tr>
<tr>
<td align="left">

/28

</td>
<td align="left">

255\.255.255.240

</td>
<td align="left">

16

</td>
</tr>
<tr>
<td align="left">

/29

</td>
<td align="left">

255\.255.255.248

</td>
<td align="left">

8

</td>
</tr>
<tr>
<td align="left">

/30

</td>
<td align="left">

255\.255.255.252

</td>
<td align="left">

4

</td>
</tr>
<tr>
<td align="left">

/31

</td>
<td align="left">

255\.255.255.254

</td>
<td align="left">

2

</td>
</tr>
<tr>
<td align="left">

/32

</td>
<td align="left">

255\.255.255.255

</td>
<td align="left">

1

</td>
</tr>
</table>

**Топология:**

```
                  [ Internet ]                                    
                       |
                       |
       172.16.10.1  [ ISP ]   172.16.20.1
               |                |
               |                |
               |                |
               |                |
         [ HQ-RTR ]         [ BR-RTR ]
         172.16.10.2        172.16.20.2
         10.10.0.1          10.10.0.2 (GRE-туннель)
              |             192.168.0.1
              |                 |
     +--------+--------+        |
     |  192.168.111.1  |        |
     |  192.168.211.1  |    [ BR-SRV ]
     |  192.168.81.1   |    192.168.0.2
     |                 |
 [ HQ-SRV ]        [ HQ-CLI ]
192.168.111.2        (DHCP)
```