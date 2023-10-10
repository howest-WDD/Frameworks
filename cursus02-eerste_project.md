# Vue

## App.vue

Het App.vue-bestand is meestal het belangrijkste Vue-bestand in een Vue.js-toepassing. Het wordt vaak gebruikt als de "root" van de applicatie, waarin andere Vue-componenten worden ingevoegd en getoond. Hier is een voorbeeld van hoe een App.vue-bestand eruit zou kunnen zien:

```html
<template>
  <div id="app">
    <header>
      <h1>Mijn Vue.js Toepassing</h1>
    </header>
    <main>
      <p>Welkom bij mijn toepassing!</p>
    </main>
    <footer>
      <p>&copy; Mijn Bedrijf</p>
    </footer>
  </div>
</template>

<script>
  export default {
    name: 'App',
    setup() {
      return {};
    },
  };
</script>

<style>
  /* Globale stijlen voor de hele toepassing */
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
  }
</style>
```

Laten we de structuur van dit App.vue-bestand uitleggen:

- `<template>`: Dit gedeelte bevat de HTML-structuur van de applicatie. Hierin kun je de lay-out van je applicatie definiëren. In dit voorbeeld is er een header, een hoofdgedeelte en een footer.

- `<script>`: Dit gedeelte bevat de JavaScript-logica voor de `App`-component. In dit geval wordt de component geëxporteerd met de naam 'App'. Je kunt hier ook andere logica toevoegen die betrekking heeft op de root van je applicatie.

- `<style>`: Dit gedeelte bevat CSS-stijlen die van toepassing zijn op de hele applicatie. Deze stijlen zijn van toepassing op elementen binnen de `App`-component. Je kunt hier globale stijlen voor je applicatie definiëren.

Het `App.vue`-bestand is vaak het startpunt van een Vue.js-toepassing en wordt gebruikt om andere componenten op te roepen. Het bevat ook algemene stijlinstellingen voor de hele toepassing.

## Databinding

We gaan nu een eerste databinding maken. We maken een `input veld` waarin we onze naam kunnen ingeven. Deze naam gaan we dan tonen in de paragraaf eronder.

- Maak een input veld aan in de `<template></template>` van `App.vue`.
- Wat is er allemaal nodig bij een goed input-veld?
- Nu willen we dit input veld binden aan een variabele in de data van `App.vue`.
  Hiervoor moeten we een aantal stappen doorlopen.

### Klaarzetten van de setupfunctie

Eerst en vooral gaan we het JavaScript gedeelte van een Vue-component klaarzetten tussen de `<script></script>`-tags:

```js
export default {
  setup() {
    return {};
  },
};
```

De `export default` functie zorgt ervoor dat we een echte Vue-component maken. De setup functie is een speciale functie die we gebruiken om data en functies klaar te zetten voor gebruik in de template.

### Aanmaken van een variabele

Het aanmaken van een variabele in Vue gaat iets anders dan in JavaScript. We gebruiken hiervoor een stukje code van Vue.js, namelijk een `ref`. Om gebruik te kunnen maken van een `ref` moeten we deze eerst importeren. Dit doen we met de volgende code:

```js
import { ref } from 'vue';

export default {
  setup() {
    const name = ref('Martijn');

    return {
      name,
    };
  },
};
```

Merk op dat we de variabele definiëren als een `const` en niet als een `let`.
Dit komt omdat we de variabele niet gaan overschrijven, maar we de waarde van de variabele geen aanpassen door de `ref` te gebruiken.

We hebben deze aangemaakte variabele ook in het `return`-gedeelte gezet. Dit betekent dat het beschikbaar is voor gebruik in de template. Variabelen die niet in de return gezet worden zijn niet bruikbaar buiten de setupfunctie.

### Gebruiken van een variabele in de template.

We kunnen nu de variabele `name` gebruiken in de template. Om deze te tonen in de template gebruiken we de dubbele accolades of moustache `{{ }}`-syntax:

```html
<p>Hello, {{ name }}</p>
```

Bij het testen zien we dat dit werkt. Nu gaan we nog een stapje verder. Ons input-veld staat te poppelen om ook iets te mogen doen. We gaan de variabele `name` binden aan het input-veld. Dit doen we met de `v-model`-directive:

```html
<input type="text" v-model="name" />
```

Je ziet dat alles wat je in het input-veld typt, ook meteen getoond wordt in de paragraaf er onder. Maar ook omgekeerd, als je de variabele aanpast, wordt ook het input-veld aangepast.

- Hoe zou je dit gedaan hebben zonder Vue.js?
- Wat is nog handig om op deze manier data te tonen?
- We gaan ook nog een knop toevoegen die de naam terug op 'Martijn' zet:

```html
<button @click="name = 'Martijn'">Reset</button>
```

Je ziet dat je rechtstreeks in de Vue code een variabele kan aanpassen. Dit is soms eens handig, maar dat gaan we eigenlijk niet zo doen. We maken liever een aparte functie die we dan aanroepen.

```html
<button @click="resetName">Reset</button>
```

De functie `resetName` moeten we nu nog aanmaken in de setupfunctie:

```js
const resetName = function () {
  name.value = 'Mighty Marty';
};
```

Indien je een functie maakt, die verder in de app gebruikt wordt, dan moet je deze ook exporteren:

```js
import { ref } from 'vue';

export default {
  setup() {
    const name = ref('Martijn');

    const resetName = function () {
      name.value = 'Mighty Marty';
    };

    return {
      name,
      resetName,
    };
  },
};
```

- Probeer nu eens een nieuwe knop te maken en deze te koppelen aan een functie die de string omdraait. Schrijf ook de nodige functie hiervoor. Probeer het bijvoorbeeld eens met de namen: 'hannah', 'reinier' of 'bob'. Kijk of de letters omgedraaid worden.
- Wat valt er op aan onze ref-variabele? Wat is er anders in de JS, dan in de HTML?

# v-for

De `v-for` directive is een van de belangrijkste directives in Vue.js en wordt gebruikt om door een array of een object te itereren en herhaalde elementen in de DOM te genereren op basis van de gegevens in de array of het object. Hier is hoe v-for in Vue.js werkt:

```html
<div v-for="item in items" :key="item.id">{{ item.text }}</div>
```

`v-for="item in items"`: Dit is de v-for directive. `item` is de alias die je kiest om elk element in de array/object mee aan te spreken, en `items` is de array/object waar je doorheen wilt lopen.

`:key="item.id"`: Dit is optioneel, maar wordt sterk aanbevolen. Het dient om de DOM-elementen uniek te identificeren. Het is belangrijk om een unieke sleutelwaarde aan elk herhaald element toe te voegen om de efficiëntie van Vue's reactiviteitssysteem te verbeteren.

`{{ item.text }}`. Dit is de inhoud van elk herhaald element. Hier kun je toegang krijgen tot de gegevens in het huidige element van de array/object en deze weergeven in de DOM.

Hier is een voorbeeld met een array:

```html
<template>
  <div>
    <ul>
      <li v-for="item in items" :key="item.id">{{ item.text }}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    setup() {
      return {
        items: [
          { id: 1, text: 'Item 1' },
          { id: 2, text: 'Item 2' },
          { id: 3, text: 'Item 3' },
        ],
      };
    },
  };
</script>
```

In dit voorbeeld zal v-for de`li`-elementen herhalen voor elk object in de items array, waarbij de text-waarde van elk object wordt weergegeven. v-for is zeer krachtig en flexibel en kan worden gebruikt in combinatie met andere Vue-functionaliteiten om dynamische lijsten en herhaalde elementen in je Vue.js-applicatie te maken. Het is een essentiële tool voor het dynamisch genereren van inhoud op basis van gegevens. We gaan nu een array maken van namen. We gaan deze array tonen in een lijstje. - Probeer dit even zelf door een lijstje aan te maken in de data:

```js
const names = ref(['Dieter', 'Christophe', 'Lien', 'Martijn']);
```

Vergeet niet om deze lijst te returnen in de setupfunctie. - Maak nu een lijstje aan in de template met de `v-for` directive. - Gebruik de `:key`-directive om de lijst uniek te maken. - Gebruik de `{{ }}`-syntax om de naam te tonen.

```html
<ul>
  <li v-for="name in names" :key="name">{{ name }}</li>
</ul>
```

## v-if / v-else

`v-if` en `v-else` zijn Vue.js directives die worden gebruikt voor conditionele weergave van elementen in de gebruikersinterface (UI). Ze stellen je in staat om bepaalde delen van je HTML-structuur weer te geven of te verbergen op basis van de waarde van een bepaalde voorwaarde.

Hier is een korte uitleg van beide directives:

`v-if`: Deze directive wordt gebruikt om een element in de DOM weer te geven als een opgegeven voorwaarde waar is. Als de voorwaarde waar is, wordt het element weergegeven; anders wordt het element uit de DOM verwijderd.

`v-else`: Deze directive wordt gebruikt in combinatie met v-if. Het wordt geplaatst op een element direct na een v-if element en wordt weergegeven als de voorwaarde van v-if niet waar is.
Hier is een voorbeeld in Vue.js:

```js
<template>
  <div>
    <p v-if="showMessage">Dit bericht wordt weergegeven als showMessage waar is.</p>
    <p v-else>Dit bericht wordt weergegeven als showMessage niet waar is.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showMessage: true // Verander dit om te testen
    };
  }
};
</script>
```

In dit voorbeeld zal de eerste `p` worden weergegeven als showMessage waar is, en de tweede `p` wordt weergegeven als showMessage niet waar is.
