Réflexion marwane

 1
  Structure actuelle du projet Git après toutes les opérations

Après toutes les manipulations (merges, rebase et reset), le projet contient :
- Une branche `main` qui représente la version stable du TP.
- Trois branches de travail (`marwane`, `Reda`, `eleve3`) qui ont divergé puis été synchronisées.
- Un merge no ff du travail de reda dans la branche de marwane → cela a créé un vrai commit de merge visible dans `git log --graph`.
- Un merge ff effectué par reda intégré directement dans l’historique sans commit de merge.
- Un double rebase de l’élève 3 sur les branches des élèves 1 et 2 → cela a réécrit l’historique pour empiler correctement les commits.
- Un commit en mode HEAD détaché (marwane) et un reset hard (élève 3), visibles également dans l’historique.


2
  git fetch récupère simplement les nouveautés du dépôt distant, mais ne touche pas à la branche sur laquelle on travaille.  
Ça permet de voir ce qui a changé sur le serveur sans modifier son travail en local

git pull fait directement la mise à jour : il télécharge les changements puis les fusionne avec la branche actuelle.  
C’est pratique quand on est sûr de vouloir être à jour tout de suite.

  
Si je travaille sur un fichier et que je ne veux surtout pas que Git modifie ma branche pendant que je suis en train d’écrire, j’utilise fetch 
Quand j’ai fini et que je veux mettre ma branche à jour, j’utilise pull

Différence entre git reset et git revert

git reset sert à revenir en arrière dans l’historique en supprimant des commits.  
C’est un outil puissant, mais il peut casser le travail si la branche est partagée, car il réécrit l’historique.

git revert fait l’inverse : il garde l’historique intact et crée un commit qui annule proprement un commit précédent.  
On voit donc toujours ce qu’il s’est passé, même si l’action est annulée.

reset dangereux 
Sur une branche utilisée par plusieurs personnes (ex : main), un reset --har` peut supprimer des commits que d’autres ont déjà récupérés.  
Ça crée des conflits et force les autres à réparer leur historique.  
Dans ce cas, il vaut mieux utiliser revert, qui n’efface rien.