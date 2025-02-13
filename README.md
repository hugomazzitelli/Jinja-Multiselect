# Jinja-Multiselect
Une version tunning du multiselect de la librairie Select2

Voici le contenu du fichier README.md :

# Composant Multiselect pour Flask

Ce composant est un widget multiselect personnalisable conçu pour les projets Flask utilisant Bootstrap. Tout le code (HTML, CSS et JavaScript) est contenu dans un seul fichier `multiselect.html` pour faciliter son intégration et sa maintenance.

## Fonctionnalités

- **Sélection multiple** : L'utilisateur peut sélectionner plusieurs options, qui s'affichent sous forme de badges.
- **Désactivation dynamique** : Possibilité de désactiver certaines options (pour éviter des choix conflictuels) via une méthode publique.
- **Customisable** : Personnalisez facilement les classes CSS utilisées pour le conteneur, l'input, les badges et le menu déroulant.
- **Facile à intégrer** : Le composant est fourni dans un seul fichier, sans dépendances externes (hors Bootstrap).

## Installation

1. **Clonez ou téléchargez** ce dépôt depuis le GitHub de l'entreprise.
2. **Placez** le fichier `multiselect.html` dans le répertoire de vos templates Flask (par exemple, `templates/components/`).
3. **Assurez-vous** que Bootstrap est chargé dans votre projet pour bénéficier des styles par défaut.

## Utilisation

### 1. Importation du composant

Dans votre template Jinja, importez le macro :

```jinja
{% from 'components/multiselect.html' import multi_select %}
```

2. Appel du composant

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

3. Paramètres du composant

| Paramètre            | Type              | Valeur par défaut                  | Description                                                                                  | Exemple                                     | Required |
|----------------------|-------------------|------------------------------------|----------------------------------------------------------------------------------------------|---------------------------------------------|----------|
| **name**             | `String`          | —                                  | Nom de l'input caché utilisé pour stocker la sélection.                                      | `"my_multiselect"`                          | Yes      |
| **options**          | `Array<String>`   | —                                  | Tableau des options disponibles.                                                             | `["Option 1", "Option 2", "Option 3"]`        | Yes      |
| **placeholder**      | `String`          | —                                  | Texte affiché dans l'input avant la saisie.                                                  | `"Sélectionnez des options..."`             | Yes      |
| **disabled_options** | `Array<String>`   | `[]`                               | Liste des options à désactiver dans le dropdown.                                | `["Option 2"]`                              | No       |
| **onChange**         | `String`          | `null`                             | Nom d'une fonction JavaScript globale à appeler lors d'un changement.            | `"onMultiselectChange"`                     | No       |
| **preselected**      | `Array<String>`   | `[]`                               | Liste des options déjà sélectionnées lors du chargement.                          | `["Option 2"]`                              | No       |
| **container_class**  | `String`          | `"multi-select-container"`         | Classe CSS du conteneur global.                                                 | `"custom-container"`                        | No       |
| **input_class**      | `String`          | `"multi-select-input"`             | Classe CSS de l'input de saisie.                                                | `"custom-input"`                            | No       |
| **badge_class**      | `String`          | `"badge bg-primary"`               | Classe CSS des badges affichant les options sélectionnées.                         | `"custom-badge"`                            | No       |
| **dropdown_class**   | `String`          | `"dropdown-menu"`                  | Classe CSS du menu déroulant.                                                   | `"custom-dropdown"`                         | No       |

4. Personnalisation des styles

Pour personnaliser l’apparence, vous pouvez passer vos propres classes CSS via les paramètres du macro ou utiliser les classes de votre librairie frontend (BootStrap, Tailwind, etc...). Par exemple :

```jinja
{{ multi_select(
    name='my_multiselect',
    options=options,
    placeholder="Tapez pour rechercher...",
    onChange="onMultiselectChange",
    preselected=[],
    container_class="custom-container",
    input_class="custom-input",
    badge_class="custom-badge",
    dropdown_class="custom-dropdown"
) }}
```

Fonction Callback

Définissez une fonction JavaScript pour traiter les changements de sélection. Par exemple :
```js
function onMultiselectChange(selectedItems, container) {
  console.log("Sélection modifiée :", selectedItems);
  // Ajoutez ici votre logique personnalisée.
}
```
