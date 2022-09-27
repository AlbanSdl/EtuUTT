## 10.4

Actuelle

### Fonctionnalités

* Ajout de la gestion complète du jeu de caractères `utf8mb4` (emojis, ...)
* Synchronisation avec l'API du guide des UEs en ligne
* Ajout d'un raccourci vers la plateforme de tickets de la scolarité
* Gestion des étudiants en double-diplôme
  * De nouveaux champs sont exposés dans l'API : `formation_list`, `branch_list`, `level_list` et `speciality_list`. Les champs précédents ont été laissés pour permettre la rétrocompatibilité. Garantie de la consistance des données entre ces tableaux (même taille, et la position x dans tous les tableaux correspond au même diplôme)
  * Affichage des doubles diplôme dans le trombi et sur les profils individuels
  * Prise en compte de tous les diplômes lors d'une recherche dans le trombi
* Ajout de filtre et de tri dans la liste des bugs
* Ajout temporaire d'une bannière sur le conflit Ukraine / Russie
* Affichage du nom de l'UE dans la page de validation des commentaires
* Ajout de la possibilité de proposer des nouvelles fonctionnalités
* Ajout des personnels UTT dans le trombi et de filtre sur le statut étudiant / enseignant
* Les photos officielles des utilisateurs sont désormais récupérées via un script externe [utt-profile-pictures](https://github.com/ungdev/utt-profile-pictures) (développé grâce à la lib python [pyutttils](http://github.com/larueli/pyutttils/)) puis placées dans un dossier et récupérées par le site etu.
* Mise à jour de la liste des UEs
* Migration vers Imagick, conservation des métadonnées des images, optimisation du traitement des images (#273, merci @Alabate)
* La commande etu:ue:import synchronise désormais les UEs de la DB avec le CSV (pas d'ajout brut). Les UEs pas dans le CSV sont marquées dépréciées.
* Les étudiants salariés de l'UTT sont également considérés comme étudiants et non plus juste salariés (accès aux commentaires, ...)

### Fix

* Forçage du timezone à Europe/Paris
* Lors de l'application des fixtures, l'ajout de l'utilisateur `user` dans une asso se fait bien avec un groupe
* La route API `/public/orgas/{login}/members` fonctionne (merci @AlbanSdl, PR #272)
* Affichage de tous les présidents d'une asso dans la liste des assos
* Suppressions des `-` dans les slugs des codes d'UEs
* Il est désormais impossible de saisir une adresse en @utt.fr dans le champ adresse mail personnelle.

## 10.3

18 octobre 2021

### Fonctionnalités

* Les utilisateurs peuvent changer leur mot de passe
* Les utilisateurs souhaitant conserver leur compte après leur départ doivent impérativement avoir un compte SIA
* Traductions mises à jour
* Connexion à son compte possible via son compte SIA
* Ajout de discord, des tickets assos dans la barre de menu à droite
* Ajout d'un champ indiquant si une asso est à reprendre ou non (et ajout à l'API)
* Ajout de l'identifiant discord sur son profil et d'un champ indiquant si on veut être syncho avec le discord UTT (et ajout à l'API)
* Affichage des trajets du jour dans le module covoit
* Ajout d'un lien vers le changelog
* La suppression d'un groupe par une asso entraine sa suppression sur le SIA
* La suppression d'une asso entraine la suppression des groupes sur le SIA
* La commande de nettoyage n'envoie plus de message sur slack pour les anciens utilisateurs

### Fix

* Réécriture du système d'authentification par formulaire (connexion externe) via un GuardAuthenticator et non plus via `form_login`.
* Les créneaux de cours étaient fusionnés s'ils étaient à la même heure même salle mais pas même jour
* Les covoits se suppriment correctement
* Les présidents d'asso sont correctement affichés
* Les notifications dans le site ne s'envoyaient pas correctement
* Utilisation de cdnjs pour TinyMCE
* La génération du semestre en cours est correcte pour les annales
* Seuls les mails finissant en utt.fr sont ajoutés au daymail
* Le logo est meilleur
* Affichage des cours du jeudi dans la liste des créneaux d'un cours
* La page des contributeurs est accessible pour les utilisateurs non authentifiés

### Divers

* Utilisation de la fonction addFlash possible, ce qui permet d'afficher plusieurs messages successivement et non un seul
* Listing des comptes SIA à supprimer
* Ajout du monitoring sentry
* Suppression des vieux daymails (plus de 15 jours) dans la commande de nettoyage
* Ajout d'un changelog

## 10.2

28 aout 2021

### Fonctionnalités

* RGPD
  * Ajout d'une page dédiée
  * Option pour effacer complétement son compte
  * Commande pour effacer définitivement les données obsolétes : utilisateurs, associations, token, ...
  * Les utilisateurs sont effacés après deux ans sans connexion
  * Possibilité de supprimer des fichiers déposés
  * Possibilité de masquer son emploi du temps (l'utilisateur apparaitra toujours disponible dans le cumul)
  * Il faut désormais s'authentifier pour accéder aux photos d'utilisateur et aux annales
  * Ajout d'un iframe pour permettre aux utilisateurs de refuser le tracking Matomo
* Le site etu peut désormais envoyer des messages sur slack
* On peut déposer des commentaires d'UEs en anonyme (les administrateurs peuvent lever l'anonymat)
* Chaque commentaire d'UE doit désormais être validé par un administrateur 
* Ajout des logements UTT dans la barre de menu à droite
* Ajout de la recherche d'UE directement sur la page d'accueil
* Amélioration de la recherche sur le trombi
  * Recherche par branche, filière, niveau
  * Recherche si à l'UTT ou ancien
* Refonte de la page des contributeurs

### Fix

* Affichage des jours des créneaux sur mobile

### Divers

* Développement simplifié
  * Dockerfile et docker-compose
  * README mis à jour
  * L'environnement de dev Symfony est plus facilement accessible (un seul fichier app.php)
* Passage de Piwik à Matomo
