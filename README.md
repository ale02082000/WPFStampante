# WPFStampante
***
- Utilizzare gli enum di C# per la gestione dei colori
- rendere persistente lo stato del programma
  -- alla riapertura le % dei colori della stampante sono invariati
  -- alla riapertura il numero di foglii nella stampante è invariato
***


<img src="https://github.com/ale02082000/WPFStampante/assets/127590077/63d26051-a51a-4c79-9f8c-04620188189b">





``` c#

public bool Stampa(Pagina p)
        {
           
            if (Fogli > 0 &&
                C >= p.C &&
                M >= p.M &&
                Y >= p.Y &&
                B >= p.B)
            {
                
                C -= p.C;
                M -= p.M;
                Y -= p.Y;
                B -= p.B;
                Fogli--;

                return true; 
            }

            return false;
        }

        public void SostituisciColore(Colore c)
        {
            
            switch (c)
            {
                case Colore.C:
                    C = 100;
                    break;
                case Colore.M:
                    M = 100;
                    break;
                case Colore.Y:
                    Y = 100;
                    break;
                case Colore.B:
                    B = 100;
                    break;
            }
        }

        public void AggiungiCarta(int qta)
        {
           
            if (qta > 0)
            {
                
                if (Fogli + qta <= 200)
                {
                    Fogli += qta;
                }
                else
                {
                    Fogli = 200;
                }
            }
        }
```

***
Il metodo Stampa gestisce il processo di stampa di una pagina, assicurandosi che ci siano fogli sufficienti e quantità adeguate di consumabili come inchiostri di colore C, M, Y e B. Se è tutto corretto, riduce le quantità disponibili di consumabili e fogli, indicando che la stampa è avvenuta con successo. In caso contrario, segnala che la stampa non è possibile.

Il metodo SostituisciColore si occupa di rinnovare la quantità di inchiostro per un colore specifico, portandola a un valore massimo di 100.

Il metodo AggiungiCarta incrementa il numero di fogli disponibili, ma garantisce che il totale non superi mai 200 fogli. In questo modo, gestisce l'aggiunta di carta in modo limitato rispetto alla capienza massima della stampante.

***









``` c#

public MainWindow()
        {
            InitializeComponent();

            
            stampante = new Stampante();

            
            try
            {
                StreamReader rd = new StreamReader("C:\\Users\\studente.ITTSBELLUZZIDAV\\Desktop\\WPFStampante-main\\bartolucci.alessandro.4i.Stampante\\bartolucci.alessandro.4i.Stampante\\Models\\persistente.csv");
                string r = rd.ReadLine();

                
                if (r != null && r.Split(';').Length >= 5)
                {
                    int.TryParse(r.Split(';')[0], out int ciano);
                    int.TryParse(r.Split(';')[1], out int magenta);
                    int.TryParse(r.Split(';')[2], out int giallo);
                    int.TryParse(r.Split(';')[3], out int nero);
                    int.TryParse(r.Split(';')[4], out int fogli);

                   
                    stampante.C = ciano <= 0 ? 100 : ciano;
                    stampante.M = magenta;
                    stampante.Y = giallo;
                    stampante.B = nero;
                    stampante.Fogli = fogli;

                   
                    AggiornaUI();
                }
            }
            catch (Exception ex)
            {
                MessageBox.Show("Errore durante la lettura del file: " + ex.Message);
            } 

```

***
Il codice inizializza la UI della finestra principale, crea un'istanza di una classe Stampante, e cerca di leggere un file CSV per impostare lo stato iniziale della stampante. Se la lettura del file avviene con successo e contiene almeno cinque elementi, vengono interpretati come valori per i consumabili (ciano, magenta, giallo, nero) e il numero di fogli nella stampante. Questi valori vengono quindi utilizzati per aggiornare lo stato della stampante. In caso di errori durante la lettura del file, viene visualizzato un messaggio di errore tramite una finestra di avviso.
***





