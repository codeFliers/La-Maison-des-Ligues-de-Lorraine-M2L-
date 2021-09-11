# La-Maison-des-Ligues-de-Lorraine-M2L

OBJET:

La Maison des Ligues de Lorraine (M2L) a pour mission de fournir des espaces et des services aux différentes ligues sportives régionales et à d’autres structures hébergées. La M2L est une structure financée par le Conseil Régional de Lorraine dont l'administration est déléguée au Comité Régional Olympique et Sportif de Lorraine (CROSL). 

La Maison des Ligues veut proposer un ensemble de logiciels à tous les clubs sportifs de la région Lorraine pour améliorer leur gestion au quotidien. Elle a reçu une demande du club de tir à l’arc de DOMBASLE, ce club a besoin d’un logiciel pour gérer ses adhérents. La Maison des Ligues a décidé de développer un logiciel de gestion des adhérents pour le club de tir à l’arc.

Présentation globale du projet

Le logiciel doit permettre la gestion des adhérents. On pourra créer un nouvel adhérent, rechercher et lister un adhérent particulier, modifier les données d’un adhérent existant, supprimer un adhérent.
Chaque adhérent doit payer un droit d’adhésion annuel à l’association de tir à l’arc. Le tarif dépend du type d’adhésion (loisir, compétition, entrainement…). On doit pouvoir fixer et modifier le tarif de chaque catégorie. 
On pourra modifier le type d’abonnement au cours de l’année si un utilisateur qui s’était inscrit pour l’entrainement seulement désire faire de la compétition.
L’utilisateur doit pouvoir obtenir un rapport récapitulatif regroupant le montant des adhésions pour chaque catégorie ainsi que le montant total des adhésions.
Un système de login sera intégré avant de pouvoir accèder à l'application.


Description du projet
La gestion des droits
L'accès au logiciel n'est autorisé uniquement qu'aux administrateurs de l'association de tir à l'arc.
Le ou les administrateurs auront un compte personnel avec un identifiant et un mot de passe.

A la première utilisation un écran de connexion sera affiché, l'utilisateur devra y taper son identifiant et son mot de passe pour accéder à l'application.

Pour les utilisations ultérieures l'utilisateur ne doit pas retaper à chaque fois son mot de passe.
Une fois dans l'application, l'utilisateur pourra à tout moment se déconnecter.

La gestion des adhérents et catégories
Une fois l'utilisateur connecté, celui-ci voit une page d'accueil d'où il peut voir les différentes ménus du logiciel.
Il aura accès entre autre à la gestion des adhérents (visionnage, modification, ajout, suppression).
Suivis de celle des différentes catégories (visionnage, modification, ajout, suppression).
Ainsi qu'un module de recherche par nom ou par prénom.
Pour finir, il aura accès à des rapports récapitulatifs (somme par catégorie, adhérents qui n'ont pas payés).

La gestion des adhérents par l'administrateur
L'administrateur sera le seul à pouvoir manier l'application. Il sera donc l'unique personne a être abilité à gérer les fonctions précédemment cités.


Norme graphique:

Visuel dit "fonctionnel" à base du framework Java Swing.

Les principes clés:

Un applicatif efficace et érgonomique.
Utilisable uniquement par un administrateur
Gestion des adhérents de l'association

Le cloisonnement des données:

Dans cette version, elle sera réservé uniquement au club de tire à l'arc "DOMBASLE".

Les fonctionnalités et les règles de gestion:

Les profils
L'uniquement profil sera celui de l'administrateur.

L'application
Les options du menu seront affichées uniquement si l'utilisateur est un administrateur connecté à l'application. L’affichage sera donc conditionné en fonction de l’habilitation.

Les options du menu et sous menus compris
	Options:					Profils:
-Gestion					Administrateur
-Recherche adhérent				Administrateur	
-Rapport récapitulatif				Administrateur


![image](https://user-images.githubusercontent.com/58827656/132957737-5b0bc948-400f-42dc-b87d-4676df6edd7b.png)

Pour faire fonction le fichier jar, utiliser phpmyadmin, cette base de données ayant comme nom 'adherent' :  
``` 
SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Base de donnÃ©es :  `adherent`
--

DELIMITER $$
--
-- ProcÃ©dures
--
CREATE DEFINER=`root`@`localhost` PROCEDURE `ObtenirTypeAdhesion` (IN `id` INT)  READS SQL DATA
select * from TypeAdhesion where idTypeAdhesion = id$$

DELIMITER ;

-- --------------------------------------------------------

--
-- Structure de la table `adherent`
--

CREATE TABLE `adherent` (
  `idAdherent` int(11) NOT NULL,
  `Nom` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `Prenom` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `CodePostal` varchar(6) COLLATE utf8_unicode_ci DEFAULT NULL,
  `Ville` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `DateNaissance` date DEFAULT NULL,
  `TypeAdhesion` int(11) NOT NULL,
  `Telephone` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
  `Email` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
  `Paiement` tinyint(1) NOT NULL DEFAULT '0'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

--
-- Contenu de la table `adherent`
--

INSERT INTO `adherent` (`idAdherent`, `Nom`, `Prenom`, `CodePostal`, `Ville`, `DateNaissance`, `TypeAdhesion`, `Telephone`, `Email`, `Paiement`) VALUES
(28, 'Jean', 'Dupont', '98000', 'Paris', '2000-03-17', 3, '06.22.12.11.28', 'jean.dupont@gmail.com', 1);

-- --------------------------------------------------------

--
-- Structure de la table `administrateur`
--

CREATE TABLE `administrateur` (
  `idAdmin` int(11) NOT NULL,
  `login` varchar(255) NOT NULL,
  `motdepasse` varchar(255) NOT NULL,
  `DateDerVisite` date NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

--
-- Contenu de la table `administrateur`
--

INSERT INTO `administrateur` (`idAdmin`, `login`, `motdepasse`, `DateDerVisite`) VALUES
(1, 'azerty123', 'azerty123', '2017-03-18');

-- --------------------------------------------------------

--
-- Structure de la table `typeadhesion`
--

CREATE TABLE `typeadhesion` (
  `idTypeAdhesion` int(11) NOT NULL,
  `Libelle` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `Tarif` int(2) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

--
-- Contenu de la table `typeadhesion`
--

INSERT INTO `typeadhesion` (`idTypeAdhesion`, `Libelle`, `Tarif`) VALUES
(2, 'CompÃ©tition', 80),
(3, 'Entrainement', 60),
(6, 'Loisir', 50);

--
-- Index pour les tables exportÃ©es
--

--
-- Index pour la table `adherent`
--
ALTER TABLE `adherent`
  ADD PRIMARY KEY (`idAdherent`),
  ADD KEY `fk_Adherent_TypeAdhesion_idx` (`TypeAdhesion`);

--
-- Index pour la table `administrateur`
--
ALTER TABLE `administrateur`
  ADD PRIMARY KEY (`idAdmin`);

--
-- Index pour la table `typeadhesion`
--
ALTER TABLE `typeadhesion`
  ADD PRIMARY KEY (`idTypeAdhesion`);

--
-- AUTO_INCREMENT pour les tables exportÃ©es
--

--
-- AUTO_INCREMENT pour la table `adherent`
--
ALTER TABLE `adherent`
  MODIFY `idAdherent` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=29;
--
-- AUTO_INCREMENT pour la table `administrateur`
--
ALTER TABLE `administrateur`
  MODIFY `idAdmin` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;
--
-- AUTO_INCREMENT pour la table `typeadhesion`
--
ALTER TABLE `typeadhesion`
  MODIFY `idTypeAdhesion` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=7;
--
-- Contraintes pour les tables exportÃ©es
--

--
-- Contraintes pour la table `adherent`
--
ALTER TABLE `adherent`
  ADD CONSTRAINT `fk_Adherent_TypeAdhesion` FOREIGN KEY (`TypeAdhesion`) REFERENCES `typeadhesion` (`idTypeAdhesion`) ON DELETE CASCADE ON UPDATE CASCADE;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
```


