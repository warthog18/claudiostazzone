---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Compilazione e Installazione di ElmerFEM su Manjaro Linux 22"
subtitle: "Compilazione da sorgenti di ElmerFEM"
summary: "Procedura per compilare e installare il software di simulazione ad elementi finiti ElmerFEM sulla distribuzione Manjaro Linux (basata su Arch Linux)"
authors: [admin]
tags: [EM_Simulation, ElmerFEM, Elementi_Finiti]
categories: [Simulazione]
date: 2023-09-02T23:29:18+02:00
lastmod: 2023-09-02T23:29:18+02:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
commentable: true
---

## Cosa è ElmerFEM
ElmerFEM è un software Open Source che risolve equazioni differenziali parziali, usando il metodo degli elementi finiti. Nasce in Finlandia nel 1995 ed è in costante sviluppo dal 2005, quando viene rilasciato sotto la licenza GNU General Public License (GPL). E' un software definito "multisym" che riesce cioè a simulare diversi fenomeni fisici, come il trasferimento di calore, comportamento dei fluidi (come aria, acqua), comportamenti elastici, trasferimento di onde sonore (acustica), microfluidi, meccanica quantistica, fenomeni elettromagnetici (molto interessanti per chi scrive, senza nulla togliere agli altri, ovviamente).

## Il significato della compilazione
Ma perché scervellarsi a compilare il codice sorgente quando si può utilizzare un pacchetto pre-compilato? Perché compilando il software sul proprio PC, si possono ottenere prestazioni notevolmente più performanti, in quanto la compilazione viene fatta su un hardware specifico: i pacchetti precompilati invece sono stati compilati su un hardware generico, che noi non conosciamo, e quindi potrebbero non essere ottimizzati per il PC sul quale il software dovrà girare (il nostro).

## Per chi non vuole "smanettare" con librerie e pacchetti da installare
Volete la strada più semplice? Va bene, seguite le istruzioni qui sotto per far fare il lavoro a YAY, scaricamento e compilazione inclusi.

Installazione del software YAY, per scaricare pacchetti dai repository AUR
```
sudo pacman -S yay
```

Installazione di ElmerFEM tramite YAY
```
yay -S elmerfem
```

E aspettiamo una decina di minuti (sul mio laptop DELL XPS13).
**Piccolo problema**: ad un certo punto la compilazione si è fermata con un errore relativo alla libreria libmmgtypesf.h (in realtà un header file della libreria MMG). E' bastato un minuto di ricerca su internet per trovare che il file in questione è stato spostato dalla cartella /usr/include/mmg/mmg3d alla cartella /usr/include/mmg/common. Ho quindi provveduto a fare un link al file residente in common, per farlo trovare al compilatore... ok, funziona!
In dieci minuti circa avete ElmerFEM funzionante.

Volete avere l'ultimissima versione di ElmerFEM, con tutti i cambiamenti e migliorie apportati dagli sviluppatori e contributori del progetto? Andate avanti a leggere...

Il processo di compilazione non è semplice per definizione, e generalmente riservato ai cosiddetti "nerd". Condivido queste informazioni proprio per semplificare il processo e con l'obiettivo di dare la possibilità a tutti di eseguire i passi che porteranno ad avere ElmerFEM compilato sul proprio sistema.

Le istruzioni per la compilazione visibili dal sito di ElmerFEM non sono esplicative per chi usa Manjaro Linux, o in generale una distribuzione Linux basata su Arch Linux, che potrebbe chiamare in modo leggermente differente le librerie e i vari pacchetti che devono essere installati prima di ElmerFEM. Ecco il secondo motivo per cui scrivo queste istruzioni.


## Preparazione del sistema

Installare il pacchetto base-devel per la compilazione

```
sudo pacman -S base-devel
```

Scaricare i sorgenti di ElmerFEM dal repository GitHub cliccando [qui](https://github.com/ElmerCSC/elmerfem.git), clonando il repository con il comando:
```
git clone https://github.com/ElmerCSC/elmerfem.git
```

Se non sapete cosa è GIT, non vi preoccupate. Basta visitare il link qui sopra, cliccare sul bottone verde "<> Code", e cliccare su "Download ZIP".


## Programmi e librerie necessari per una compilazione senza errori

La prima fase della compilazione consiste nella creazione di un file che contiene tutte le informazioni necessarie: le librerie da utilizzare, i percorsi dove creare i vari file risultato della compilazione, e altre cose.

Con libreria MUMPS (attualmente non funziona in Manjaro)
Libreria MUMPs

yay -S mumps
yay -S parmetis (restituisce errore gklib...)

```
cmake -DWITH_QT5=TRUE -DWITH_ELMERGUI:BOOL=TRUE -DWITH_MPI:BOOL=TRUE -DWITH_Mumps:BOOL=TRUE -DWITH_LUA:BOOL=TRUE -DCMAKE_INSTALL_PREFIX=../install ../../elmerfem
```

Senza libreria MUMPS
```
cmake -DWITH_QT5=TRUE -DWITH_ELMERGUI:BOOL=TRUE -DWITH_MPI:BOOL=TRUE -DWITH_LUA:BOOL=TRUE -DCMAKE_INSTALL_PREFIX=../install ../../elmerfem
```

Il comando per eseguire la compilazione vera e propria è semplicemente **make**
