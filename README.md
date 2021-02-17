# project_mvn

### Cosa e' Maven
In sintesi Maven e' un strumento che permette la *gestione delle dipendenze* e il *build automation* per i progetti Java.
Maven e' anche un insieme di standard applicate e una struttura di repository che serve per lo sviluppo. 
In altre parole Maven e':

- Gestione delle dipendenze
- Repository 
- Build automation
- Progetto strutturato secondo uno standard


### Struttura progetto Maven

```
<project ...>
  <groupId>com.mycompany</groupId>
  <artifactId>my-app</artifactId>
  <version>1.0.0</version>
 
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```

### Struttura del progetto nel filesystem
La struttura di un progetto semplice Maven e' la seguente.

```
my-app
|-- pom.xml
 -- src
    |-- main
    |    -- java
    |        -- com
    |           -- mycompany
    |               -- myapp
    |                   -- App.java
     -- test
        -- java
            -- com
                -- mycompany
                    -- myapp
                        -- AppTest.java
```
                       
* `src` struttura standard per un progetto Java.
* `main` codice sorgente del progetto.
* `test` codice sorgente dei unit test .
* `pom.xml` il cuore del progetto con tutte le nostre configurazioni.
                 
 
### Maven come build automation tool
Maven definisce un ciclo di vita standard per il building, il test e il deployment di file di distribuzione Java.
* compilazione del codice sorgente
* esecuzione dei unit test  (ad esempio, tramite JUnit)
* generazione dei pacchetti, jar o war, a partire dal codice binario
* deployment dell' applicazione in ambiente di test o di produzione.

Per fare questo Maven usa i `Goals`.

### I plugins di Maven
Maven non e' altro che un esecutore di plug-in, alcuni presenti di default e altri che si possono aggiungere all'occorrenza.

### I Goals
Un `goal` e' lo specifico compito eseguito da un determinato plug-in. 
Tra i vari `goals` quelli piu' importanti per il ciclo di vita dello sviluppo sono:
- `compile` compila i sorgenti del progetto.
- `test` esegue i file test compilati usando uno specificabile framework per i test.
- `package` prende i file compilati ed esegue il package in un file JAR (o war,..ecc).
- `install` installa il package nel repository locale, da utilizzare come dipendenza in altri progetti in locale.
- `deploy` copia il pacchetto finale nel repository remoto per condividerlo con altri sviluppatori e progetti. 
- `clean` ripulisce gli artifact creati nelle precedenti esecuzioni.

I `goal` possono essere eseguiti in catena, esempio:
- `mvn clean install`

### Installazione Maven 
Installare Maven significa estrarre il file `.zip` nel filesystem. La struttura di Maven sara' la seguente:

```
MAVEN_HOME
|-- bin
    |-- mvn  
     -- (e altri file binari neccessari per eseguire Maven. Il file mvn sarebbe l'eseguibile di Maven)
 -- boot
 -- conf
    |-- settings.xml
 -- lib
    |-- (i .jar neccessari per eseguire Maven)
 -- LICENSE
 -- NOTICE
 -- README.txt
```

#### Maven settings.xml
La configurazione del Maven viene fatta nel file `settings.xml` si possono configurare il repository locale, i repository remoti, proxy, servers, mirrors, etc.
Per default il pecorso del repository locale si trova in `C:\Users\nome_utente\.m2\repository`, ma si puo' cambiare nell' elemento `<localRepository>`

```
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
  
  <localRepository>C:/Users/nome_utente/.m2/repository</localRepository>
 ```
 
#### Eseguire Maven dalla linea di commando
Per poter eseguire Maven dalla linea di commando bisogna aggiungere la cartella `/bin` alla *variabile di sistema* `PATH`. 
Esempio:
 
```
set MAVEN_HOME="c:/programs files/apache-maven-3.x.y"
set PATH=%MAVEN_HOME%/bin;%PATH%
```
Oppure usando il `SYSTEM VARIABLES` del sistema operativo.

Aprire un `prompt di comandi` e digitare.

```
mvn -v
```
Sulla console dovrebbe vedersi una cosa del genere:

```
C:\>mvn -v
Apache Maven 3.6.1 (d66c9c0b3152b2e69ee9bac180bb8fcc8e6af555; 2019-04-04T21:00:29+02:00)
Maven home: C:\Users\nome_utente\apache-maven-3.6.1\bin\..
Java version: 1.8.0_261, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jdk1.8.0_261\jre
Default locale: it_IT, platform encoding: Cp1252
OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
```

### Installare un progetto al Repository Locale

- `mvn clean` - Cancella la cartella `target`
- `mvn compile` - Legge dal `pom.xml` le `dependencies` dichiarate e cerca di recuperarle prima dal repository locale. 
Se i `jar` richiesti non sono presenti localmente, Maven si collega al repository centrale sul web, e scarica i pacchetti nel repository locale.
Poi compila i sorgenti creando una cartella `target` dove mette i file `.class` generati.
- `mvn package` - Partendo dai file binari generati nel goal `compile` impachetta e crea un file `jar` o `war` che lo mette prima dentro la cartella `target`
- `mvn install` - Copia dalla cartella target il `jar` o `war` creato nel goal `package` e lo mette nel repository locale, precisamente nel percorso:
`C:/Users/nome_utente/.m2/repository/com/mycompany/my-app/1.0.0/my-app-1.0.0.jar`

Il goal `install` implica l'esecuzione del goal `package`, il quale implica l'esecuzione di `compile`, per questo di solito si usa il seguente 
commando composto per poter pulire e poi installare un progetto.
- `mvn clean install`


Perche':
- `<groupId>com.mycompany</groupId>` rappresenta il nome del gruppo del progetto o di diversi progetti in comune fra di loro. 
- `<artifactId>my-app</artifactId>` rappresenta il nome del progetto
- `<version>1.0.0</version>` rappresenta la versione del progetto
- `<packaging>jar</packaging>` rappresenta il tipo di pacchetto che si vuole avere (war, jar etc.). 


### See
* [Sito ufficiale Maven](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)
* [Cosa e' Maven - Stackoverflow](https://stackoverflow.com/questions/13335351/what-does-maven-do-in-theory-and-in-practice-when-is-it-worth-to-use-it)
* [Goals in Maven](https://www.baeldung.com/maven-goals-phases)