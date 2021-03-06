.. _usage:

********************
Tutoriel Utilisateur
********************

.. note::
   Comment utiliser le projet ? Se connecter, utiliser l’application  

Ce projet se lance en 2 parties. La première doit être effectué par l' :ref:`enseignant <administrateur>`. Une fois fait, l'étudiant peut alors accéder à son
:ref:`espace <joueur>`. 

.. _administrateur:

=====================
Partie administrateur
=====================

L'administrateur, contrairement à l'étudiant, doit avoir un compte créé au préalable. 

Création du compte Admin 
------------------------

Pour créer le compte administrateur, il vous faut entrer quelques lignes de commandes. 

La première, vous permettra de voir tous les `containers` Docker du projet 

.. code-block:: console 

   docker ps 

Vous devez obtenir une lite comme celle-ci à l'exception près des id des `containers`. 

.. figure:: ../_static/img/ContainersId.png
   :align: center
   :target: ../../_images/ContainersId.png

   *Liste des containers Docker*

.. _id_container:

Veuillez maintenant copier l'id du `container` nommé `web`. Le nom du container correspond à la deuxième colonne 
appelée `IMAGE` dans les logs, l'id se trouve, quant à lui, dans la première colonne. Ici son id est le *2e1e86347b5a*

Il vous faut maintenant aller dans le dossier du `container` en éxécutant la commande suivante et en remplaçant 
`CONTAINER_ID` par l'id que vous avez :ref:`relevé ci-dessus <id_container>`. 

.. code-block:: console 

   docker exec -it CONTAINER_ID /bin/sh

Ensuite, éxécutez la commande suivante et suivez les instructions. 

.. code-block:: console 

   python django_server/manage.py createsuperuser


Si vous avez bien effectué la procédure, vous devez avoir le message suivant. 

.. figure:: ../_static/img/CreateSuperUserSuccess.png
   :align: center 
   :target: ../../_images/CreateSuperUserSuccess.png

   *Si la procédure s'est bien déroulée*

Utilisation de l'interface administrateur
-----------------------------------------

.. _connexion_admin:

Connexion
^^^^^^^^^

Une fois que le compte administrateur est créé, il peut se rendre sur la `page de connexion <http://127.0.0.1:8000/admin/>`_
admin.

.. figure:: ../_static/img/InterfaceConnexionAdmin.png
   :align: center
   :target: ../../_images/InterfaceConnexionAdmin.png

   *Page de connexion administrateur*

Une fois fait, il arrive sur la page d'accueil de l'interface admin. 

Interface des parties jouées
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. figure:: ../_static/img/InterfaceAccueilAdmin.png
   :align: center
   :target: ../../_images/InterfaceAccueilAdmin.png

   *Page d'accueil de l'administrateur*

On y trouve en 

1. Un bouton pour accéder à l'historique des parties jouées.
2. Un bouton pour créer une nouvelle partie.
3. Ce bouton revient au même que le 1., il permet d'accéder à l'historique des parties.
4. Un résumé de vos dernières actions. 
5. Un bouton permettant d'accéder à tous les utilisateurs qui se sont déjà connectés au moins une fois. 

Création d'une partie
^^^^^^^^^^^^^^^^^^^^^

Pour créer une partie il faut renseigner 5 informations : 

1. Le lien du flux odata.
2. Le Set sur lequel la partie est jouée.
3. Les équipes en jeu. Toutes les lettres collées. Par exemple, si les équipes A, B, C, D et E sont en jeu, il faut remplir "ABCDE". 
4. La date de début de la partie jouée. 
5. L'heure de début de la partie jouée. 

Voici un exemple : 

.. figure:: ../_static/img/InterfaceCreationGameAdmin.png
   :align: center
   :target: ../../_images/InterfaceCreationGameAdmin.png

   *Interface de création d'une partie*

.. _id_partie:

L'ID de la partie en cours
^^^^^^^^^^^^^^^^^^^^^^^^^^

Quand la partie est créée, il faut communiquer aux étudiants l'ID de la partie pour leur permettre
de se connecter à leur tour. L'ID est, dans l'historique des parties jouées *[1]*, le numéro après le 
mot "Game" *[2]*. 

A ce moment là, le programme se met en marche automatiquement et récupère les données du flux odata
toutes les minutes. 

(Voir :ref:`ici <fin_de_partie>` les conditions d'arrêts)

.. figure:: ../_static/img/InterfaceGamesAdmin.png
   :align: center
   :target: ../../_images/InterfaceGamesAdmin.png

   *Interface Games - Historique des parties jouées et en cours*

.. _Au_cours_d_une_partie:

Au cours d'une partie 
^^^^^^^^^^^^^^^^^^^^^

Au cours d'une partie, l'enseignant peut la mettre en pause en utilisant le bouton prévu à cet effect
en bas à droite de la fenêtre de détails de la partie. 

Il pourra, bien entendu, la relancer via le bouton "Play" lorsque la partie reprendra. 

.. _fin_de_partie:

La fin d'une partie 
^^^^^^^^^^^^^^^^^^^

La fin d'une partie peut-être déclenchée par 3 moyens 

1. Nous avons atteint le Jour 10 du Round 8, la partie s'arrête. 
2. L'enseignant clique sur le bouton "Stop", la partie s'arrête. 
3. La partie a été lancée il y a plus de 7 jours, le programme considère que c'est un oubli et la partie est arrêtée.  

.. _joueur:

=============
Partie Joueur
=============

Utilisation de l'interface joueur
---------------------------------

.. _connexion_joueur:

Connexion
^^^^^^^^^

Pour vous `connecter <http://127.0.0.1:8000/login/>`_, il suffit de vous identifier avec votre nom d'équipe *(eg : M_1)*, avec 
votre mot de passe utilisé sur le jeu ERPsim et le :ref:`numéro de la partie <id_partie>` en cours communiqué
par l'enseignant. 

.. warning:: 
   Le mot de passe par défaut sur ERPsim est *ERPSIM*, il vous a été demandé de le 
   changer lors de votre première connexion au jeu. Pour accéder à l'aide, il faut bien entrer
   le NOUVEAU mot de passe que vous avez saisi. 

.. note:: 
   N'importe quelle personne de l'équipe peut se connecter à l'aide. Par contre, il ne peut
   y avoir qu'une seule connexion à l'aide par équipe en simultané.

Quand l'utilisateur se connecte, il est redirigé vers une `page <http://127.0.0.1:8000/admin/>`_ où il trouvera toutes les
informations utiles pour l'aider à jouer. 

Il pourra alors choisir entre avoir une vue sur des :ref:`recommandations <interface_recommandations>` ou une vue
sur les :ref:`évolutions de l'entreprise <interface_evolution>`.

.. note::   
   Ces pages sont mises à jour chaque minute, après chaque jour joué dans la simulation.

.. warning::
   Pour mettre à jour cette page, vous devez rafraîchir la page manuellement *(F5)*

.. _interface_joueur:

Interface de l'aide
^^^^^^^^^^^^^^^^^^^

Dans cette partie, nous pouvons voir tout en haut de l'écran, votre nom de joueur, le Round en cours, le Jour en cours 
ainsi que la date dans la simulation.

.. figure:: ../_static/img/EnteteInterfaceJoueur.png
   :align: center
   :target: ../../_images/EnteteInterfaceJoueur.png

   *Entete de l'interface du joueur*

.. note:: 
      Par défaut, le jeu commence au 1er Janvier. 

Vous y trouverez aussi 2 boutons pour vous renvoyer, soit sur les graphiques d'évolution de l'entreprise, soit sur les tableaux de bas de page. 

.. _tips:

Conseils de départ
""""""""""""""""""

.. figure:: ../_static/img/TipsInterfaceJoueur.png
   :align: center
   :target: ../../_images/TipsInterfaceJoueur.png

   *Conseils donnés au joueur pour démarrer la partie*

La partie *Tips* consiste à donner des conseils au joueur avant que la partie ne commence. En effet, il est recommadé de faire
des modifications sur les prix avant même que le jeu ne commence. Il faut aussi par ailleurs, dispatcher les produits de l'entrpôt 
principal vers les entrepôts régionaux. 

Cette partie est l'objet d'amélioration que vous pouvez trouver dans la partie :ref:`perspective d'évolutions <evolution>`.

.. _interface_evolution:

Interface Evolution
"""""""""""""""""""

.. figure:: ../_static/img/EvolutionInterfaceJoueur.png
   :align: center
   :target: ../../_images/EvolutionInterfaceJoueur.png

   *Graphiques de l'évolution des stocks et des ventes*

La partie évolution se décompose en deux parties : 

* Le graphique des ventes 

Le graphique des ventes est un graphique en barre. Un graphique représente une région (Nord, Sud, Ouest), et une barre représente un produit. |br|
Ainsi, vous pouvez voir très vite, dans quelle région le produit se vend le mieux. 

.. warning::

   Attention à l'axe des ordonnées, qui représente le nombre de ventes, qui n'est pas le même sur chacun des graphiques. 

Grâce à cela, vous avez une répartition des ventes, pour savoir si un produit se vend plus dans le Nord ou dans l'Ouest par exemple. Vous 
pouvez ainsi, mieux gérer vos stocks et envoyer plus de produits dans la région où le produit se vend le mieux. |br|
Plus la partie avance, plus cette répartition des ventes est fiable. 

* Le graphique des stocks

Les 4 graphiques à droite correspondent à chacun des entrepôts : l'entrepôt général, du Nord, du Sud, de l'Ouest. 

Vous pourrez ainsi voir très vite où sont vos produits, si vous avez été réapprovisionné dans l'entrepôt principal, si le dispatche a bien 
été effectué et voir le niveau des stocks baisser avec les ventes. |br|
Cette vue très synthétique vous permettra de prendre des décisions très rapidement. 

.. note::
   
   Vous pouvez sélectionner un produit en double cliquant dessus dans la légende. 

.. _interface_recommandations:

Interface Recommandations
"""""""""""""""""""""""""
Dans la partie recommandation, en bas de page, on retrouve 2 tableaux. 

.. figure:: ../_static/img/TableauxInterfaceJoueur.png
   :align: center
   :target: ../../_images/TableauxInterfaceJoueur.png

   *Tableaux des Recommandations*

.. note:: 

   Chaque ligne des deux tableaux correspond au même produit. Exemple : Première ligne - Milk = $$-T01

* Tableau des transferts de Stock

Dans la tableau de gauche, on retrouve les informations quant aux transferts de stocks, de l'entrepôt principal vers les 
entrpôts régionaux. Il vous suffit alors, après chaque réapprovisionnement dans l'entrepôt principal, de recopier ces valeurs 
dans la transaction *Stock Transfert* d'*ERPSIM* avec un *Push* sur 1 jour. 

.. warning:: 

   N'oubliez pas de *Save* vos changements pour qu'ils soient effectifs. 

Une fois que vous avez sauvegardé vos changements, retournez dans la tuile *Inventory* à droite de la précédente 
afin de voir quand le dispatche est réalisé. Une fois que les entrepôts régionaux ont été fournit, il ne doit plus rester 
que quelques de unités de quelques produits dans l'entrepôt principal. |br|
A ce moment là, deux choix s'offrent à vous, soit vous laissez les paramètres de *Stock Transfert* un jour de plus pour 
que le reste des produits soit transféré vers les entrepôts régionaux et vous effacez les paramètres de transfert de stock, 
soit vous effacez tout de suite toutes les données de *Stock Transfert* et attendez le prochain réaopprovisionnement. 

.. warning:: 

   Quand vous faites un *Clear* des données dans *Stock Transfert*, il faut aussi faire un *Save* pour que vos changements 
   soient pris en compte ! 

Ainsi, répétez ces opérations à chaque réapprovisionnement soit tous les 5 jours. |br| 
Si vous avez bien fait les changements dans *ERPSIM*, au jour suivant dans ERPSIM Helper, le tableau de répartition des stocks 
ne doit contenir que des 0 à l'exception de quelques valeurs si vous avez préféré *Clear* les transferts de stock avant de vider complètement 
l'entrepôt principal. 

.. warning::

   Faites attention au Jour et au Round affiché sur ERPSIM Helper ! Il se peut qu'il y ait un décalage et que le tableau des stocks 
   ne s'actualise pas immédiatement. 

* Tableau des prix de ventes 

Dans le tableau de droite, on retrouve les prix des produits. Les prix sont les mêmes quelques soient les régions. 
Dans la colonne *de droite* on retouve le prix que nous conseillons d'appliquer au produit. La colonne à côté, *A NOTER* 
correspond à l'augmentation ou à la diminution à appliquer au prix pour arriver au prix affiché dans la colonne de droite. 

Par exemple : Si le produit est actuellement à 50€, nous conseillons de le mettre à 55€, alors son prix est augmenté de 10%, c'est ce qui 
est affiché dans la colonne *A METTRE*. 

.. note:: 

   Dans notre aide, les prix sont aumgentés ou baissés de 10%. De cette manière, le prix ne fluctue pas à outrance. Ce facteur permet aussi de changer 
   le prix très vite dans *ERPSIM* en cochant les produits à augmenter et en appliquant 10% d'augmentation sur ceux-ci, ou en cochant les 
   produits à baisser et en appliquant 10% de diminution sur ceux-ci. 

   On pourrait tout de même prévoir, dans la partie :ref:`perspective d'évolution <evolution>`, d'optimiser cette partie pour augmenter 
   ou diminuer le prix d'un certain coefficient pour chaque produit. 

.. warning:: 

   Attention à la latence qu'il peut y avoir entre *ERPSIM* et ERPSIM Helper. Il ne faut pas faire diminuer le prix d'un produit 2 fois 
   dans la même journée. N'oubliez donc pas de vérifier le Jour et le Round en cours, notés en haut de page.

================
Lecture suivante
================

Dans la :ref:`section suivante <fonctionnement>`, vous retrouverez le fonctionnement général du projet. 