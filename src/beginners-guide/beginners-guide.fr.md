# Guide du débutant

{{Chemin|Tutoriels|Notions et stratégies}}

''Avant de lire cette introduction au jeu, pensez-bien à ceci : Ce site est un wiki est contient de nombreuses pages qui expliquent différentes notions. Lorsqu'un mot apparaît en bleu, c'est qu'il s'agit d'un lien cliquable. Ces liens vous amèneront sur d'autres pages, sur lesquels vous pourrez trouver des informations précieuses. Alors n'hésitez pas à en profiter pour découvrir les différents notions du jeu. Par exemple, cette page n'expliquera le fonctionnement des armes du jeu de fond en comble, mais vous trouverez certainement un lien sur le mot "Arme" qui vous permettra d'en apprendre plus ! Bonne lecture !''


Bienvenue sur [[Leek Wars]] !

Avant de coder, d'établir des stratégies ou de raconter des idioties sur le chat, il va falloir en apprendre un peu plus sur  [[Leek Wars]].

Dans cet étrange jeu, vous serez un '''Eleveur''', un homme ou une femme entièrement dévoué à la tâche de faire progresser ses petits protégés.
Mais vous ne serez pas n'importe quel éleveur, vous aurez à vous occuper de '''Poireaux''' ! Vous l'aviez déjà compris ? Ah.

Vos poireaux ne sont pas de simples légumes. Ils peuvent se déplacer (Personne ne sait comment), et surtout, ils peuvent combattre.
Via un arsenal d'[[Armes]] et des [[Puces]] permettant de lancer des sorts, ces poireaux sont de véritables machines de guerre.
Ils peuvent même faire appel à des [[Bulbes]] qui les aideront dans leurs combats.
Ils possèdent aussi des [[Caractéristiques]], qui les rendent plus ou moins efficaces dans certains domaines.
En revanche, ils ont su garde une âme sensible et sont victime de la mode, ils leur arrivent de changer de couleur et d'enfiler des chapeaux.

Vous commencerez calmement en vous occupant d'un unique poireau maigrichon. Mais il grandira vite, et avec l'expérience, vous pourrez élever jusqu'à 4 poireaux (Les éleveurs de [[Leek Wars]] privilégient la qualité à la quantité depuis 1853).

Mais il ne suffit pas de lancer vos poireaux au combat, il faut d'abord leur apprendre à combattre !
[[Leek Wars]] est avant tout un jeu de programmation, vous devrez donc créer une '''intelligence artificielle''', une '''IA'''.
Ainsi, l'IA est une sorte de script que votre poireau exécutera à chaque tour de jeu et qui lui indiquera quoi faire.

Vous êtes prêts ? Alors commençons par ... le commencement.


= Répartir son capital =

Vos poireaux gagnent des [[Points de Capital]] lorsqu'il gagne un niveau. Heureusement, il commence avec 50 points ! La première chose à faire est donc de répartir ces points, mais pas n'importe comment !

Rendez-vous sur la page de votre [[Poireau]], il s'agit du premier onglet de la barre de navigation, celui qui porte le nom de votre [[Poireau]].
Vous y trouverez diverses informations, mais celles qui nous intéressent sont celles-ci :

[[Image:niveau1points.png]]

Votre poireau étant niveau 1, je vous conseille fortement de distribuer ces points dans la [[Vie]] [[Fichier:statsLife.png|16px|link=Caractéristiques#La Vie]] et la [[Force]] [[Fichier:statsStrength.png|16px|link=Caractéristiques#La Force]]. Les autres caractéristiques nécessitent des [[Puces]] que vous n'avez pas encore débloqué pour pouvoir être utiles. La [[Vie]] augmente simplement les points de vie de votre poireau, utile pour ne pas mourir trop vite. Et la [[Force]] permet d'infliger plus de dégâts avec vos [[Armes]] et vos [[Puces]] offensives.

Il y a deux caractéristiques auxquelles vous devez aussi vous intéresser.
Les [[PT]] [[Fichier:statsTP.png|16px|link=Caractéristiques#Les PT]] sont les points d'actions de votre [[Poireau]], cela détermine la quantité d'actions qu'il peut faire par tour. Par exemple, équiper une arme consomme 1 [[PT]], tirer avec le [[Pistolet]] en consomme 3.
Les [[PM]] [[Fichier:statsMP.png|16px|link=Caractéristiques#Les PM]] déterminent de combien de cellules votre [[Poireau]] pourra se déplacer en un tour.

Si vous voulez en savoir plus sur les différentes caractéristiques, c'est ici : [[Caractéristiques]].


Sur la page de votre [[Poireau]], vous pouvez aussi voir qu'il est équipé d'un [[Pistolet]]. Il vous faudra gagner quelques niveaux avant de pouvoir débloquer d'autres [[Armes]] et des [[Puces]].

Maintenez que votre [[Poireau]] est prêt, occupons-nous de son '''IA''' !

= L'IA =

Rendez-vous maintenant dans l'onglet "[[Editeur]]".
Vous y trouverez une première IA, nommée "Sans Titre". Elle contient un code minimal qui permettra à votre poireau d'avancer vers son adversaire et de l'attaquer.

<syntaxhighlight>
//--------------------------------
//------- Code de base -----------
//--------------------------------

// On prend le pistolet
setWeapon(WEAPON_PISTOL); // Attention : coûte 1 PT

// On récupère l'ennemi le plus proche
var enemy = getNearestEnemy();

// On avance vers l'ennemi
moveToward(enemy);

// On essaye de lui tirer dessus !
useWeapon(enemy);
</syntaxhighlight>

Les lignes qui comment par "//" permettent de commenter votre code. Il s'agit simplement de phrases qui permettent de clarifier le code, et non d'instructions que suivra votre [[Poireau]].

La première instruction est très importante. Contrairement aux [[Puces]], les armes doivent être prises en main pour être utilisées. Vous pouvez avoir 2 à 4 armes sur un poireau selon son niveau, mais il ne peut en utiliser qu'une seule à la fois. Il porte plusieurs armes mais ne peut se servir que de celle qu'il a dans les mains. Ainsi, il faut utiliser la fonction [[setWeapon]] pour changer l'arme que votre poireau a dans les mains.
'''Attention''', changer l'arme courante consomme 1 [[PT]], et ce, même si vous le faites alors que vous avez déjà cette arme dans les mains. Il est donc judicieux de ne faire ce [[setWeapon]] que lorsque c'est nécessaire. Pour cela, il suffit d'une condition utilisant la fonction [[getWeapon]] qui renvoie l'arme actuellement utilisée.

Ensuite, il vous faut une cible. C'est là que [[getNearestEnemy]] intervient. cette fonction renvoie l'ennemi le plus proche. Des variantes existent pour trouver les alliés ou pour avoir le plus "loigné plutôt que le plus proche.

Viens le tour de [[moveToward]] qui permet d'avancer vers un poireau d'autant de [[PM]] que possible.

Enfin, la fonction [[useWeapon]] permet d'utiliser l'arme actuellement dans les mains de votre poireau sur une cible. Si les conditions d'utilisation de l'arme sont remplies (portée, vue,...), cette fonction consomme autant de [[PT]] qu'il en faut pour utiliser l'arme; sinon, la fonction n'utilise aucun PT (et votre poireau ne tirera pas).

Voilà le détail de ce code. Gardez à l'esprit qu'il ne s'agit pas du code du combat entier. C'est le code qui est exécuté à '''chaque tour''' ! A chaque fois que ce sera à son tour de jouer, votre poireau équipera son arme, avancera vers son adversaire, et attaquera.


== Attaquer efficacement ==

Mais vous n'irez pas bien loin avec ce code ! Car celui-ci n'est qu'un modèle, et est loin d'être très performant.

A la première instruction, vous équipez l'arme [[WEAPON_PISTOL]]. Regardez bien sa fiche (Disponible au [[Marché]]) :

[[Image:armepistol.png]]

Le symbole de l'étoile http://leekwars.com/static//image/icon_tp.png indique le coût en [[PT]] de l'utilisation de cette arme.

Et vous avez peut-être remarqué lorsque vous avez réparti vos [[Points de capital]] que vous en aviez 10. Vous voyez où je veux en venir ?

Cette ligne ne vous fait tirer qu'une seule fois avec votre arme :

<syntaxhighlight>
useWeapon(enemy);
</syntaxhighlight>

Il vous reste donc 7 [[PT]] après l'avoir utilisée. Vous pouvez tirer encore deux fois ! (6 [[PT]] en réalité, à cause du "setWeapon(WEAPON_PISTOL);" qui en consomme 1) 

Modifiez le code pour tirer 3 fois avec votre arme. Vous infligerez bien plus de dégâts.

Si vous débutez en programmation, contentez-vous d'écrire 3 fois l'instruction.

Si vous avez un peu d'expérience, faites-le dans une boucle.


== Utiliser une puce ==

Sachez qu'au niveau 1, vous avez aussi accès à une [[Puce]]. Les puces, contrairement aux armes, n'ont pas besoin d'être "prises en main". Il suffit d'équiper une puce sur la page de votre [[Poireau]] pour pouvoir l'utiliser.

Pour utiliser une puce, il faut se servir de la fonction [[useChip]]. Celle-ci prend deux paramètres : la puce à utiliser et la cible.

Ainsi, pour utiliser la puce [[Décharge]] sur l'ennemi le plus proche, il faut procéder comme ceci :

<syntaxhighlight>
var enemy = getNearestEnemy();
useChip(CHIP_SHOCK, enemy);
</syntaxhighlight>

[[CHIP_SHOCK]] est la constante de la puce [[Décharge]], vous pouvez la trouver sur la fiche de cette puce au [[Marché]].


= Agresser ses congénères =

Votre [[Poireau]] est fin prêt pour les combat !
Il est temps d'aller dans le [[Potager]] pour affronter d'autres poireaux !

Sélectionnez un poireau parmi les 5 proposés pour l'affronter. Vous gagnez de l'[[Expérience]] et des [[Habs]] (La monnaie du jeu) lorsque vous faites un combat au [[Potager]].

Lors de votre premier jour, vous pouvez faire jusqu'à 50 combats. Les autres jours, vous ne pourrez en faire que 30. Si vous ne faites pas tous vos combats quotidiens, sachez qu'ils sont reportés sur un jour. Ainsi, si la veille il vous restait 10 combats à faire, vous en aurez 40 aujourd'hui. Si vous ne les faites pas, vous en aurez 60 le lendemain (les 10 d'hier seront perdus).

[[Image:potagerniveau1.png]]

= Conclusion =

Vous savez désormais tout ce qu'il y a à savoir pour bien commencer sur [[Leek Wars]].

Il vous faudra maintenant améliorer vos compétences de développeur d'IA et de stratège pour progresser.

Si ce n'est pas votre première expérience en programmation, je vous invite à lire ce [https://leekwars.com/help/tutorial Tutoriel] qui vous permettra de vous familiariser avec le langage.

En revanche, si c'est la première fois que vous faites de la programmation, je ne peux que vous conseiller de lire ce [[Tutoriel_LeekScript | Tutoriel sur le LeekScript]].


Bonne chance, jeune Eleveur !
