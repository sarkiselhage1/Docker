Nous avons créé notre fichier Docker dans le dernier chapitre. Il est maintenant temps de créer le fichier Docker. Le fichier Docker peut être construit avec la commande suivante -
![](1.jpeg)
### docker build 
##Apprenons-en plus sur cette commande.
#construction de docker
## docker build  -t ImageName:TagName dir
* -t - est de mentionner une balise à l'image

* ImageName - C'est le nom que vous voulez donner à votre image.

* TagName - Ceci est la balise que vous voulez donner à votre image.

* Dir - Le répertoire où le fichier Docker est présent.Valeur de retour
##Aucun

##Exemple
sudo docker build –t myimage: 0.1.
Ici, myimage est le nom que nous donnons à l'image et 0.1 est le numéro d'étiquette que nous donnons à notre image.

Puisque le fichier Docker est dans le répertoire de travail actuel, nous avons utilisé "." à la fin de la commande pour indiquer le répertoire de travail actuel.

##Sortie
Dans la sortie, vous verrez d’abord que l’image Ubuntu sera téléchargée à partir de Docker Hub, car aucune image n’est disponible localement sur la machine.
![](1.jpeg)
Enfin, lorsque la construction est terminée, toutes les commandes nécessaires sont exécutées sur l'image.
![](2.jpeg)
Vous verrez alors le message construit avec succès et l'ID de la nouvelle image. Lorsque vous exécutez la commande images Docker, vous pourrez alors voir votre nouvelle image.
![](3.jpeg)