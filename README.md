# hajime-ui

Bibliothèque de composants Django Cotton réutilisables, stylés avec Tailwind CSS et compatibles HTMX + Alpine.js.

## 1. Installation

```bash
pip install git+ssh://git@github.com/yanis-san/hajime-ui.git@v0.2.0
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

## 3. Composants disponibles

---

### `<c-ui.btn>`

```html
<c-ui.btn href="{% url 'login' %}" variant="primary">Se connecter</c-ui.btn>
<c-ui.btn type="submit" variant="outline" size="sm">Annuler</c-ui.btn>
```

| Prop | Valeurs |
|---|---|
| `variant` | `primary` · `secondary` · `outline` · `ghost` · `danger` |
| `size` | `sm` · `md` · `lg` |
| `href` | URL (génère un `<a>`) |
| `type` | `button` · `submit` |
| `disabled` | `true` · `false` |

---

### `<c-ui.badge>`

```html
<c-ui.badge variant="orange">Nouveau</c-ui.badge>
```

| Prop | Valeurs |
|---|---|
| `variant` | `gray` · `orange` · `green` · `red` · `blue` · `yellow` |

---

### `<c-ui.alert>`

```html
<c-ui.alert variant="success" dismissible="true">Profil mis à jour.</c-ui.alert>
```

| Prop | Valeurs |
|---|---|
| `variant` | `success` · `error` · `warning` · `info` |
| `title` | Titre optionnel |
| `dismissible` | `true` · `false` (Alpine.js) |

---

### `<c-ui.avatar>`

```html
<c-ui.avatar :user="request.user" size="md" />
```

| Prop | Valeurs |
|---|---|
| `user` | Objet User Django |
| `size` | `sm` · `md` · `lg` |

---

### `<c-ui.empty_state>`

```html
<c-ui.empty_state icon="📭" title="Aucun résultat" message="Essayez autre chose.">
  <c-ui.btn href="/" variant="outline" size="sm">Retour</c-ui.btn>
</c-ui.empty_state>
```

| Prop | Description |
|---|---|
| `icon` | Emoji ou caractère affiché en grand |
| `title` | Titre principal |
| `message` | Texte secondaire |
| slot | Bouton ou lien optionnel |

---

### `<c-ui.page_header>`

```html
<c-ui.page_header title="Catalogue" subtitle="Toutes nos formations">
  <c-ui.badge variant="gray">12 formations</c-ui.badge>
</c-ui.page_header>
```

| Prop | Description |
|---|---|
| `title` | Titre H1 |
| `subtitle` | Sous-titre |
| slot | Badge, bouton… |

---

### `<c-ui.progress_bar>`

```html
<c-ui.progress_bar :value="progression" max="100" />
```

| Prop | Description |
|---|---|
| `value` | Valeur actuelle |
| `max` | Valeur max (défaut 100) |

---

### `<c-ui.navbar>` ✨ NEW

Navigation responsive avec backdrop blur et menu mobile Alpine.js.

```html
<c-ui.navbar brand="MonSite" brand_href="/">
  <a href="/" class="nav-link">Accueil</a>
  <a href="/about" class="nav-link">À propos</a>

  <c-slot name="actions">
    <c-ui.btn href="/contact" variant="primary" size="sm">Contact</c-ui.btn>
  </c-slot>
</c-ui.navbar>
```

| Prop | Description |
|---|---|
| `brand` | Texte ou HTML du logo/marque |
| `brand_href` | URL du lien brand (défaut `/`) |
| slot | Liens de navigation |
| `actions` slot | Boutons côté droit |

---

### `<c-ui.hero>` ✨ NEW

Section héros plein écran.

```html
<c-ui.hero title="Bienvenue" subtitle="Description du site" align="center" bg_class="bg-cream">
  <c-ui.btn href="/start" variant="primary" size="lg">Commencer</c-ui.btn>

  <c-slot name="media">
    <img src="/img/hero.jpg" alt="Hero" class="rounded-2xl" />
  </c-slot>
</c-ui.hero>
```

| Prop | Valeurs |
|---|---|
| `title` | Titre (accepte HTML via `\|safe`) |
| `subtitle` | Sous-titre |
| `align` | `center` · `left` |
| `bg_class` | Classes Tailwind pour le fond |
| slot | Boutons CTA |
| `media` slot | Image ou vidéo |

---

### `<c-ui.section>` ✨ NEW

Container avec fade-in au scroll (Alpine `x-intersect`).

```html
<c-ui.section title="Nos services" subtitle="Ce que nous proposons" id="services">
  <!-- contenu -->
</c-ui.section>
```

| Prop | Description |
|---|---|
| `title` | Titre de section |
| `subtitle` | Sous-titre |
| `id` | ID HTML |
| `bg_class` | Classes de fond |

---

### `<c-ui.feature_card>` ✨ NEW

Carte feature avec icône et hover effect.

```html
<c-ui.feature_card icon="🎌" title="Formation au Japon" description="2 mois de formation intensive." />
```

| Prop | Description |
|---|---|
| `icon` | Emoji ou HTML |
| `title` | Titre |
| `description` | Description |

---

### `<c-ui.pricing_card>` ✨ NEW

Carte de tarification.

```html
<c-ui.pricing_card title="Individuel" price="35€" period="heure" featured="true">
  <c-slot name="features">
    <li>✓ Cours personnalisé</li>
    <li>✓ Support WhatsApp</li>
  </c-slot>
  <c-slot name="cta">
    <c-ui.btn href="/contact" variant="primary" class="w-full">Réserver</c-ui.btn>
  </c-slot>
</c-ui.pricing_card>
```

| Prop | Description |
|---|---|
| `title` | Nom de la formule |
| `price` | Prix affiché |
| `period` | Période (heure, mois…) |
| `description` | Description courte |
| `featured` | `true` pour mise en avant (fond sombre + badge) |
| `features` slot | Liste de features |
| `cta` slot | Bouton d'action |

---

### `<c-ui.testimonial>` ✨ NEW

Carte de témoignage.

```html
<c-ui.testimonial
  quote="Les cours sont géniaux !"
  author="Marie D."
  role="Étudiante"
  avatar_url="/img/avatars/marie.jpg" />
```

| Prop | Description |
|---|---|
| `quote` | Texte du témoignage |
| `author` | Nom de l'auteur |
| `role` | Rôle / titre |
| `avatar_url` | URL de l'avatar (optionnel) |

---

### `<c-ui.contact_form>` ✨ NEW

Wrapper stylé pour formulaire (HTMX ready).

```html
<c-ui.contact_form action="{% url 'contact' %}" title="Nous contacter"
                   form_attrs='hx-post="{% url "contact" %}" hx-swap="outerHTML"'>
  {{ form.as_div }}
  <c-ui.btn type="submit" variant="primary">Envoyer</c-ui.btn>
</c-ui.contact_form>
```

| Prop | Description |
|---|---|
| `action` | URL du formulaire |
| `method` | Méthode HTTP (défaut `post`) |
| `title` | Titre |
| `subtitle` | Sous-titre |
| `form_attrs` | Attributs du `<form>` (ex: `hx-post`) |

---

### `<c-ui.footer>` ✨ NEW

Pied de page multi-colonnes.

```html
<c-ui.footer brand="MonSite" copyright="© 2026 MonSite. Tous droits réservés.">
  <c-slot name="columns">
    <div>
      <h4 class="font-semibold text-sm text-gray-900 mb-3">Navigation</h4>
      <a href="/" class="block text-sm text-gray-500 hover:text-gray-900">Accueil</a>
    </div>
  </c-slot>
  <c-slot name="social">
    <a href="#">Twitter</a>
    <a href="#">Instagram</a>
  </c-slot>
</c-ui.footer>
```

| Prop | Description |
|---|---|
| `brand` | Texte ou HTML du brand |
| `copyright` | Texte de copyright |
| `columns` slot | Colonnes de liens |
| `social` slot | Icônes réseaux sociaux |
| `bottom` slot | Ligne du bas |

---

## 4. Mettre à jour dans tous tes projets

```bash
# Dans ~/hajime-ui : modifier un composant, bump la version dans pyproject.toml
git add -A && git commit -m "feat: nouveaux composants"
git tag v0.2.0 && git push && git push --tags

# Dans chaque projet consommateur
pip install --upgrade "git+ssh://git@github.com/yanis-san/hajime-ui.git@v0.2.0"
```

## Stack requise côté projet

| Outil | Rôle |
|---|---|
| Tailwind CSS | Classes utilitaires |
| HTMX | Interactions serveur |
| Alpine.js | État client local |
| django-cotton >= 0.9 | Moteur de composants |
