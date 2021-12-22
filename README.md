# Puppet

## Vocabulaire Puppet
    Noeud (Node) : serveur ou poste de travail administré par Puppet ;
    Site : ensemble des noeuds gérés par le Puppet Master ;
    Classe : moyen dans Puppet de séparer des morceaux de code ;
    Module : unité de code Puppet qui est réutilisable et pouvant être partagé ;
    Catalogue : ensemble des classes de configuration à appliquer à un nœud ;
    Facter : librairie multi-plateforme qui fournit à Puppet sous forme de variables les informations propres au système (nom, adresse ip, système d’exploitation, etc.) ;
    Ressource (Resource): objet que Puppet peut manipuler (fichier, utilisateur, service, package, etc.) ;
    Manifeste (Manifest) : regroupe un ensemble de ressource.

## Architecture
Puppet conseille de coupler son fonctionnement avec un gestionnaire de version type « git ». Un serveur PuppetMaster contient la configuration commune et les points de différence entre machines ;

Chaque client fait fonctionner puppetd qui :
   * applique la configuration initiale pour le nœud concerné ;
   * applique les nouveautés de configuration au fil du temps ;
   * s’assure de manière régulière que la machine correspond bien à la configuration voulue.

La communication est assurée via des canaux chiffrés, en utilisant le protocole https et donc TLS (une mini-pki est fournie).

Toute la configuration (le référentiel) de Puppet est centralisée dans l’arborescence /etc/puppet du serveur de référence :

    /etc/puppet/manifests/site.pp : est le premier fichier analysé par Puppet pour définir son référentiel. Il permet de définir les variables globales et d’importer des modules ;

    /etc/puppet/manifests/node.pp : permet de définir les nœuds du réseau. Un nœud doit être défini par le nom FQDN de la machine ;

    /etc/puppet/modules/<module> : sous-répertoire contenant un module.

