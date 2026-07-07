# Miral Abaya — Site Web

## Structure

- `index.html` — la page du site (une seule page).
- `data/products.json` — la liste des articles (nom, prix, description, photos, délai de livraison). Modifiable via `/admin`.
- `data/settings.json` — le numéro WhatsApp utilisé pour les commandes. Modifiable via `/admin`.
- `assets/` — logo et photos des articles.
- `admin/` — panneau d'administration (Decap CMS) pour éditer le contenu sans toucher au code.

## Mettre le site en ligne (Netlify — gratuit)

1. Aller sur [netlify.com](https://www.netlify.com) et créer un compte (avec le compte GitHub qui héberge ce dépôt).
2. "Add new site" → "Import an existing project" → choisir ce dépôt GitHub.
3. Dans la configuration du site :
   - **Base directory**: `site`
   - **Publish directory**: `site` (ou `.` si demandé relatif à la base directory)
   - **Build command**: laisser vide (le site n'a pas besoin de build).
4. Déployer. Netlify donne une URL du type `nom-aleatoire.netlify.app` — vous pourrez brancher votre propre nom de domaine plus tard dans "Domain settings".

## Activer le panneau d'administration (pour que ton client gère les articles)

Le site utilise **Decap CMS** avec l'authentification **Netlify Identity** — ton client n'a besoin d'aucune compétence technique, juste d'un email et d'un mot de passe.

1. Dans le tableau de bord Netlify du site → **Identity** → "Enable Identity".
2. Toujours dans Identity → **Services** → "Git Gateway" → "Enable Git Gateway".
3. Dans Identity → **Settings and usage** → "Registration" → mettre sur **Invite only** (pour que seules les personnes invitées puissent se connecter).
4. Dans Identity → onglet **Identity** (liste des utilisateurs) → "Invite users" → entrer l'email de ton client.
5. Ton client reçoit un email, clique sur le lien, choisit un mot de passe.
6. Il peut ensuite se rendre sur `https://<ton-site>.netlify.app/admin/` pour se connecter et gérer :
   - **Articles (Collection)** → ajouter/modifier/supprimer des abayas, changer les prix, uploader des photos, changer la catégorie (Classique = 1 semaine / VIP = 1 mois).
   - **Réglages du Site** → modifier le numéro WhatsApp si besoin.
7. Chaque modification publiée dans `/admin` crée automatiquement un commit sur GitHub et redéploie le site — aucune intervention technique nécessaire ensuite.

## Une fois le nom de domaine définitif connu

Remplacer `https://miralabaya.com/` dans `index.html` (balises `canonical`, Open Graph, Twitter, JSON-LD) et dans `robots.txt` / `sitemap.xml` par le vrai domaine du site.

## Développement local

Comme le site charge `data/products.json` via `fetch()`, il faut le servir via un petit serveur local (pas juste ouvrir le fichier HTML directement) :

```bash
cd site
python3 -m http.server 8000
# puis ouvrir http://localhost:8000
```
