# Phonegap kurs 22.03.2012 på Skuret

## Verktøy og oppgaver

1.  Installer Xcode fra App Store eller fra [Apple Developer Portal](https://developer.apple.com/) hvis du har medlemskap. Kurset er testet med versjon 4.2 av Xcode for Snow Leopard, men burde fungere fint for versjon 4.3 også.
2.  Last ned og installere siste versjon av [PhoneGap](http://phonegap.com/download) og dets innhold. Naviger til iOS-mappa og kjør installer.
3.  Start opp Xcode og velg "Connect to a repository"

    3.1 Lim inn git@github.com:andersmartinsen/Workshop-Cordova-iOS.git som location
    
    3.2 Trykk next
    
    3.3 Velg for eksempel Cordova som Name og trykk Clone
    
    3.4 Tilbake i hovedvinduet velg Open Other nede i venstre hjørnet
    
    3.5 Naviger deg fram mappen hvor du valgte å clone prosjektet og let etter filen som heter "workshop.cordova.xcodeproj" som er prosjektfilen. Velg denne, prosjektet med kode lastes inn, og du er så klar til å sette i gang med oppgavene.
4.  Trykk Cmd + R for å kjøre i gang simulatoren for å se hva som finnes allerede i applikasjonen

## Lenker

* [PhoneGap guide for iOS](http://phonegap.com/start#ios-x4)
* [PhoneGap API](http://docs.phonegap.com/en/1.5.0/)
* [jQuery Mobile](http://jquerymobile.com/demos/1.0.1/)
* [Twitter API console](https://dev.twitter.com/console)
* [jQuery - getJSON] (http://api.jquery.com/jQuery.getJSON/)

## Utgangspunkt/utdelt kode

Vi har laget en enkel webapp med [JQuery Mobile](http://jquerymobile.com/demos/1.1.0-rc.1/). Dette er en typisk en-sides-webapp, der alle delene av appen er egne div'er som lastes av JQuery Mobile. Startsiden (index.html) er en liste med lenker til oppgavesidene. Oppgavesidene inneholder den html'en du trenger for å putte inn selve funksjonaliteten.

Nederst i index.html har vi en script-tag som lager et nytt App-javascriptobjekt. I konstruktøren sender vi med ID'ene til elementene vi vil at skal gjøre ting, f.eks søke etter tweets fra nåværende lokasjon.

Selve applikasjonskoden finnes i filen app.js. Her lager vi et javascriptobjekt vi har kalt App. Metoden setupBindings() blir kjørt i konstruktøren og den bestemmer hva som skjer når man f.eks klikker på knapper. Da blir ulike metoder i App kjørt.

I app.js vil du ofte se this.enMetode(enParameter). Her referer this til App-objektet. Flere steder ser du var self = this. Dette gjør vi fordi inni andre funksjoner betyr this noe annet. For å fremdeles ha en referanse til App, slik at du kan kalle andre metoder i App-objektet, bruker vi self.enMetode(enParameter) isteden.

Vi har laget metoden renderTweets() som tar inn et objekt (typisk fra JSON) med tweets, legger dem til en html-liste og ber JQuery Mobile om å tegne lista. RenderUser(user) tar inn et user-objekt og dytter ulike felter fra dette objektet inn på riktig plass i html'en. Disse to metodene bruker du for å vise innhold du har hentet fra twitter sitt API (som du finner lenken til i koden). Vi bruker typisk $.ajax()-metoden for å gjøre disse nettverkskallene.

Når du har tegnet innholdet med renderTweets() eller renderUser(), må du også bytte til siden der den nye html'en ble satt inn. JQuery Mobile viser som standard bare den første siden den finner i index.html (en div med data-role=page). Dette gjøres med metoden $.mobile.changePage. Den tar inn et jquery-objekt, f.eks $("#min-side").

## Oppgaver

### Oppgave 1
Søk etter keywords på twitter og vis dem i en liste med tweets. Søkefeltet og søkeknappen er allerede knyttet opp til riktige metoder i App-objektet. Du må altså hente ut søkeordet fra søkefeltet og bruke $.ajax() til å hente svar i JSON-format. Dette sender du så til renderTweets(tweets) og bytter til resultatsiden (som også er ett attributt på App).

### Oppgave 2
Søke etter tweets i nærheten med geolokasjon. Her må du bruke phonegap til å finne lokasjonen din i bredde- og lengdegrad som du legger på som parametre i den oppgitte twitter-url'en. Bruk $.ajax() eller $.getJSON() som i forrige oppgave til å gjøre kallet. Du bruker renderTweets() og samme resultatside som i forrige oppgave.

### Oppgave 3
Her skal man kunne søke etter et brukernavn på twitter og så legge til kontaktinfo (bilde og navn i det minste) i kontaktlista på telefonen. I metoden searchByTwitterName() lager du selve twitter-søket. Metoden renderUser() tar inn objektet du får fra twitter og skriver du ut i html'en. I lagreAnsattTilKontaktLista() bruker du phonegap til å lagre brukeren i kontaktlista. Husk å bytt til "vis-bruker"-siden.

### Oppgave 4
Modifiser oppgave 2 (geolokasjon) til å først sjekke om telefon har nettverkstilgang. Hvis den ikke har nettverk, bruk PhoneGap sitt notification-API for å vise en fornuftig feilmelding.

### Oppgave 5
Her skal du lage en enkel lydopptaker som bruker telefonens standard lydopptaksfunksjon. Du bruker phonegap sitt Capture API for å ta opp lyden. Lag et Media-objekt av opptaket og spill det av. Du velger selv om du vil lage en ny metode i App for dette, eller om du bare vil legge det direkte på riktig sted i setupBindings().



## Tips

Du kan bruke Chrome til å teste appen din. På mac/linux kan du starte Chrome i en modus som tillater nettverkskallene vi trenger.
open -a /Applications/Google\ Chrome.app --args  -allow-file-access-from-files -disable-web-security