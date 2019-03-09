Par défaut, lorsque vous lancez un conteneur, vous utiliserez également une commande shell lors du lancement du conteneur, comme indiqué ci-dessous. C'est ce que nous avons vu dans les chapitres précédents lorsque nous travaillions avec des conteneurs.
![](1.jpeg)
Dans la capture d'écran ci-dessus, vous pouvez constater que nous avons émis la commande suivante -
### sudo docker run –it centos /bin/bash 
Nous avons utilisé cette commande pour créer un nouveau conteneur, puis la commande Ctrl + P + Q pour sortir du conteneur. Cela garantit que le conteneur existe toujours, même après sa sortie du conteneur.

Nous pouvons vérifier que le conteneur existe toujours avec la commande Docker ps. Si nous devions sortir directement du conteneur, le conteneur lui-même serait détruit.

Maintenant, il existe un moyen plus simple d’attacher les conteneurs et de les sortir proprement sans avoir à les détruire. Un moyen d'y parvenir consiste à utiliser la commande nsenter.

Avant d'exécuter la commande nsenter, vous devez d'abord installer l'image nsenter. Cela peut être fait en utilisant la commande suivante -
### docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter

![](2.jpeg)
Avant d'utiliser la commande nsenter, nous devons obtenir l'ID de processus du conteneur, car cela est requis par la commande nsenter. Nous pouvons obtenir l'ID de processus via la commande d'inspection Docker et le filtrer via le Pid.
![](3.jpeg)
Comme indiqué dans la capture d'écran ci-dessus, nous avons d'abord utilisé la commande docker ps pour afficher les conteneurs en cours d'exécution. Nous pouvons voir qu'il existe un conteneur en cours d'exécution avec l'ID de ef42a4c5e663.

Nous utilisons ensuite la commande Docker inspect pour inspecter la configuration de ce conteneur, puis nous utilisons la commande grep pour filtrer simplement l'ID de processus. Et à la sortie, nous pouvons voir que l'ID de processus est 2978.

Maintenant que nous avons l'ID de processus, nous pouvons poursuivre et utiliser la commande nsenter pour établir une liaison avec le conteneur Docker.

entrer
Cette méthode permet de s’attacher à un conteneur sans quitter le conteneur.

# Syntaxe
nsenter –m –u –n –p –i –t commandeID conteneur

# Les options
* -u est utilisé pour mentionner l'espace de noms Uts

* -m est utilisé pour mentionner l'espace de noms de montage

* -n est utilisé pour mentionner l'espace de noms réseau

* -p est utilisé pour mentionner l'espace de noms de processus

* -i s pour que le conteneur s'exécute en mode interactif.

* -t est utilisé pour connecter les flux d'E / S du conteneur au système d'exploitation hôte.

containerID - Il s'agit de l'ID du conteneur.

Commande - Il s'agit de la commande à exécuter dans le conteneur.

## Valeur de retour
Aucun

### sudo nsenter –m –u –n –p –i –t 2978 /bin/bash
![](4.jpeg)

De la sortie, on peut observer les points suivants -

* L'invite passe directement au shell bash lorsque nous émettons la commande nsenter.

* Nous émettons ensuite la commande exit. Normalement, si vous n’utilisiez pas la commande nsenter, le conteneur serait détruit. Mais vous remarquerez que lorsque nous exécutons la commande nsenter, le conteneur est toujours opérationnel.