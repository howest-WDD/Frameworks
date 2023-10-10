# Vue

## Wat is Vue?

Vue (uitgesproken als /vjuː/, zoals "view") is een JavaScript-framework voor het bouwen van gebruikersinterfaces. Het bouwt voort op standaard HTML, CSS en JavaScript en biedt een declaratief en componentgebaseerd programmeermodel dat je helpt om efficiënt gebruikersinterfaces te ontwikkelen, of ze nu eenvoudig of complex zijn.

## Starten met Vue 3

Als we met de Vue aan de slag gaan, hebben we een paar tools nodig:

1. [Node.js](https://nodejs.org/en/) met npm (Node Package Manager)
2. [VS Code](https://code.visualstudio.com/) als editor
3. [Volar Extension](https://marketplace.visualstudio.com/items?itemName=Vue.volar) voor VS Code

### Node.js installeren

Om te kunnen werken met Vue.js moeten we gebruik maken van Node.js en moeten we op ons systeem te installeren, volg daarom deze stappen:

1. **Download Node.js**: Ga naar de officiële Node.js-website op [https://nodejs.org/](https://nodejs.org/).

2. **Kies een versie**: Op de website vind je twee versies van Node.js: LTS (Long Term Support) en Current. Voor de meeste gebruikers is de LTS-versie de beste keuze, omdat deze stabiel is en wordt ondersteund voor een langere periode. Klik op de LTS-versie om deze te downloaden.

3. **Kies je besturingssysteem**: Selecteer het juiste installatiepakket voor je besturingssysteem. Er zijn installatieprogramma's beschikbaar voor Windows, macOS en verschillende Linux-distributies.

4. **Start de installatie**: Nadat het installatieprogramma is gedownload, voer je het uit en volg je de installatie-instructies op het scherm.

5. **Verifieer de installatie**: Om te controleren of Node.js correct is geïnstalleerd, open je een terminal of opdrachtprompt en voer je de volgende opdrachten uit:
   ```bash
   node -v
   npm -v
   ```
   Als alles goed is verlopen, zou je de versienummers van Node.js en npm moeten zien.

### Installeren van Vue CLI

Als je Vue CLI (Command Line Interface) nog niet op je systeem hebt geïnstalleerd, dan moet je dit eerst, éénmalig, doen met het volgende npm-commando in je terminal:

```bash
npm install -g @vue/cli
```

## Een Leeg Vue 3-project aanmaken

Om een leeg Vue 3-project aan te maken, kun je de Vue CLI (Command Line Interface) gebruiken.

Volg deze stappen:

1.  Navigeer in de Terminal van VS Code naar de map waar je de projectmap wilt maken en voer het volgende commando uit om een nieuw Vue 3-project te genereren, je hoeft geen submap aan te maken, Vue CLI zal dit voor je doen:

    ```bash
    npm create vue@latest
    ```

2.  Nadat je het commando hebt uitgevoerd, zal Vue CLI je vragen om een `naam` te kiezen voor je project. Deze naam mag geen hoofdletters bevatten en mag geen spaties bevatten en zal gebruikt worden als naam voor de map waarin je project wordt aangemaakt. Je kunt ook een punt `.` gebruiken om het project in de huidige map aan te maken zonder eerst een submap te maken.
    Nadat je een naam hebt gekozen, zal Vue CLI je vragen om een aantal opties te kiezen. We kiezen voor elke optie die ons voorgeschoteld wordt 'No' of drukken gewoon op 'Enter'.

    ```bash
    ✔ Project name: project-naam
    ✔ Add TypeScript? … No / Yes
    ✔ Add JSX Support? … No / Yes
    ✔ Add Vue Router for Single Page Application development? … No / Yes
    ✔ Add Pinia for state management? … No / Yes
    ✔ Add Vitest for Unit testing? … No / Yes
    ✔ Add an End-to-End Testing Solution? … No / Cypress / Playwright
    ✔ Add ESLint for code quality? … No / Yes
    ✔ Add Prettier for code formatting? … No / Yes

    Scaffolding project in ./project-naam
    Done.
    ```

3.  Het project staat nu klaar in de map `project-naam`. We moeten enkel nog de dependencies (de benodigde node_modules) installeren. Let op, je moet wel eerst navigeren naar de map `project-naam`!

    ```bash
    cd project-naam
    ```

4.  Installeer de `dependencies` met het volgende commando:

    ```bash
    npm i
    ```

    Bij deze stap worden alle benodigde `node_modules` geïnstalleerd. Dit kan even duren.
    Als je een foutmelding krijgt, probeer dan eerst het commando `npm i` nog eens uit te voeren.

    ⚠️ Let op indien je met git(hub) werkt. De `node_modules` map mag niet worden gecommit/geüpload naar git(hub). Vergeet dus niet een _.gitingore_ file aan te maken en daarin de `node_modules` map te vermelden.

5.  Het project is nu klaar om te starten. Je kunt het project starten met het volgende commando:

    ```bash
    npm run dev
    ```

    Als alles tot hiertoe goed verlopen is, kan je nu surfen naar http://localhost:5173/ en zou je de standaard Vue 3-pagina moeten zien.

## Vue 3 project structuur

Een Vue.js 3-project heeft doorgaans een specifieke projectstructuur die is georganiseerd rond de Vue-cli (Vue Command Line Interface) en de aanbevolen bestandsindeling. Hier is een algemene projectstructuur voor een Vue.js 3-project:

```bash
project-naam/
|-- node_modules/          # Hier worden alle afhankelijkheden geïnstalleerd
|-- public/                # Openbare bestanden (toegankelijk via de browser)
|   |-- index.html         # Hoofd-HTML-bestand
|-- src/                   # Broncode van je Vue.js-applicatie
|   |-- assets/            # Statische bestanden zoals afbeeldingen en stijlen
|   |-- components/        # Vue-componenten
|   |-- views/             # Vue-weergaven of pagina's
|   |-- App.vue            # Hoofd Vue-component
|   |-- main.js            # Ingangspunt van je applicatie
|-- .gitignore             # Git-ignore-bestand om bestanden/ mappen uit te sluiten van versiebeheer
|-- package.json           # NPM-pakketconfiguratie
|-- README.md              # Documentatie voor je project
|-- vite.config.js         # Vue-cli configuratiebestand
|-- ...                    # Andere bestanden
```

Hier is een beknopte uitleg van de belangrijkste mappen en bestanden:

- **node_modules:** Hier worden alle projectafhankelijkheden opgeslagen na het uitvoeren van npm install.

- **public:** Dit is de map voor openbare bestanden die direct toegankelijk zijn via de browser, zoals favicon.ico

- **src:** Dit is waar je de broncode van je Vue.js-applicatie plaatst. Dit omvat componenten, weergaven, stijlen, enz.

  - **assets:** Hier kun je statische bestanden zoals afbeeldingen, pictogrammen en stijlen opslaan die worden gebruikt in je app.

  - **components:** Hier kan je herbruikbare Vue-componenten plaatsen die in je applicatie worden gebruikt.

  - **views:** Dit is waar je de Vue-weergaven of pagina's plaatst die corresponderen met verschillende routes in je app (later)

  - **App.vue**: Het hoofdcomponent van je applicatie waarin je de router (later) en de lay-out van je app definieert.

  - **main.js**: Het ingangspunt van je applicatie waarin je Vue initialisatie en andere configuratie kunt doen.

- **index.html:** Dit is het hoofd-HTML-bestand van je applicatie. Het bevat een `<div id="app">` waarin je Vue-app wordt gemonteerd.

- **andere bestanden:** Er zijn ook andere bestanden zoals package.json, vite.config.js, enz. die worden gebruikt voor het configureren van je Vue.js-applicatie.
