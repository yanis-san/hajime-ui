# hajime-ui

Bibliothèque de composants Django Cotton réutilisables — Tailwind CSS + HTMX + Alpine.js.

## Installation

```bash
pip install git+ssh://git@github.com/yanis-san/hajime-ui.git

# version précise
pip install git+ssh://git@github.com/yanis-san/hajime-ui.git@v0.1.0
```

## Configuration

Ajouter dans `INSTALLED_APPS` :

```python
INSTALLED_APPS = [
    ...
    "hajime_ui",
]
```

## Composants disponibles

### `<c-ui.btn>`
```html
<c-ui.btn href="/url/" variant="primary" size="md">Valider</c-ui.btn>
<c-ui.btn type="submit" variant="outline" size="sm">Annuler</c-ui.btn>
```
**Props** : `variant` (primary · outline · ghost · danger), `size` (sm · md · lg), `href`, `type`

---

### `<c-ui.badge>`
```html
<c-ui.badge variant="gray">Brouillon</c-ui.badge>
<c-ui.badge variant="orange">Nouveau</c-ui.badge>
```
**Props** : `variant` (gray · orange · green · red · blue)

---

### `<c-ui.alert>`
```html
<c-ui.alert type="success">Enregistré avec succès.</c-ui.alert>
<c-ui.alert type="error">Une erreur est survenue.</c-ui.alert>
```
**Props** : `type` (success · error · warning · info)

---

### `<c-ui.avatar>`
```html
<c-ui.avatar :user="request.user" size="md" />
```
**Props** : `user`, `size` (sm · md · lg)

---

### `<c-ui.empty-state>`
```html
<c-ui.empty-state
  icon="🔍"
  title="Aucun résultat"
  message="Essayez d'autres termes de recherche.">
  <c-ui.btn href="/" variant="outline" size="sm">Retour</c-ui.btn>
</c-ui.empty-state>
```
**Props** : `icon`, `title`, `message`, slot enfant optionnel

---

### `<c-ui.page-header>`
```html
<c-ui.page-header title="Catalogue" subtitle="Toutes nos formations">
  <c-ui.badge variant="gray">12 formations</c-ui.badge>
</c-ui.page-header>
```
**Props** : `title`, `subtitle`, slot enfant optionnel (badge, bouton…)

---

### `<c-ui.progress-bar>`
```html
<c-ui.progress-bar :value="progression" max="100" />
```
**Props** : `value`, `max` (défaut 100), `color`

---

## Mettre à jour un composant

```bash
# Dans hajime-ui : modifier le composant, bump version dans pyproject.toml
git add -A && git commit -m "fix: btn hover state"
git tag v0.1.1 && git push && git push --tags

# Dans chaque projet consommateur
pip install --upgrade git+ssh://git@github.com/yanis-san/hajime-ui.git@v0.1.1
```

## Stack requise côté projet

- **Tailwind CSS** — classes utilitaires
- **HTMX** — interactions serveur
- **Alpine.js** — état client local
- **django-cotton >= 0.9** — moteur de composants
