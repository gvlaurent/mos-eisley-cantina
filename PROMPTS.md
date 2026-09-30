# Prompts used

Journal des prompts utilisés avec Cursor (Cmd+K / Ctrl+K) et des
interventions manuelles, un bloc par commit.

---

## feature/sticky-nav

### `4a52eb6` — add: sticky behavior on top nav

Prompt Cursor, sur le bloc `<nav>` sélectionné :

> Contexte : landing page statique, HTML + Tailwind via CDN.
> Tâche : rends ce `<nav>` collé en haut du viewport pendant le scroll.
> Contraintes : utilitaires Tailwind uniquement. Pas de `<script>`, pas de JS,
> pas de CSS custom, pas de nouvelle classe inventée. Ne touche à aucune autre
> partie du fichier.
> Sortie : renvoie uniquement le bloc `<nav>` modifié.

Résultat : ajout de `sticky top-0` sur la balise `<nav>`.

Ce que le modèle a manqué : le `z-50`. Sans contexte d'empilement, la nav
passe sous les sections au défilement. Corrigé au commit suivant.

---

### `ad554be` — fix: merge html classes; remove duplicate sticky on nav, wire nav anchors

Correction manuelle après relecture du fichier, pas de prompt Cursor.

Trois problèmes traités :

1. Deux attributs `class` sur `<html>` (`class="dark"` puis
   `class="scroll-smooth"`). HTML ne retient que le premier : `scroll-smooth`
   n'existait pas pour le navigateur. Fusionnés en `class="dark scroll-smooth"`.
2. `sticky top-0 z-50` présent à la fois sur le `<header>` et sur le `<nav>`
   imbriqué, avec les mêmes classes de fond : deux barres translucides
   superposées et deux bordures.
3. Liens de nav pointant vers `#music` et `#signin`, sans section
   correspondante dans la page.

---

### `73dc870` — fix: rebuild index.html after duplicated document paste

Reconstruction manuelle du fichier.

Le fichier contenait un document HTML complet collé à l'intérieur du `<body>`
d'un autre, plus un fragment de `<nav>` et de `<main>` orphelin après le
`</html>` de fermeture. Accident de copier-coller lors d'une passe précédente,
committé sans relecture du diff.

Corrections apportées :

- un seul `<!DOCTYPE html>`, un seul `<html>`, un seul `<body>`
- comportement sticky conservé uniquement sur le `<header>` ; la `<nav>` ne
  porte plus que son `aria-label`
- liens de nav alignés sur les `id` réellement présents ; la section tarifs
  devient `id="menu"` pour servir de cible au lien « Menu »
- `scroll-mt-24` sur les sections cibles, pour que la nav collante ne masque
  pas le titre à l'arrivée
- bouton « Voir le menu » du hero converti de `<button>` en `<a>` : un élément
  qui navigue est un lien, pas un bouton
- dégradé sombre du `<main>` activé (la version claire rendait le texte
  `slate-300` illisible)
- classes de centrage contradictoires nettoyées sur les icônes (`grid` et
  `flex` cumulés sur le même élément)

---

## Enseignements de la session

- Relire `git diff` avant chaque commit. Le document dupliqué aurait été vu
  immédiatement : le commit `ad554be` annonçait trois correctifs mineurs et
  pesait 235 insertions.
- Un commit dont le volume ne correspond pas à son message est un signal.
- Vérifier que les `id` cibles existent avant de conclure qu'un scroll
  fluide est cassé.
- Sauvegarder le fichier avant de lancer `git status` : Git ne lit que le
  disque, pas la mémoire de l'éditeur.