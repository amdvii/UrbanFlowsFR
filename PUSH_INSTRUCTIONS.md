# Push vers GitHub — instructions

> ⚠️ Avant de commencer : révoque le PAT que tu as partagé dans le chat sur
> https://github.com/settings/tokens (sécurité). Tu en recréeras un neuf
> si besoin pour ce push.

## Étape 1 — Ouvre un terminal dans le dossier du projet

Sur Windows (PowerShell) :
```powershell
cd "C:\chemin\vers\UrbanFlows-FR"
```

Sur Mac/Linux :
```bash
cd "/chemin/vers/UrbanFlows-FR"
```

> Astuce VS Code : clic droit sur le dossier `UrbanFlows-FR` dans
> l'explorateur → "Ouvrir dans le terminal intégré".

## Étape 2 — Nettoie le `.git` cassé puis initialise

Il y a un dossier `.git/` cassé dans le projet (résidu d'une init qui a
échoué côté sandbox Cowork à cause des permissions du dossier monté).
Supprime-le d'abord :

Sur Windows (PowerShell) :
```powershell
Remove-Item -Recurse -Force .git
```

Sur Mac/Linux :
```bash
rm -rf .git
```

Puis initialise proprement :

```bash
git init -b main
git config user.email "a.eish@outlook.fr"
git config user.name "Ahmed EISH"
git add .
git commit -m "Initial commit — UrbanFlows-FR : pipeline ETL + EDA + lois Zipf/Gibrat"
```

## Étape 3 — Pousse sur GitHub

⚠️ Le repo `amdvii/UrbanFlowsFR` contient déjà un README minimal (créé
quand tu as fait "Initialize this repository with a README" sur GitHub).
On va l'écraser avec le contenu local (qui est bien plus complet) via un
**force-push**.

```bash
git remote add origin https://github.com/amdvii/UrbanFlowsFR.git
git push -u origin main --force
```

Quand git te demande tes identifiants :
- **Username** : `amdvii`
- **Password** : ton **nouveau** PAT (PAS ton mot de passe GitHub)

> Le `--force` est sans risque ici : le seul truc qui va être écrasé
> côté GitHub est le README minimal d'init. Aucun travail réel ne se
> perd.

> Si tu as installé GitHub CLI (`gh`), tu peux à la place faire
> `gh auth login` une fois pour toutes, puis `git push -u origin main`
> sans avoir à coller de token.

## Étape 4 — Vérifie

Va sur https://github.com/amdvii/UrbanFlowsFR — tu dois voir le README
qui s'affiche avec les figures, l'arborescence des notebooks, etc.

## Étape 5 — Sécurité

Re-révoque le PAT que tu viens d'utiliser (https://github.com/settings/tokens).
Pour pousser des futurs commits, utilise `gh auth login` une bonne fois
pour toutes — c'est plus propre que de manipuler des PATs.
