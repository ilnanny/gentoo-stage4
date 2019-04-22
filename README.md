# gentoo-stage4

## Sommario
- [Idea] (# Idea)
- [Stage4 TYPES] (# Stage4-types)
- [Script] (# script)
- [Supporto per altri Cloud Provider] (# Support-for-others-Cloud-Provider)
- [Pacchetti] (# pacchetti)
- [Servizi] (# Servizi)
- [Kernels] (# Kernels)
- [Accesso SSH] (# Accesso SSH)
- [Future changes and releases] (# Future-changes-and-releases)
- [Changelog] (# Changelog)
- [Cosa devi fare ...] (# What-you-need-to-do ...)

## Idea
Tutti noi sappiamo che un'installazione di Gentoo richiede del tempo rispetto a qualsiasi altra distribuzione. Negli ultimi anni, ho eseguito l'installazione tramite uno script di installazione automatica che richiede alcuni minuti, ma su ciascuna installazione vengono eseguite operazioni ripetitive, quindi perché non disporre di un archivio contenente le informazioni di base che è necessario aggiungere ad ogni installazione?

L'idea deriva dal fatto che alcuni provider di hosting (come Hetzner) non forniscono un'immagine Gentoo sui loro server cloud virtuali, quindi questo è un modo FACILE e VELOCE di avere Gentoo installato ovunque.

## TIPI Stage4
Sto fornendo due tipi di stage4:
- ***Standard***
 Usa il profilo standard (default / linux / amd64 / 17.0). Poiché al giorno d'oggi il compilatore impone pie e ssp, questo stage4 mira a evitare la compilazione con ssp / pie / relro e altre protezioni, ** per accelerare il più possibile ** dove i flag di protezione non sono necessari, altrimenti sembrerebbe molto simile allo stage hard4.
 Se stai cercando qualcosa compilato con protezioni indurite, guarda la fase Indurita.
- ***Indurito***
 Usa il profilo hardened (default / linux / amd64 / 17.0 / hardened) senza modifiche, quindi tutte le protezioni sono abilitate.

Il pacchetto `app-admin / checksec` fornisce uno script che può aiutarti a capire lo stato dei binari compilati:
~~~~
~ $ checksec --proc-all
~~~~

## Scripts
I'm providing two scripts:
- ***stage4*** ( For general usage )
- ***stage4-hetzner-cloud*** ( For Hetzner Cloud )

Perché più script invece di uno?
L'obiettivo ** è quello di mantenere lo script il più semplice possibile senza dozzine di if/for, così le persone saranno in grado di capire rapidamente cosa fa.

** Se il tuo provider cloud offre un sistema di salvataggio, probabilmente sarai in grado di installare lo stage4 generale. **

## Supporto per altri fornitori di servizi cloud
Vuoi avere il tuo fornitore cloud preferito completamente supportato qui? Basta aprire un ticket e farò del mio meglio per aggiungere il supporto.

## Pacchetti
Pacchetti inclusi nello stage4:

~~~~
app-admin/checksec
app-admin/logrotate
app-admin/spectre-meltdown-checker
app-admin/syslog-ng
app-misc/delay
app-misc/tmux
app-portage/eix
app-portage/gentoolkit
net-misc/ntpsec
sys-boot/grub
sys-kernel/linux-firmware
sys-power/acpid
sys-process/cronie
sys-process/htop
~~~~

## Servizi
Servizi aggiunti al runlevel predefinito:
~~~~
syslog-ng
acpid
cronie
net.eth0 (only for stage4-hetzner-cloud)
ntp
sshd
~~~~

## Kernels
Per lo script * stage4-hetzner-cloud * viene fornito un kernel monolitico personalizzato. Si basa sull'hardware Hetzner Cloud. Se è necessario includere altri moduli, viene fornita la relativa configurazione del kernel, quindi è possibile iniziare da lì.
Per lo script * stage4 *, viene fornito un kernel basato su genkernel.

## Accesso SSH
Se c'è un file chiamato id_rsa.pub nello stesso percorso in cui stai eseguendo lo script stage4, questo file verrà copiato come`/root/.ssh/authorized_keys`

## Modifiche e rilasci futuri
I cambiamenti futuri nello stage 4 possono essere rilevanti per:
- kernel
- aggiornamento dei pacchetti
- qualsiasi altra modifica nella configurazione

I rilasci non saranno frequenti.
Ciò non significa che il progetto non venga mantenuto, ma semplicemente non è necessario avere un rilascio ogni settimana.
Di solito una versione verrà pubblicata dopo le principali modifiche ** stabili ** (gcc, glibc) e per ogni aggiornamento di toolchain, verrà eseguito un completo `emerge -e world` prima di pubblicare una nuova versione.

In ogni caso è possibile installare stage4 ** in qualsiasi momento ** e aggiornare agli ultimi pacchetti stable disponibili tramite emerge con:

` ~ $ emerge -DuNav world`

## Novità
Per evitare la navigazione e la ricerca nella cronologia git, viene fornito un Changelog in chiaro, che riepiloga e tiene traccia delle modifiche tra le versioni.

## Cosa devi fare...
Se stai usando qualcosa da questo repository, apprezzo se "Star" il repository. Questo mi darà un'idea di quante persone stanno usando questa roba e, di conseguenza, quanti sforzi ho bisogno di mettere per mantenere il progetto in buono stato.

---

\# Gentoo hetzner cloud  
\# Gentoo stage4  
\# Gentoo cloud  
