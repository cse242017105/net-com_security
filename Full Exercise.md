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
