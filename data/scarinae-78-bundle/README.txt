EEB 187 FishView mini-bundle (Demo 8)
Family: scarinae
Species exported: 76 (85 regular + 1 error)
Total Included images: 155
Species missing tip in tree: 0
Tree format: newick
Error-species: Chlorurus_japanensis (5 images)

Files (HYBRID layout — flat exemplars + per-species replicate folders):
-----
  scarinae-mini-tree.tre                  — full family phylogeny (NEXUS or Newick).
  images/<Genus_species>.png              — regular species' ★ exemplar (flat, simple path).
  images/<Genus_species>/exemplar.png     — same exemplar, folder entry.
  images/<Genus_species>/img-N.png        — any additional Included images for that species.
  images/<error-sp>/img-1..5.png          — error species' 5-image noise stack (no flat file).
  species_metadata.csv          — species,role,gestalt_k,n_included,exemplar_filename,extra_picks
  picked_species.txt            — flat list of exported species (Genus_species).
  picked_tip_labels.txt         — parallel tip labels ('' if no match).
  missing_tips.txt              — species WITHOUT a matching tip (warning).

Recipes that want ONE image per species: glob images/*.png (flat — error species excluded).
Recipes that bootstrap over N replicates: iterate the per-species folder.

Consume from R:
  bundle <- "scarinae-mini-bundle"
  tree   <- ape::read.tree(file.path(bundle, "scarinae-mini-tree.tre"))
  tips   <- readLines(file.path(bundle, "picked_tip_labels.txt"))
  sub    <- ape::keep.tip(tree, tips[nzchar(tips)])
  meta   <- read.csv(file.path(bundle, "species_metadata.csv"))
