## getWeaponEffects

#### Structure

getWeaponEffects(Nombre weapon)  :  TableauDeNombres effects

#### Description

Renvoie les effets de l'arme  **weapon** sous la forme d'un tableau multidimensionnel.

#### Paramètres

-   weapon :  L'id de l'arme dont les effets seront retournés.

#### Retour

-   effects :  Un tableau contenant les effets de l'arme  **weapon**. Chaque effet est lui-même un tableau de la forme [type, min, max, turns, targets].
    -   **type**  est le type d'effet que l'arme applique. Il s'agit d'une constante parmis les [constantes d'effet](#).
    -   **min**  et  **max**  sont la valeur minimum et maximum de l'effet (comme indiqué dans le [marché](#)).
    -   **turns**  est la durée de l'effet en nombre de tours.
    -   **targets**  représente les joueurs qui seront touchés par cet effet dans la zone. Ils sont représentés par les [constantes de cibles](#).

#### Exemple

	for(var effect in getWeaponEffects(WEAPON_GAZOR)){
		if(effect[0] === EFFECT_MAGIC){
			debug('Cette arme empoisonne !') ;
		}
	}

#### Aller plus loin

En combinant cette fonction avec d'autres, il est possible de calculer des choses assez interessantes, comme par exemple les dégats moyens réels qu'une arme va faire.


	function getRealMeanDamage(target){
		var damage = 0 ;
		var strength = 1 + getStrength()/100 ; // Calcul le coefficient de force de votre poireau.
		var relative_shield = getRelativeShield(target) * (1+getResistance(target)/100) ; // Calcul le coefficient du bouclier relatif de la cible.
		var absolute_shield = getAbsoluteShield(target) * (1+getResistance(target)/100) ; // Calcul le coefficient du bouclier absolu de la cible.
		for(var effect in getWeaponEffects(WEAPON_PISTOL)){
			if(effect[0] === EFFECT_DAMAGE){
				damage += (effect[1]+effect[2])/2 * strength * relative_shield - absolute shield ;
			}
		}
		return damage ;
	}

Attention toutefois. Certaines armes ne font pas directement de dégats et d'autres ont des effets sur plusieurs tours, voir les deux ! A vous de prendre ça en compte !
