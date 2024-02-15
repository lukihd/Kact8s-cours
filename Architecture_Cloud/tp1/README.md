# TP 1 Déployer un site web sur AWS

L'objectif est de déployer grâce à la console :

- Une machine virtuelle (Service EC2)
- Se connecter à la base de donnée existante
- Accéder à l'application depuis internet grâce en affectant une IP publique
- Configurer les flux de la VM depuis la console pour qu'elle ai accès à la DB (security group)


## Créer une machine virtuelle EC2

Créer une machine virtuelle avec les prérequis suivant :
- OS : Amazon Linux 2023 AMI
- Type d'instance : T2.Micro
- Créer une paire de clé SSH pour vous y connecter plus tard
- Network : 
  - Affecter une IP publique
  - Créer un sécurity group qui vous donne accès en SSH et expose le port 80 vers internet
- Stockage : 8go GP3

## Créer la base de donnée RDS

Créer une base de donnée PostgreSQL avec les prérequis suivant :
- Méthode de création : Standard
- Moteur de DB : Postgresql
- Template de l'instance : Free Tier
- Type de l'instance : db.T3.micro
- Connectivité : Connect to EC2 et sélectionnez votre instance EC2
- Pas besoin d'ajouter de security group
- désactiver performance insight
- mettre un nom de db
- désactiver les backup et le chiffrement

## Installer l'application sur l'instance EC2

L'utilisateur de base sur EC2 est ec2-user, vous devrez vous connecter dessus avec le .pem que vous aurez créer lors de la création de la VM.

- Copier les fichiers de l'application dans le dossier home de l'utilisateur ec2-user
- Se connecter à l'instance en SSH
- Renseigner les variables d'environnement de l'application (fichier python) dans la VM avec les informations de la DB
- Installer Docker et Docker compose (Amazon linux est basé sur CentOS donc c'est yum le package manager)
- Se connecter par le navigateur à l'IP de la VM et vérifier que ça fonctionne