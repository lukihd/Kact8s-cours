# TP2 Déployer une infrastructure Web avec terraform

>**Vous ne devez pas créer une seule ressource dans AWS depuis la console.** Tout doit être dans terraform, ex keypair, security_groups,...

## Rendu attendu
- Dépot github avec le code source.
- Un Readme qui explique comment vous avez déployés étapes par étapes les ressources dans AWS avec Terraform.
  
## Notation
- Qualité du code Terraform /5 (Code bien formaté et respecte les bonnes pratiques terraform)
- Code fonctionnel /5 (Déploie correctement et l'infrastructure est fonctionnelle)
- Respecte les besoins /10 (Répond aux exigences exprimées dans le schéma d'architecture)

>Je tenterai de débugger votre code pendant 10min si il n'est pas fonctionnel lors du rendu.


## Prérequis

Installer la cli AWS : https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
Installer terraform : https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Dans le service IAM d'AWS sélectionnez votre utilisateur et cliquez sur créé une `Access Key`
dans la cli aws entrez la commande : `aws configure`
entrez les credentials liés à votre access key, la région est `eu-west-1`

## Sujet

L'objectif de ce TP est de déployer une infrastructure web avec Terraform en se basant sur un schéma d'architecture ([schéma](./architecture.jpg)). Utilisez le schéma pour comprendre les inter-connexions entre les services

Si vous avez besoin d'un récap sur terraform allez voir [ici](../README.md#fonctionnement-de-terraform)

Chaque ressource du TP que vous déploieront devront avoir les nom :`nomDuService-nomPrénom` ex mon launch_template s'appellera : launchTemplate-lucasErisset

On déploiera les services suivants :

- 1 `bucket S3` avec le nom : ynov-infracloud-nomprénom
  - envoie du fichier assets/puppy.jpg dans le bucket
  - rendre public l'accès au bucket avec un policy AWS.

- 1 `launch_template` contenant la configuration de la VM à partir des informations suivantes :
  - image_id : ami-012ba92271e91512d
  - instance_type : t2.micro
  - user_data : (encodé en base64 pour que le site puisse se lancer)
    ```shell
      #!/bin/bash
      cd /home/ubuntu/app/
      sudo docker compose up --build -d
    ```
  - une carte réseau qui à minima :
    - doit avoir une ip publique
    - doit être supprimée quand la vm est supprimée
  - security group a minima :
    - attacher le security group de la DB : sg-04891020a5d7968f5
    - une règle security group qui donne accès en inbound au loadbalancer
    - une règle security group qui donne accès en inbound en ssh depuis internet

- 1 `autoscaling group` pour déployer automatiquement des instances à partir d'un `launch_template`
  - 2 instances max
  - 2 instances désirées

- 1 `load balancer applicatif` sur le port 80
  - un security group depuis internet vers le port 80 des EC2
  - Subnets id : subnet-0e3b5a73eb879dbe8 -> eu-west-1a
  - Subnets id : subnet-00c1a909f003623cf -> eu-west-1b
- 1 `listener` sur le port 80 pour le load balancer
- 1 `target_group` sur le port 80 lié automatiquement aux instances de l'autoscaling

