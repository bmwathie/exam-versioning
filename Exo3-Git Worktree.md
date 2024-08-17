# Git Worktrees

Les **Git worktrees** sont une fonctionnalité puissante qui permet de travailler sur plusieurs branches d'un même dépôt simultanément, sans avoir à cloner le dépôt plusieurs fois. Voici une explication détaillée avec des exemples et des cas d'utilisation :

## Qu'est-ce qu'un Git Worktree ?

Un **worktree** est une copie de travail d'un dépôt Git qui permet de vérifier différentes branches dans des répertoires distincts. Cela facilite le développement parallèle, les tests ou la correction de bugs sans interférer avec votre branche principale de travail.

## Exemple de base

### Création d'un Worktree

Supposons que vous travaillez sur la branche `main` et que vous devez corriger un bug sur la branche `bugfix`. Vous pouvez créer un worktree pour la branche `bugfix` :

```bash
# Crée un nouveau worktree pour la branche bugfix dans le répertoire bugfix
git worktree add ../bugfix bugfix
```

## Utilisation du Worktree

Vous pouvez maintenant naviguer vers le répertoire bugfix et travailler sur cette branche sans affecter votre branche main :

```bash
cd ../bugfix
# Faites vos modifications et commitez-les
git commit -am "Correction du bug"
```

## Cas d’utilisation

### 1. Développement parallèle

   Imaginez que vous travaillez sur une nouvelle fonctionnalité dans une branche `feature-x` et que vous devez soudainement corriger un bug critique sur la branche `main`. Avec les worktrees, vous pouvez facilement basculer entre les branches sans perdre votre contexte de travail.

   ```bash
   # Crée un worktree pour la branche feature-x
   git worktree add ../feature-x feature-x

   # Crée un worktree pour la branche main pour corriger le bug
   git worktree add ../main main
   ```
### 2. Tests et intégration continue

   Les worktrees peuvent être utilisés pour tester différentes versions de votre code en parallèle. Par exemple, vous pouvez avoir un worktree pour la branche `develop` et un autre pour la branche `release` afin de tester les intégrations avant de les fusionner.

   ```bash
   # Crée un worktree pour la branche develop
   git worktree add ../develop develop

   # Crée un worktree pour la branche release
   git worktree add ../release release
   ```

### 3. Bisecting avec Worktrees

   Lors de la recherche de bugs, vous pouvez utiliser `git bisect` avec des worktrees pour tester différentes versions de votre code sans affecter votre environnement de travail principal.

   ```bash
   # Commence le bisecting
   git bisect start
   git bisect bad HEAD
   git bisect good <commit>

   # Crée un worktree pour tester une version spécifique
   git worktree add ../bisect <commit>
   ```

## Gestion des Worktrees

### Lister les Worktrees

Pour voir tous les worktrees associés à votre dépôt, utilisez :

```bash
git worktree list
```
### Supprimer un Worktree

Pour supprimer un worktree, utilisez :

```bash
git worktree remove ../feature-x
```

