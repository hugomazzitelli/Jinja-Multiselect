# Jinja-Multiselect pour Flask

Ce composant est un widget multiselect personnalisable conçu pour les projets Flask utilisant Bootstrap. Tout le code (HTML, CSS et JavaScript) est contenu dans un seul fichier `multiselect.html` pour faciliter son intégration et sa maintenance.

## Fonctionnalités

- **Sélection multiple** : L'utilisateur peut sélectionner plusieurs options, qui s'affichent sous forme de badges.
- **Désactivation dynamique** : Possibilité de désactiver certaines options (pour éviter des choix conflictuels) via une méthode publique.
- **Customisable** : Personnalisez facilement les classes CSS utilisées pour le conteneur, l'input, les badges et le menu déroulant.
- **Facile à intégrer** : Le composant est fourni dans un seul fichier, sans dépendances externes (hors Bootstrap).

## Installation

1. **Clonez ou téléchargez** ce dépôt depuis le GitHub.
2. **Placez** le fichier `multiselect.html` dans le répertoire de vos templates Flask (par exemple, `templates/components/`).
3. **Assurez-vous** que Bootstrap est chargé dans votre projet pour bénéficier des styles par défaut.

## Utilisation

### 1. Importation du composant

Dans votre template Jinja, importez le macro :

```jinja
{% from 'components/multiselect.html' import multi_select %}
```

### 2. Appel du composant

Voici un exemple simple d’utilisation :

```jinja
{% set options = ["Option 1", "Option 2", "Option 3"] %}

<form>
  {{ multi_select(
      name='my_multiselect',
      options=options,
      placeholder="Sélectionnez des options...",
      disabled_options=[],        {# Liste d'options à désactiver (optionnel) #}
      onChange="onMultiselectChange",  {# Nom de la fonction JS à appeler lors d'un changement (optionnel) #}
      preselected=["Option 2"]    {# Valeurs pré-sélectionnées (optionnel) #}
  ) }}
  <button type="submit" class="btn btn-primary">Envoyer</button>
</form>
```

### 3. Paramètres du composant

| Paramètre             | Type             | Valeur par défaut                                       | Description                                                                                  | Exemple                                     |
|-----------------------|------------------|---------------------------------------------------------|----------------------------------------------------------------------------------------------|---------------------------------------------|
| **name** <span style="background-color:#d9534f;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Required</span>            | `String`         | —                                                       | Nom de l'input caché utilisé pour stocker la sélection.                                      | `"my_multiselect"`                          |
| **options** <span style="background-color:#d9534f;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Required</span>         | `Array<String>`  | —                                                       | Tableau des options disponibles.                                                             | `["Option 1", "Option 2", "Option 3"]`        |
| **placeholder** <span style="background-color:#d9534f;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Required</span>     | `String`         | —                                                       | Texte affiché dans l'input avant la saisie.                                                  | `"Sélectionnez des options..."`             |
| **disabled_options** <span style="background-color:#5bc0de;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Optional</span> | `Array<String>`  | `[]`                                                    | Liste des options à désactiver dans le dropdown.                                             | `["Option 2"]`                              |
| **onChange** <span style="background-color:#5bc0de;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Optional</span>         | `String`         | `null`                                                  | Nom d'une fonction JavaScript globale appelée lors d'un changement de sélection.             | `"onMultiselectChange"`                     |
| **preselected** <span style="background-color:#5bc0de;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Optional</span>     | `Array<String>`  | `[]`                                                    | Liste des options déjà sélectionnées lors du chargement.                                     | `["Option 2"]`                              |
| **container_class** <span style="background-color:#5bc0de;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Optional</span> | `String`         | `"multi-select-container"`                              | Classe CSS du conteneur global. **(Les classes réservées par le composant sont `ms-c`.)**      | `"custom-container"`                        |
| **input_class** <span style="background-color:#5bc0de;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Optional</span>     | `String`         | `"multi-select-input"`                                  | Classe CSS de l'input de saisie. **(Les classes réservées par le composant sont `ms-i`.)**      | `"custom-input"`                            |
| **badge_class** <span style="background-color:#5bc0de;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Optional</span>     | `String`         | `"badge bg-primary me-1 mb-1 d-flex align-items-center"`  | Classe CSS des badges affichant les options sélectionnées.                                   | `"custom-badge"`                            |
| **dropdown_class** <span style="background-color:#5bc0de;color:white;padding:2px 4px;font-size:0.8em;border-radius:3px;">Optional</span>  | `String`         | `"dropdown-menu w-100 shadow-sm"`                       | Classe CSS du menu déroulant. **(Les classes réservées par le composant sont `ms-d`.)**         | `"custom-dropdown"`                         |

### 4. Personnalisation des styles

Pour personnaliser l’apparence, vous pouvez passer vos propres classes CSS via les paramètres du macro ou utiliser les classes de votre librairie frontend (BootStrap, Tailwind, etc...). Par exemple :

```jinja
{{ multi_select(
    name='my_multiselect',
    options=options,
    placeholder="Tapez pour rechercher...",
    onChange="onMultiselectChange",
    preselected=[],
    container_class="custom-class",
    input_class="custom-class text-secondary",
    badge_class="custom-class p-1",
    dropdown_class="custom-class border-0"
) }}
```
> :warning: **Warning:** Ne pas utiliser les classes `ms-c`, `ms-i` et `ms-d` ailleurs sur votre page, car elles sont réservées par le composant pour garantir son bon fonctionnement.

Fonction Callback

Définissez une fonction JavaScript pour traiter les changements de sélection. Par exemple :
```js
function onMultiselectChange(selectedItems, container) {
  console.log("Sélection modifiée :", selectedItems);
  // Ajoutez ici votre logique personnalisée.
}
```
