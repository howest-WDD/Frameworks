# Vue.js

## API data gebruiken

We bekijken hoe we data kunnen ophalen van een API en deze kunnen gebruiken in onze Vue app.

### API data ophalen

We gaan een API gebruiken die een lijst van personen teruggeeft. De API is te vinden op [https://randomuser.me/api/?results=10](https://randomuser.me/api/?results=10). Je kan deze URL in je browser openen en je krijgt een JSON object terug met 10 personen. De API en de data zijn hier volledig onbelangrijk. Het gaat erom dat we data ophalen van een externe bron.

We gaan deze data ophalen in onze Vue app. We gaan dit doen in de `setup` functie. We gaan hiervoor de `fetch` functie gebruiken. Deze functie is een asynchrone functie. Dit wil zeggen dat de functie niet meteen de data teruggeeft, maar dat we moeten wachten tot de data is opgehaald. We gaan dus een `await` gebruiken om te wachten op de data. We gaan ook een `try` en `catch` gebruiken om eventuele fouten op te vangen.

```js
import { ref } from 'vue';

export default {
  setup() {
    const users = ref([]);

    const fetchUsers = async () => {
      try {
        const response = await fetch('https://randomuser.me/api/?results=10');
        const data = await response.json();
        users.value = data.results;
      } catch (error) {
        console.log(error);
      }
    };

    fetchUsers();

    return {
      users,
    };
  },
};
```

We hebben nu de data opgehaald en in de variabele `users` geplaatst. We kunnen deze data nu gebruiken in onze template.

### Data tonen in de template

We gaan de data tonen in een lijst. We gaan hiervoor een `v-for` gebruiken. We gaan ook een `key` toevoegen aan de `v-for`. Dit is een unieke waarde die Vue gebruikt om de items in de lijst te identificeren. We gaan de `name` van de persoon gebruiken als `key`.

```html
<ul>
  <li v-for="user in users" :key="user.name">
    {{ user.name.first }} {{ user.name.last }}
  </li>

  <li v-if="users.length === 0">Geen gebruikers gevonden</li>
</ul>
```

We hebben ook een `v-if` toegevoegd om te controleren of er wel gebruikers zijn. Als er geen gebruikers zijn, dan tonen we een bericht.

### Loading state voorzien

We gaan ook een loading state voorzien. We gaan hiervoor een extra variabele `loading` voorzien. Deze variabele gaan we op `true` zetten voor we de data ophalen en op `false` zetten als de data is opgehaald.

```js
import { ref } from 'vue';

export default {
  setup() {
    const users = ref([]);
    const loading = ref(true);

    const fetchUsers = async () => {
      try {
        const response = await fetch('https://randomuser.me/api/?results=10');
        const data = await response.json();
        users.value = data.results;
        loading.value = false;
      } catch (error) {
        console.log(error);
      }
    };

    fetchUsers();

    return {
      users,
      loading,
    };
  },
};
```

We gaan nu de `loading` variabele gebruiken in de template. We gaan een `v-if` gebruiken om te controleren of de data aan het laden is. Als de data aan het laden is, dan tonen we een loading state. Als de data is opgehaald, dan tonen we de lijst met gebruikers.

```html
<ul v-if="!loading">
  <li v-for="user in users" :key="user.name">
    {{ user.name.first }} {{ user.name.last }}
  </li>

  <li v-if="users.length === 0">Geen gebruikers gevonden</li>
</ul>
```

### Loading state tonen

We gaan de loading state nog wat uitbreiden. We gaan de loading state tonen aan de hand van skelletons / ghosts.
We maken een paar lege skeletten aan voor we de data ophalen. We gaan deze skeletten tonen als de data aan het laden is. We gaan ook een extra div voorzien om de skeletten te tonen. We gaan deze div tonen als de data aan het laden is en verbergen als de data is opgehaald.

```html
<div v-if="loading">
  <div
    class="skeleton"
    v-for="user in 10"
    :key="user"
    style="height: 50px; margin-bottom: 10px;"
  ></div>
</div>
<ul v-else>
  <li v-for="user in users" :key="user.name">
    {{ user.name.first }} {{ user.name.last }}
  </li>

  <li v-if="users.length === 0">Geen gebruikers gevonden</li>
</ul>
```


### Error state voorzien

We gaan ook een error state voorzien. We gaan hiervoor een extra variabele `error` voorzien. Deze variabele gaan we op `false` zetten voor we de data ophalen en op `true` zetten als er een error is opgetreden.

```js
import { ref } from 'vue';

export default {
  setup() {
    const users = ref([]);
    const loading = ref(true);
    const error = ref(false);

    const fetchUsers = async () => {
      try {
        const response = await fetch('https://randomuser.me/api/?results=10');
        const data = await response.json();
        users.value = data.results;
        loading.value = false;
      } catch (error) {
        console.log(error);
        loading.value = false;
        error.value = true;
      }
    };

    fetchUsers();

    return {
      users,
      loading,
      error,
    };
  },
};
```

We gaan nu de `error` variabele gebruiken in de template. We gaan een `v-if` gebruiken om te controleren of er een error is opgetreden. Als er een error is opgetreden, dan tonen we een error state. Als er geen error is opgetreden, dan tonen we de lijst met gebruikers.

```html
<ul v-if="!loading && !error">
  <li v-for="user in users" :key="user.name">
    {{ user.name.first }} {{ user.name.last }}
  </li>

  <li v-if="users.length === 0">Geen gebruikers gevonden</li>
</ul>

<p v-if="error">Er is een fout opgetreden</p>
```

### Error state tonen

We gaan de error state nog wat uitbreiden. We gaan de error state tonen in een `alert`-box. We gaan hiervoor een extra variabele `errorMessage` voorzien. Deze variabele gaan we op `null` zetten voor we de data ophalen en op de error message zetten als er een error is opgetreden.

```js
import { ref } from 'vue';

export default {
  setup() {
    const users = ref([]);
    const loading = ref(true);
    const error = ref(false);
    const errorMessage = ref(null);

    const fetchUsers = async () => {
      try {
        const response = await fetch('https://randomuser.me/api/?results=10');
        const data = await response.json();
        users.value = data.results;
        loading.value = false;
      } catch (error) {
        console.log(error);
        loading.value = false;
        error.value = true;
        errorMessage.value = error.message;
      }
    };

    fetchUsers();

    return {
      users,
      loading,
      error,
      errorMessage,
    };
  },
};
```

We gaan nu de `errorMessage` variabele gebruiken in de template. We gaan een `v-if` gebruiken om te controleren of er een error is opgetreden. Als er een error is opgetreden, dan tonen we een error state. Als er geen error is opgetreden, dan tonen we de lijst met gebruikers.

```html
<ul v-if="!loading && !error">
  <li v-for="user in users" :key="user.name">
    {{ user.name.first }} {{ user.name.last }}
  </li>

  <li v-if="users.length === 0">Geen gebruikers gevonden</li>
</ul>

<p v-if="error">
  Er is een fout opgetreden: {{ errorMessage }}
</p>
```

### Error state verbergen

We gaan de error state nog wat uitbreiden. We gaan de error state verbergen als er op de `close` knop wordt geklikt. We gaan hiervoor een extra functie `hideError` voorzien. Deze functie gaan we gebruiken in de `v-on` directive om de error state te verbergen.

```js
import { ref } from 'vue';

export default {
  setup() {
    const users = ref([]);
    const loading = ref(true);
    const error = ref(false);
    const errorMessage = ref(null);

    const fetchUsers = async () => {
      try {
        const response = await fetch('https://randomuser.me/api/?results=10');
        const data = await response.json();
        users.value = data.results;
        loading.value = false;
      } catch (error) {
        console.log(error);
        loading.value = false;
        error.value = true;
        errorMessage.value = error.message;
      }
    };

    const hideError = () => {
      error.value = false;
    };

    fetchUsers();

    return {
      users,
      loading,
      error,
      errorMessage,
      hideError,
    };
  },
};
```

We gaan nu de `hideError` functie gebruiken in de template. We gaan een `v-on` (`@`) gebruiken om te controleren of er op de `close` knop wordt geklikt. Als er op de `close` knop wordt geklikt, dan verbergen we de error state.

```html
<ul v-if="!loading && !error">
  <li v-for="user in users" :key="user.name">
    {{ user.name.first }} {{ user.name.last }}
  </li>

  <li v-if="users.length === 0">Geen gebruikers gevonden</li>
</ul>

<p v-if="error">
  Er is een fout opgetreden: {{ errorMessage }}
  <button @click="hideError">Close</button>
</p>
```
