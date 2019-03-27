Nous avons déjà appris à utiliser Docker File pour créer nos propres images personnalisées. Voyons maintenant comment créer une image de serveur Web pouvant être utilisée pour créer des conteneurs.

Dans notre exemple, nous allons utiliser le serveur Web Apache sur Ubuntu pour créer notre image. Suivez les étapes ci-dessous pour construire notre fichier Docker de serveur Web.

Étape 1 - La première étape consiste à créer notre fichier Docker. Utilisons vim et créons un fichier Docker avec les informations suivantes.

FROM ubuntu 
RUN apt-get update 
RUN apt-get install –y apache2 
RUN apt-get install –y apache2-utils 
RUN apt-get clean 
EXPOSE 80 CMD [“apache2ctl”, “-D”, “FOREGROUND”]

Les points suivants doivent être notés à propos des déclarations ci-dessus -

* Nous créons d’abord notre image à partir de l’image de base Ubuntu.

* Ensuite, nous allons utiliser la commande RUN pour mettre à jour tous les paquets sur le système Ubuntu.

* Ensuite, nous utilisons la commande RUN pour installer apache2 sur notre image.

* Nous utilisons ensuite la commande RUN pour installer les packages d’utilitaires apache2 nécessaires sur notre image.

* Ensuite, nous utilisons la commande RUN pour nettoyer tous les fichiers inutiles du système.

* La commande EXPOSE permet d’exposer le port 80 d’Apache du conteneur à l’hôte Docker.

* Enfin, la commande CMD est utilisée pour exécuter apache2 en arrière-plan.


![](1.jpeg)

Maintenant que les détails du fichier ont été entrés, enregistrez simplement le fichier.

Étape 2 - Exécutez la commande de compilation Docker pour générer le fichier Docker. Cela peut être fait en utilisant la commande suivante -

sudo docker build –t = ”mywebserver”.
Nous étiquetons notre image en tant que mywebserver. Une fois l'image créée, vous recevrez un message indiquant que le fichier a été créé.

![](2.jpeg)
Étape 3 - Le fichier du serveur Web étant maintenant créé, il est maintenant temps de créer un conteneur à partir de l'image. Nous pouvons le faire avec la commande d'exécution Docker.

sudo docker run –d –p 80:80 mywebserver 
![](3.jpeg)

Les points suivants doivent être notés à propos de la commande ci-dessus -

* Le numéro de port exposé par le conteneur est 80. Par conséquent, avec la commande –p, nous mappons le même numéro de port sur le numéro de port 80 de notre hôte local.

* L'option –d permet d'exécuter le conteneur en mode détaché. Cela permet au conteneur de s'exécuter en arrière-plan.

Si vous allez sur le port 80 de l'hôte Docker dans votre navigateur Web, vous verrez maintenant qu'Apache est opérationnel.

![](4.jpeg)
