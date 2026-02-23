# hajime-ui

Bibliothèque de composants [Django Cotton](https://django-cotton.com) réutilisables, stylés avec Tailwind CSS et compatibles HTMX + Alpine.js.

---

## 1. Installation

```bash
pip install git+ssh://git@github.com/yanis-san/hajime-ui.git@v0.1.1
```

## 2. Configuration

Ajouter dans `settings.py` :

```python
INSTALLED_APPS = [
    ...
    "django_cotton",  # requis
    "hajime_ui",      # ← ajouter
]
```

Aucune config supplémentaire — Django trouve les templates du package automatiquement via `INSTALLED_APPS`.

---

## 3. Composants disponibles

### `<c-ui.btn>`

```html
<c-ui.btn href="{% url 'login' %}" variant="primary">Se connecter</c-ui.btn>
<c-ui.btn type="submit" variant="outline" size="sm">Annuler</c-ui.btn>
```

| Prop | Valeurs |
|---|---|
| `variant` | `primary` · `outline` · `ghost` · `danger` |
| `size` | `sm` · `md` · `lg` |
| `href` | URL (génère un `<a>`) |
| `type` | `button` · `submit` |

---

### `<c-ui.badge>`

```html
<c-ui.badge variant="orange">Nouveau</c-ui.badge>
<c-ui.badge variant="gray">Brouillon</c-ui.badge>
```

| Prop | Valeurs |
|---|---|
| `variant` | `gray` · `orange` · `green` · `red` · `blue` |

---

### `<c-ui.alert>`

```html
<c-ui.alert type="success">Profil mis à jour.</c-ui.alert>
<c-ui.alert type="error">Une erreur est survenue.</c-ui.alert>
```

| Prop | Valeurs |
|---|---|
| `type` | `success` · `error` · `warning` · `info` |

---

### `<c-ui.avatar>`

```html
<c-ui.avatar :user="request.user" size="md" />
```

| Prop | Valeurs |
|---|---|
| `user` | objet `User` Django |
| `size` | `sm` · `md` · `lg` |

---

### `<c-ui.empty-state>`

```html
<c-ui.empty-state
  icon="📭"
  title="Aucun résultat"
  message="Essayez autre chose.">
  <c-ui.btn href="/" variant="outline" size="sm">Retour</c-ui.btn>
</c-ui.empty-state>
```

| Prop | Description |
|---|---|
| `icon` | Emoji ou caractère affiché en grand |
| `title` | Titre principal |
| `message` | Texte secondaire |
| slot | Bouton ou lien optionnel |

---

### `<c-ui.page-header>`

```html
<c-ui.page-header title="Catalogue" subtitle="Toutes nos formations">
  <c-ui.badge variant="gray">12 formations</c-ui.badge>
</c-ui.page-header>
```

| Prop | Description |
|---|---|
| `title` | Titre H1 |
| `subtitle` | Sous-titre |
| slot | Badge, bouton… |

---

### `<c-ui.progress-bar>`

```html
<c-ui.progress-bar :value="progression" max="100" />
```

| Prop | Description |
|---|---|
| `value` | Valeur actuelle |
| `max` | Valeur max (défaut `100`) |

---

## 4. Mettre à jour dans tous tes projets

```bash
# Dans ~/hajime-ui : modifier un composant, bump la version dans pyproject.toml
git add -A && git commit -m "fix: btn hover state"
git tag v0.1.2 && git push && git push --tags

# Dans chaque projet consommateur
pip install --upgrade "git+ssh://git@github.com/yanis-san/hajime-ui.git@v0.1.2"
```

---

## Stack requise côté projet

| Outil | Rôle |
|---|---|
| [Tailwind CSS](https://tailwindcss.com) | Classes utilitaires |
| [HTMX](https://htmx.org) | Interactions serveur |
| [Alpine.js](https://alpinejs.dev) | État client local |
| [django-cotton](https://django-cotton.com) `>= 0.9` | Moteur de composants |
