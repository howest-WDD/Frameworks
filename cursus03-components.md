# Vue.js

## Componenten

In Vue.js 3 kun je met componenten werken om je code te structureren en herbruikbaarheid te bevorderen.

Hier zijn de basisstappen om met componenten te werken in Vue.js 3:

1.  **Componenten aanmaken:**
    Om een component te maken, kun je een .vue-bestand maken. Dit bestand bevat meestal drie secties: template, script, en style. Hier is een eenvoudig voorbeeld van een componentbestand met de naam `MijnComponent.vue`:

    ```html
    <template>
      <div>
        <h1>{{ message }}</h1>
      </div>
    </template>

    <script>
      export default {
        setup() {
          return {
            message: 'Dit is mijn Vue.js component.',
          };
        },
      };
    </script>

    <style scoped>
      /* Stijlen specifiek voor dit component */
    </style>
    ```

2.  **Registreren van componenten**: Nadat je een component hebt gemaakt, moet je dit registreren in de Vue-instantie of in een ander component waarin je het wilt gebruiken. Dit kan gedaan worden in het main.js-bestand waar je je Vue-instantie maakt, of in een ander componentbestand.

    ```html
    // App.vue
    <script setup>
      import MijnComponent from './components/MijnComponent.vue';
    </script>
    ```

3.  **Gebruik van componenten:**
    Je kunt een component in je template gebruiken door de component-tag te gebruiken die je hebt gedefinieerd bij de registratie. Bijvoorbeeld:

    ```html
    <template>
      <div>
        <MijnComponent></MijnComponent>
      </div>
    </template>
    ```

4.  **Props:**
    Om gegevens van de oudercomponent naar het kindcomponent door te geven, kun je gebruikmaken van props. Definieer prop-namen in je kindcomponent en geef waarden door vanuit de oudercomponent. Hier is een voorbeeld:

    ```js
    <script>
      export default {
        props: ['text'],
      };
    </script>
    ```

    En in de oudercomponent:

    ```html
    <mijn-component :text="bericht"></mijn-component>
    ```

    Zorg ervoor dat `bericht` in de oudercomponent is gedefinieerd.

5. **Emit:**
    Soms wil je terug van de component naar de bovenliggende code iets sturen of terug geven. Daarvoor dienen emits. Je kan een emit aanmaken in de child component en deze oproepen in de child component. Hier is een voorbeeld:

    ```vue
    <script>
      export default {
        emits: ['update'],
        setup(props, { emit }) {
          const update = () => {
            emit('update', 'Dit is een bericht vanuit de child component');
          };

          return {
            update,
          };
        },
      };
    </script>
    ```

    En in de oudercomponent:

    ```html
    <mijn-component @update="update"></mijn-component>
    ```

    Zorg ervoor dat `update` in de oudercomponent is gedefinieerd.


Dit zijn de basisstappen om met componenten in Vue.js 3 te werken. Met deze structuur kun je componenten maken en ze in je toepassing hergebruiken om je code schoon en goed georganiseerd te houden.

## Script setup aanpak

In Vue.js 3 kun je de script setup aanpak gebruiken om je componenten te schrijven. Dit is een nieuwe manier om componenten te schrijven die je helpt om je code schoon en goed georganiseerd te houden. Hier zijn de basisstappen om de script setup aanpak te gebruiken:

  1. **Props:**
    Om props te gebruiken in de script setup aanpak, kun je de `defineProps` functie gebruiken. Hier is een voorbeeld:

    ```vue
    <script setup>
      import { defineProps } from 'vue';

      const props = defineProps({
        text: String,
      });
    </script>
    ```

  2. **Emit:**
    Om emits te gebruiken in de script setup aanpak, kun je de `defineEmits` functie gebruiken. Hier is een voorbeeld:

    ```vue
    <script setup>
      import { defineEmits } from 'vue';

      const emits = defineEmits(['update']);
    </script>
    ```


