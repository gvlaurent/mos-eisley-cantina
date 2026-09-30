### Prompt Cursor - Exo 2

Génère une grille de 3 cartes Tailwind pour Mos Eisley Cantina avec Play CDN.

STRUCTURE:
- grid-cols-1 md:grid-cols-3 gap-6
- Chaque <article> contient:
  * Une boîte d'icône: size-12 rounded-xl bg-violet-500/10 ring-1 ring-violet-400/20 flex items-center justify-center text-2xl
  * Un <h3> en gras
  * Un paragraphe de description
  * Style sombre: bg-white/[0.03] border border-white/10 backdrop-blur rounded-xl p-8
  * Hover effect: hover:-translate-y-1 transition
  * Focus rings: focus-visible:ring-2 focus-visible:ring-violet-400

CONTENU EXACT (avec emojis comme icônes):
1. Icône: 🎵 | Titre: "Musique en direct" | Texte: "Musique en direct chaque nuit. Du coucher au lever du soleil, assez fort pour couvrir un chasseur de primes."
2. Icône: 🔫 | Titre: "Contrebandiers bienvenue" | Texte: "Les contrebandiers bienvenue. Pas de questions. Cabines au fond, aucune trace."
3. Icône: 🤖 | Titre: "Droits des droïdes" | Texte: "Droits des droïdes : voir règlement. Limites au sol. Mise en veille recommandée."

### Corrections apportées après génération

1. Centré les emojis: Ajouté `flex items-center justify-center` dans les icônes
2. Corrigé la syntaxe des couleurs: `bg-white/(0.03)` → `bg-white/[0.03]`
3. Ajouté du padding au texte: `text-sm text-slate-300 leading-relaxed` pour lisibilité
4. Amélioré les focus rings: Ajouté `focus-visible:ring-2 focus-visible:ring-offset-2`
5. Vérifiées au DevTools: Tous les liens/cartes réagissent au Tab