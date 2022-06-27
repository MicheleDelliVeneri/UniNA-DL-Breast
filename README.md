# UniNA-DL-Breast

Repository per condividere gli scripts di pulitura dati per applicazioni di Deep Learning. 

## Obiettivo Generale
L'obiettivo di questo progetto è la creazione di una pipeline che effettui la *pulitura* di un dataset costituito da **N** coppie di cubi **(inserire formato file cubi)** contenenti rispettivamente, MRI al seno e corrispondenti segmentazioni.
Per pulitura del dataset si intende quella serie di operazioni preliminari che sono necessarie per rimuovere errori nel dataset, effettuare correzioni e prepararne l'utilizzo per future operazioni. 
In questo particolare caso, la pulitura del dataset è necessaria al fine di addestrare un'architettura di Deep Learning (DL) a segmentare in maniera automatica le MRI, o per essere più formali a risolvere il problema di imaging:
$$ y = Ax + n $$
dove *y* è il cubo MRI, *x* è il cubo di segmentazione, *A* è un operatore lineare ed n sono tutte le fonti di rumore presenti nei dati (dai rumori di carattere statistico, ad artefatti presenti nei dati).Per segmentazione si intende che ogni pixel del cubo è caratterizzato con un valore intero incrementale che ne definisce esplicitamente l'appartenenza ad una classe (es. tessuto adiposo, ghiandola, tumore, etc..).
Un cubo è una serie di immagini prese a diverse profondità all'interno del seno della paziente, che quindi sono altamente correlate tra di loro a causa della natura tridimensionale delle strutture che compongono il seno. Le dimensioni del cubo sono [n_f, n_w, n_h] dove *n_f* è il numero di immagini (o slices) in frequenza (la penetrazione è legata ala frequenza di emissione delle onde radio) e *n_w* ed *n_h* sono il numero di pixels che compongono l'immagine in larghezza ed altezza. L'unica differenza che dovrebbe sussistere tra i due cubi è il formato con cui sono salvati i valori al loro interno. Per il cubo MRI (o input_cube) questi sono float 32, mentre per il cubo di segmentazione (target_cube) sono interi. 
Il dataset presenta alcuni problemi evidenti: 
1. il numero di slices *n_f* tra alcune coppie di (input_cube, target_cube) non 
