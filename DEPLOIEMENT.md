# Déploiement portfolio — 2 variantes prêtes (bascule < 15 min)

> Préparé le 10/11 par builder. **Aucune publication effectuée** — exécution = main ou Nadim.
> ⚠️ État actuel : `deploy/` EST le repo GitHub Pages `nadimsahiri9-cmyk/nadimsahiri9-cmyk.github.io` (remote configuré).
> Les modifs portfolio v2 (5 packs + offres packagées) sont dans `index.html` **non commitées** — c'est le push qui publie.

---

## Variante A — GitHub Pages (gratuit, ~5 min)

**Cible** : https://nadimsahiri9-cmyk.github.io/

1. Éditer `index.html` : décommenter le bloc **VARIANTE A** dans le `<head>` (canonical + og:url).
2. Depuis `sysops/portfolio/deploy/` :
   ```bash
   git add index.html && git commit -m "portfolio v2 — boutique 5 packs + offres packagées" && git push origin main
   ```
3. **Settings → Pages** du repo : Source = "Deploy from a branch", branche `main`, `/ (root)` — normalement déjà configuré (le site est déjà en ligne).
4. Vérifier : https://nadimsahiri9-cmyk.github.io/ → 200, section « Offres packagées » visible, 5 packs en boutique.
5. ⚠️ Ne PAS ajouter de fichier `CNAME` à la racine (il basculerait le site sur un domaine custom).

---

## Variante B — domaine pro (~15 min, DNS compris)

**Cible** : ex. `https://nadim.dev/` (à adapter au domaine réellement acheté).

1. **Acheter le domaine** (Nadim, registrar au choix — OVH/Cloudflare/Gandi). Vérifier la dispo AVANT de communiquer l'URL.
2. **DNS chez le registrar** (propagation : minutes à ~1 h) :
   - Apex `nadim.dev` → 4 A records : `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `www` → CNAME `nadimsahiri9-cmyk.github.io`
3. Dans `deploy/` : copier `CNAME.example` → `CNAME` (contenu = domaine choisi, une seule ligne, sans https://), décommenter le bloc **VARIANTE B** de `index.html`, puis :
   ```bash
   cp CNAME.example CNAME   # éditer si domaine ≠ nadim.dev
   git add CNAME index.html && git commit -m "domaine custom + portfolio v2" && git push origin main
   ```
4. **Settings → Pages** : Custom domain = `nadim.dev` → attendre le check DNS → cocher **Enforce HTTPS** (après la 1re émission de certificat, ~quelques minutes).
5. Vérifier : https://nadim.dev/ → 200 + HTTPS + section Offres visible. www redirige automatiquement vers l'apex.

---

## Après bascule (2 min)

- `og:image` à ajouter quand les visuels de cover seront prêts.
- Lien portfolio à mettre à jour dans les profils Malt/Codeur + bio GitHub.
- Si migration A → B plus tard : ajouter le CNAME + DNS, rien d'autre (l'URL .github.io redirige vers le domaine custom).
