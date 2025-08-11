---
title: Automazione Laboratori EMC
summary: Automazione di alcuni processi, come la creazione di report, grazie all'uso di macro Word in VBA

authors:
- admin

tags:
- Automazione

date: 2020-03-28T01:05:49+02:00

# Optional external URL for project (replaces project detail page).
# external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: Smart


# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
draft: false
share: false
---

L'attività giornaliera di un laboratorio di compatibilità elettromagnetica è composta da svariate azioni, la principale è ovviamente l'esecuzione delle misure EMC.

A conclusione della campagna di misure, arriva la parte forse più tediosa di tutte: raccolta dati e stesura del report di misura. Tale attività può essere noiosa, ma è molto, molto importante per diverse ragioni:
- è il completamento di tutto il progetto di misura, e quindi apre le porte della fatturazione, cioè la possibilità di richiedere il pagamento della prestazione;
- il risultato dell'operazione di repostistica è un documento fornito al cliente, che non aspetta altro per poter commercializzare il suo prodotto, in quanto il report EMC, unito ad altri, fornisce la documentazione che "sta dietro" alla Dichiarazione di Conformità.

Fin dai primi giorni di quel lontano Marzo 2008, mi resi conto che la creazione di un report EMC, era per la maggior parte una sequenza di operazioni meccaniche puramente informatiche...
copia un'immagine, ridimensionala, copia la tabella, incollala... erano tutte operazioni che venivano eseguite a mano e che non richiedevano alcuna elaborazione concettuale.
Inoltre, cosa che attualmente non è più applicabile, il template del report utilizzato era strutturato con un corpo principale e svariati allegati (uno per ogni prova).

In un laboratorio di Compatibilità Elettromagnetica che esegue prove su un ampio spettro di tipologie di prodotti,
l'attività di reportistica è il collo di bottiglia della campagna prove. Questo dipende dal fatto che se si lavorasse con dei Template pre-costruiti, si avrebbe bisogno di una decina di documenti modello. Inoltre, per le campagne più complesse in cui è necessaria una "gap analysis", il report viene customizzato per-attività, rendendo di fatto inutile il suo utilizzo.

Non mi ci volle molto per capire che con una macro Microsoft Word&copy; si poteva automatizzare la gran parte del lavoro. Mi misi subito all'opera, e fornisco qui sotto alcune schermate del progetto che svolsi.

{{< figure src="inizioanonym.jpg" caption="Lo splash screen della macro" numbered="true" >}}

Decisi di strutturare la macro in modo che fosse di facile utilizzo per i miei colleghi, fornendola quindi di una interfaccia utente (GUI): Microsoft Word&copy; consente di crearne una in modo molto semplice, trascinando sullo spazio di lavoro oggetti grafici come caselle d testo, menù drop-down, e altri elementi.

Divisi poi in diverse TAB le varie operazioni che la macro poteva svolgere: il primo tab raffigurato qui sotto consentiva di scrivere le intestazioni del documento: come ad esempio il numero del progetto, il nome del campione sotto test, la data di invio, la revisione del documento.

{{< figure src="intestazioni.jpg" caption="La configurazione delle intestazioni del documento" numbered="true" >}}

{{< figure src="draft.jpg" caption="Creazione dei documenti Draft e Definitivo" numbered="true" >}}

{{< figure src="ETC.jpg" caption="Configurazione dell'allegato per la prova di Emissioni del Transitorio Condotto (Automotive)" numbered="true" >}}

Il linguaggio di programmazione utilizzato per le macro in Microsoft Word&copy; e Microsoft Excel&copy; è il Visual Basic fornito all'interno della suite Microsoft Office, entro la quale sono già contenuti svariati comandi per l'integrazione con l'intera suite.

{{< figure src="armfli.jpg" caption="Configurazione dell'allegato di Armoniche e Flicker" numbered="true" >}}

{{< figure src="ridimensionamento.jpg" caption="Integrazione software per il ridimensionamento delle immagini" numbered="true" >}}

{{< figure src="sequenze.jpg" caption="Creazione di sequenze di operazioni" numbered="true" >}}
