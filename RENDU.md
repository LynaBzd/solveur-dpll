                      Mini-projet 1 : solveur DPLL récursif
                             fichier RENDU
                       (à remplir obligatoirement)

**Un mini-projet sans fichier RENDU rempli ne recevra pas de note.**

Date limite: 28 octobre 2022, 23h59

Identité
--------
Nombre de binôme: 48
Nom, prénom 1: BOUZID, Lyna
Nom, prénom 2: AKBAS, Aleysa


Questions sur votre code
------------------------
0. Avez-vous testé que `make dpll` s'exécute sans erreurs ou warnings,
   et que ensuite `./dpll sudoku-4x4.cnf` donne la réponse attendue (voir
   fichier README) ?

**Réponse 0**
[Test Compilation](captureCompilation.png)

`make dpll` s'exécute sans warnings ni erreurs.

`./dpll sudoku-4x4.cnf` donne la réponse attendue mentionnée dans le README (`solveur_split`donne la même réponse)
---

1. Avez-vous utilisé la fonction `filter_map` (donné dans dpll.ml)
   dans votre implémentation de `simplifie` ? 
   - Si oui, expliquez en quelques phrases en français comment vous
     l'avez utilisée.
   - Si non, expliquez en quelques phrases en français comment
     fonctionne votre implémentation de `simplifie`.

   **Réponse 1:** Oui, nous avons effectivement utilisé la fonction 'filter_map'. Une fonction auxiliaire `supprime_litteral` s'occupe de simplifier l'ensemble des clauses en mettant
   le littéral 'l' à vrai. Ainsi, quand on applique  `filter_map (fun c -> supprime_litteral l c) clauses)`, clauses respecte la condition de `supprime_litteral`, ce qui nous renvoie tous les éléments de clauses qui staisfont c. 

---

2. Pour l'implémentation de `unitaire`, quelles sont les fonctions
   auxiliaires que vous avez utilisées et/ou écrites ? (Par une
   fonction auxiliaire, on entend ici soit une fonction d'une
   bibliothèque, par exemple des fonctions comme `List.length`,
   `List.rev_append`, ou une fonction `aux_unitaire` que vous avez
   écrite vous-mêmes.) Expliquez en quelques phrases en français
   comment ces fonctions auxiliaires sont utilisées dans votre
   implémentation de la fonction `unitaire`.

   **Réponse 2:** Nous avons utilisé la fonction auxiliaire `List.length`, pour trouver la clause unitaire. On saît qu'une clause unitaire est de taille 1, on fait alors un parcours de nos clauses en vérifiant pour chacune si elle était de longueur 1. Lorsque c'est le cas, on peut renvoyer le littéral à l'aide de `List.head` (la tête de la liste est bien le seul littéral de la clause).

---

3. Pour l'implémentation de `pur`, quelles sont les fonctions
   auxiliaires que vous avez utilisées et/ou écrites ?  Expliquez en
   quelques phrases en français comment ces fonctions auxiliaires sont
   utilisées dans votre implémentation de la fonction `pur`.

   **Réponse 3:** Nous avons utilisé une fonction auxiliaire 'purAux' qui, dans un premier temps, parcourt une clause. Si la clause est vide, elle lève une exception, sinon elle parcourt chaque élément de la clause, et si la clause est vide, on renvoie un failwith "pas de littéral pur", sinon si `clauses' contient au moins un littéral pur, retourne ce littéral. La fonction 'pur', fait donc appel à la fonction 'purAux' avec les arguments attendus.

   On utilise une seule fonction auxiliaire afin d'y passer deux parmètres (type `int list`). Il s'agit de la même clause. Le premier paramètre sert à effectuer les parcours de liste récursif, et le deuxième paramètre permet de garder en mémoire la liste source. Tant qu'il y a des éléments dans la liste on la parcourt. Chaque parcourt vérifie si un élément de la liste est un opposé de la tête. Tant qu'il en trouve la fonction continue, et s'il arrive & la fon de la liste cela lève l'exception. Si dans un parcours il ne trouve pas l'élément opposé, il peut renvoyer la tête (c'est un littéral pur !).

---

4. Donnez un exemple d'une formule pour laquelle les deux fonctions
   `solveur_split` et `solveur_dpll_rec` ont un comportement
   différent, et expliquez les différences entre ces deux fonctions.

   **Réponse 4** La fonction 'solveur_split' ne traite pas les cas où on a une clause unitaire ou pur, alors que la fonction 'solveur_dpll_rec' traite tous les cas. 
   Si on a par exemple la clause [[1;2;3];[-1;2];[3]], la fonction `solveur_split`, ne traitera pas le cas où la clause [3] est unitaire, et fera donc un split, en séparant le cas de 1 et -1. solveur_dpll_rec commencera quant à lui par traiter le cas où [3] est unitaire, pour par la suite traiter le cas où le littéral -1 est pur, sans passer par un split inutile. 

---

5. Avez-vous d'autres remarques sur votre rendu ? (question optionnelle)

**à remplir**

---

--fin du fichier RENDU--