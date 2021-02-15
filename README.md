# project_mvn

### Cosa e' Maven
Maven è un software usato principalmente per la gestione di progetti Java e build automation.

### File system e repository locale di un progetto Maven 
Dopo aver creato un progetto maven, all'interno della root, si creerano una cartella `src`,che è la definizione di una struttura standard per un progetto Java, al cui interno ci saranno una cartella `main`, codice sorgente del progetto, e una cartella `test`, codice sorgente dei test d’unità; poi verra' creato anche un file `pom.xml`, che è il cuore del progetto, dove vengono poste tutte le nostre configurazioni.
Una volta installato Maven si crea una repository locale nel percorso `Users\nome_utente\.m2\repository`. Ogni volta che lanciamo la compilazione di un progetto, Maven legge dal `pom.xml` le `dependencies` dichiarate e cerca di recuperarle prima di tutto dal repository locale. Se i `jar` richiesti non sono presenti localmente, Maven si collega al repository centrale sul web, e scarica i pacchetti nel repository locale. 
Gli elementi fondamentali del file pom sono i seguenti:
- `<groupId></groupId>`, rappresenta il nome del gruppo del progetto o di diversi progetti in comune fra di loro. 
- `<artifactId></artifactId>`, rappresenta il nome del progetto
- `<version></version>`, rappresenta la versione del progetto
- `<packaging></packaging>`, rappresenta il tipo di pacchetto che si vuole avere (war, jar etc.). 

### Cosa sono i goals 
Maven non e' altro che un esecutore di plug-in, alcuni presenti di default e altri che si possono aggiungere all'occorrenza. Il `goal` non e' altro che lo specifico compito eseguito da quel plug-in. Tra i vari `goals` quelli piu' importanti sono:
- `validate`: valida il progetto.
- `compile`: compila i sorgenti del progetto.
- `test`: esegue i file test compilati usando uno specificabile framework per i test. Non necessita che venga effettuato il package o il deploy.
- `package`: prende i file compilati ed esegue il package in un file JAR (o war,..ecc).
- `verify`: esegue ogni controllo per verificare se il package è valido.
- `install`: installare il package nel repository locale, da utilizzare come dipendenza in altri progetti in locale.
- `deploy`: copia il pacchetto finale nel repository remoto per condividerlo con altri sviluppatori e progetti. 
- `clean`: ripulisce gli artifact creati nelle precedenti esecuzioni.
- `site`: genera un sito di documentazione per il progetto.
Se invoco un goal qualsiasi, vengono eseguiti tutti i goals precedenti fino a quello invocato.


### See
* [Cosa e' Maven](https://stackoverflow.com/questions/13335351/what-does-maven-do-in-theory-and-in-practice-when-is-it-worth-to-use-it) - Descrizione di Maven in teoria e in pratica
* [Installazione e primo progetto](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) - Come si installa Maven e come potrebbe essere un primo progetto 
* [Concetto di goals](https://www.baeldung.com/maven-goals-phases) - Descrizione dei goals di default di Maven