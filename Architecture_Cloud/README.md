# Architecture Cloud

- [Architecture Cloud](#architecture-cloud)
  - [1. Le Cloud Computing c'est quoi ?](#1-le-cloud-computing-cest-quoi-)
    - [1.1. Définition](#11-définition)
    - [1.2. Cloud Computing VS On Premise Computing](#12-cloud-computing-vs-on-premise-computing)
    - [1.3. Caractéristiques principales du Cloud Computing](#13-caractéristiques-principales-du-cloud-computing)
    - [1.4. Cloud Publique, Privé et Hybride quelle différence](#14-cloud-publique-privé-et-hybride-quelle-différence)
    - [1.5. Les modèles de services dans le Cloud](#15-les-modèles-de-services-dans-le-cloud)
    - [1.7. Les différentes familles de ressources](#17-les-différentes-familles-de-ressources)
    - [1.8. Exemple d'utilisation dans un cadre professionnel](#18-exemple-dutilisation-dans-un-cadre-professionnel)
    - [1.9. Le portail AWS](#19-le-portail-aws)
  - [2. Deep dive dans les ressources d'un Cloud](#2-deep-dive-dans-les-ressources-dun-cloud)
    - [2.1. Les solutions de stockage](#21-les-solutions-de-stockage)
      - [2.1.1. Disques](#211-disques)
      - [2.1.2. Fichiers](#212-fichiers)
    - [2.2. Les ressources de Compute](#22-les-ressources-de-compute)
      - [2.2.1. Machines virtuelles](#221-machines-virtuelles)
      - [2.2.2. Conteneurs](#222-conteneurs)
      - [2.2.3. Fonctions](#223-fonctions)
    - [TP 1 : Monter un site web](#tp-1--monter-un-site-web)
  - [3. Le métier d'Ingénieur Cloud](#3-le-métier-dingénieur-cloud)
    - [3.1. C'est quoi le job d'un Ingénieur Cloud](#31-cest-quoi-le-job-dun-ingénieur-cloud)
    - [3.2. Pas mal de DevOps quand même](#32-pas-mal-de-devops-quand-même)
    - [3.3. Et t'es payé combien ?](#33-et-tes-payé-combien-)
    - [3.2. Les outils de l'Ingénieur Cloud](#32-les-outils-de-lingénieur-cloud)
  - [4 Le Well-Architected Framework l'outil premier de l'Ingénieur Cloud](#4-le-well-architected-framework-loutil-premier-de-lingénieur-cloud)
    - [4.1. Le pilier Operational Excellence](#41-le-pilier-operational-excellence)
    - [4.2. Le pilier de la Fiabilité](#42-le-pilier-de-la-fiabilité)
  - [5. Infrastructure as Code](#5-infrastructure-as-code)
    - [TP 2 : Passer d'un schéma d'architecture au déploiement de l'app](#tp-2--passer-dun-schéma-darchitecture-au-déploiement-de-lapp)
    - [4.3. Le pilier de la Sécurité](#43-le-pilier-de-la-sécurité)
    - [4.4. Services de sécurité d'AWS](#44-services-de-sécurité-daws)
    - [TP 2 : Suite, on ajoute de la sécurité](#tp-2--suite-on-ajoute-de-la-sécurité)
  - [3. Le métier d'Architecte Cloud](#3-le-métier-darchitecte-cloud)
    - [3.1. C'est quoi le job d'un Architecte Cloud](#31-cest-quoi-le-job-dun-architecte-cloud)
    - [3.2. Pas mal de politique quand même](#32-pas-mal-de-politique-quand-même)
    - [3.3. Et t'es payé combien ?](#33-et-tes-payé-combien--1)
    - [3.2. Les outils de l'Architecte Cloud](#32-les-outils-de-larchitecte-cloud)
  - [Comprendre un besoin](#comprendre-un-besoin)
    - [Pilier sustainability](#pilier-sustainability)
    - [Pilier finops](#pilier-finops)

(Jour 1)
## 1. Le Cloud Computing c'est quoi ?

### 1.1. Définition

Le [Cloud Computing](https://www.cnil.fr/fr/definition/cloud-computing) est un terme général désignant une mise à disposition de ressources informatiques à travers Internet par une organisation. Plus communément appelé `le Cloud`, il permet de payer à l'utilisation des serveurs ou services fournis par un fournisseur Cloud aussi appelé `Cloud Service Provider` ou `CSP`.

En simple, vous n'avez pas à acheter de serveurs ou d'appareils réseaux, vous louez et tout est géré par le CSP, on vous livre une majorité de services clé en main et prêt à être configurés en fonction de vos besoins. Pour exemple, le service le plus commun permet de déployer des machines virtuelles à la demande. Vous, en tant que client de ces CSP, allaient demander à provisionner une machine virtuelle sur votre compte avec les spécifications matérielles que vous choisissez et qui influencera le tarif. C'est ce qu'on appelle un service à la demande.

Mais du coup pourquoi avoir son infrastructure chez un CSP plutôt que d'avoir l'infrastructure `On Premise` ?

### 1.2. Cloud Computing VS On Premise Computing

Avoir son infrastructure On Premise signifie qu'on détient et maintient son propre système d'information dans un DataCenter ou un local informatique qui appartient à l'entreprise. Le matériel (serveurs, baies, racks, switch, ...) est acheté par l'entreprise à un instanté puis est remplacé tous les 3 ans en général, impliquant un coût à l’instanté fort. L'avantage premier est la responsabilité du matériel. Par exemple dans le cadre d'une activité sensible, géré sois même son infrastructure, connaître chaque niveau et maîtriser ses données est très important et n'est pas ou difficilement possible avec un CSP. Toutefois pour un StartUp acheter des serveurs et toute une infrastructure en ferais couler plus d'une avant même d'avoir commencer. Avec ce modèle vous achetez des serveurs à plusieurs milliers d'euros avec plus de capacité de prévu pour absorber "la charge". Ce qui signifie que vos serveur ne seront jamais rentabilisés à 100%. La maintenance est aussi détenu par l'entreprise ce qui requiert des compétences rares sur le marché de l'emploi et les métiers de l'informatique ne sont pas les moins bien payés. Tous ces facteurs entraînent plusieurs entreprises à ce poser la question de passer ou de commencer sur un CSP.

Avoir son infrastructure dans le Cloud, c'est contracter avec un CSP pour nous fournir des services informatiques en payant uniquement ce que nous consommons. Pour cela le CSP fourni son infrastructure sous forme de location qui permet à n'importe quel individu d'utiliser ses services à la demande. Ca nous permet par exemple de déployer une seule machine qui nous coûterai 10 Centimes d'euros de l'heure, et lorsque "la charge" augmente on peut en ajouter un second au même prix qui s'arrêtera juste après la montée de charge. Cette flexibilité et les prix agressifs sont les avantages principaux du Cloud, c'est ce qui rend ces outils très attractifs aux entreprises qui souhaitent se développer très vite (startup, scaleup) mais aussi aux plus grosses d'innover bien plus rapidement dans des domaines comme l'intelligence artificielle ou le mainframe qui sont extrêmement coûteux à faire On Premise.

### 1.3. Caractéristiques principales du Cloud Computing

Les caractéristiques principales du Cloud Computing sont donc :

- **La Flexibilité :** Pouvoir lancer une machine, un nouveau service, ou réaliser un PoC en quelques heures sans devoir acheter des serveurs ou développer de nouvelles fonctionnalités sur l'infrastructure existante.
- **Le Coût :** Le `pay as you go` est le modèle le plus connu des CSP et il permet de payer à la demande donc de réduire fortement les coûts. Attention ça peut être à double tranchant une bonne gestion du FinOps est très importante ou les coûts du Cloud dépasseront les coûts On Premise.
- **Les Fonctionnalités :** Un accès instantané à des ressources à l'autre bout du monde, des services qui seraient inaccessibles pour des entreprises de petites tailles comme l’intelligence artificielle ou l'HPC. 
- **Rapidité et agilité :** Déployer en quelques secondes une infrastructure complète du réseau à l'application, en quelques clics ou de façon complètement automatisée. 
  
>L'exemple parfait c'est le développement d'une application. Quand le développer va envoyer son code sur Git, une pipeline va déployer automatiquement une instance de l'application dans le Cloud pour que le développeur puisse la tester, ou tout simplement déployer en production automatiquement.

### 1.4. Cloud Publique, Privé et Hybride quelle différence

Maintenant qu'on sait à quel point le Cloud peut être un vecteur de croissance important pour les entreprises, il faut choisir un modèle de Cloud. Il en existe trois, chacun a ses propres avantages et s'adapte aux besoins de chaque entreprises.

Un Cloud public permet à n'importe quel individu de créer un compte et d'utiliser leurs ressources moyennant de mettre sa carte bleu. Ca nous donne accès aux réseaux les plus vastes du monde ainsi qu'un panel de services informatiques dont vous n'imaginez même pas qui peut en avoir besoin. Les plus connus sont : Amazon Web Services (AWS), Microsoft Azure, Google Cloud Computing (GCP) et en France OVH.

Un Cloud privé à contrario est géré aussi par un CSP mais qui ne met à disposition ses services qu'aux personnes morales (entreprises, associations, ...). Ces CSP disposent eux aussi de leurs propre DataCenter et sont souvent plus régionaux comme Cheops à Bordeaux ou Thalès et Dassault. Ils sont souvent plus spécialisés (mais pas toujours) et vont offrir des services dédiés à des industries comme la défense, ou le bancaire. Il arrive aussi que de grands groupes développent leurs propres CSP en interne pour servir leurs utilisateurs internes. `

Le dernier modèle c'est le Cloud Hybride. C'est le fait d'utiliser plusieurs Cloud Service Providers et de les faire interagir entre eux. Ca s'applique de privé vers publique, publique vers publique ou privé vers privé. Ca a de grands avantages car tous les CSP ne proposent pas les même fonctionnalités. Par exemple Microsoft Azure fourni la plupart des outils d'Active Directory par Microsoft Entra ID et est utilisé par de nombreuses entreprises pour se connecter à un autre provider comme AWS. L’intérêt aussi est de dupliquer son infrastructure ou ses données dans les DataCenter d'une autre entreprise. Ca permet de créer de la redondance en cas de DDoS ou juste d'accès aux données dans une région ou le CSP principal n'est pas déployé. 

Le modèle Hybride est souvent privilégié par les grands groupes tandis que l'utilisation d'un Cloud publique est souvent privilégié par des entités plus petites ou avec des besoins d’expansions rapide à moindre coût.S

### 1.5. Les modèles de services dans le Cloud

Dans le Cloud on utilise différents niveau de responsabilité de l'infrastructure par le bié de modèles dit `As a Service`. On en recense de plus en plus mais les trois qui nous intéressent sont les suivants :

**Infrastructure as a Service (IaaS) :** Ce modèle nous permet de gérer l'infrastructure jusqu'à l'OS. Il est majoritairement utilisé lorsqu'une machine virtuelle est impliquée dans le service. On va donc sélectionner l'hardware que l'on souhaite, sa connectivité réseau et ses disques et gérer tout ce qu'il se passe à partir de l'OS et le CSP n'interviendra pas à ce niveau.

**Platform as a Service (PaaS) :** Ce modèle rend abstrait la couche de l'OS et nous donne directement accès à l'application. Le CSP va donc gérer les mises à jour de l'OS et de l'hardware et voir même de l'application à la demande de l'administrateur. Ici que du clic clic fini les configurations Linux ou Windows. On retrouve ce modèle notamment sur les bases de données dites *managées* dans lesquels on va seulement interagir avec le moteur de base de données mais pas avec l'OS directement. On entend d'ailleurs souvent le terme `Managed instance` ou `Managed service`.

**Software as a Service (SaaS) :** Ce modèle est sûrement le plus commun sur internet, il permet à un utilisateur de consommer une application depuis n'importe quel appareil connecté et en général depuis un navigateur internet en contrepartie d'un abonnement. Ici le fournisseur va gérer les mises à jour, l'infrastructure et ne laissera à l'utilisateur que l'administration de l'application. Ce modèle on le retrouve par exemple chez Github, Elastic Cloud ou tout simplement les CSP Publiques qui fournissent l'accès à leurs services par le biais de ce modèle pour administrer les utilisateurs.

-> Exercice rapide : quel est le meilleur modèle pour le cas en face ?

### 1.7. Les différentes familles de ressources

Les CSP fournissent des `ressources`, qui correspondent à un service, une machine, un disque, ect. Il en existe des familles communes à la majorité :
- Compute : Machines virtuelles, conteneurs, fonctions.
- Stockage : Disques, fichiers, bases de données.
- Intelligence artificielle : LLM, VM dédiées ...
- Sécurité : Gestion des accès et droits (IAM), outils d'audit, guardrails, firewall ...
- Réseau : Cloud privé virtuels, table de routage, outils d'audit réseau, vpn ...

Et plein d'autres.

### 1.8. Exemple d'utilisation dans un cadre professionnel

Ici notre exemple montre l'organisation d'une application web basique avec un système de stockage de fichier qui sert de CDN, une vm front et back pour notre app, la sécurité mise en place autour et le WAF qui va protéger l'application des DDoS par exemple.

-> Montrer une schéma d'archi et expliquer le contexte et la mise en place quite à faire une démo basique de cette infra
### 1.9. Le portail AWS
-> Ils ne vont pas créer de compte je vais leur en fournir un comme ça pas de dépense chelou dans AWS pour eux avec un wipe des ressources le soir.

## 2. Deep dive dans les ressources d'un Cloud

On l'a vu un CSP peut avoir plein de familles de ressources mais les plus communes restent le stockage et le compute. Chez AWS ça ce manifeste par différentes solutions managées ou géré par vous et répondent à des besoins différents.

### 2.1. Les solutions de stockage
#### 2.1.1. Disques

Chez AWS les disques s'appellent EBS (Elastic Block Store). Ce service permet de fournir des disques persistants qui agissent comme des volumes attachés à votre VM. 

Grâce à EBS vous pouvez attacher ou détacher des disques pour les affecter à d'autre VM donc par exemple lors de la migration de version si vous avez stockés vos données sur un disques séparés du root disk vous pourrez le rattacher à la nouvelle VM à jour en quelques clics et presque sans interruption de service.

On peut aussi décider de choisir la performance du disque (SSD/HDD) et surtout l'I/O que vous pouvez envoyer dans le disque. Moins l'I/O est haut moins ce sera cher. Toutes les applications n'ont pas besoin d'un SSD on va donc économiser des sous sur ce genre de détails.

Comme sur n'importe quel fonctionnement avec des disques vous aurez la possibilité de faire des snapshot qui vous permettront des créer d'autre disques à partir du premier. Vous pourrez donc dupliquer une VM ou la faire revenir dans un état initial de la même façon qu'un conteneur.

#### 2.1.2. Fichiers

Chez AWS on retrouve deux service principaux : 

EFS : Elastic File Storage qui va vous permettre d'avoir un partage de fichier NFS entre des VM ou des conteneurs. Notamment utiles quand vous devez centraliser des logs ou si vous avez besoin de partager facilement des fichiers entre vos VM sans payer de VM dédiée.

S3 : Simple Storage Service est un des plus vieux d'AWS, il vous permet de stocker à des coût dérisoires des Terras de données. Ici on s'en sert beaucoup pour stocker des images pour s'en servir de CDN ou alors pour stocker les logs. C'est une solution pour un stockage à long terme et à moindre coût. Aussi S3 est un service Global ce qui signifie que n'importe quel ressource stockées dessus est accessible en quelques microsecondes à travers le globe. Très puissant lorsque vous avez une application disponible à travers le monde entier. Il permet aussi par exemple d'hoster un site web statique pratiquement gratuitement.

### 2.2. Les ressources de Compute
#### 2.2.1. Machines virtuelles

Les VM ici appelée par le service EC2 : Elastic Compute Cloud est le service le plus utilisé de la plateforme et un service que vous retrouverez chez n'importe quel provider. Il permet aux utilisateurs de louer des ressource de compute (ram, cpu, i/o) sur demande, ce qui leur permet de créer et de gérer des instances de serveurs virtuels dans le cloud. EC2 offre une flexibilité exceptionnelle en termes de choix de système d'exploitation, de type d'instance et de capacité de calcul, permettant aux utilisateurs de dimensionner rapidement leurs ressources en fonction de leurs besoins.

En le couplant avec d'autre services comme l'autoscaling on est capable de déployer des machines en fonction du traffic sur l'application ou les ressources consommées par la VM. Il a aussi un intégration étroite avec un grand panel de services comme S3 ou d'autre dont on parlera plus tard qui étant et permet aux applications d'être bien plus performantes.

#### 2.2.2. Conteneurs

ECS ou Elastic Container Service est les service de conteneur à la demande d'AWS. Il permet de déployer un conteneur full managé comme le ferais docker en local. Ici il se décline sous différentes formes pour s'intégrer avec Elastic Kubernetes Service, ou Fargate qui s'approche de docker swarm. Grâce à cette diversité vous pouvez déployer vos conteneur en quelques secondes ce qui est parfait pour une application avec une architecture microservice. Attention ECS est un service presque PaaS il est forcément plus onéreux que d'utiliser une instance EC2 et d'y mettre Docker mais vous demande bien moins de gestion donc à vous de voir ce qui est le plus propice à votre besoin.

#### 2.2.3. Fonctions

Les fonctions ou Lambda chez AWS sont sûrement quelque chose dont vous n'avez jamais entendu parler. Une Lambda c'est un script ou un bout de code exécuté en parallèle par des dizaines, centaines ou milliers de processus. Les fonctions sont très intéressantes pour du traitement de fichier comme des OCR ou pour scaler facilement des appels API. Cet outil est surtout utilisé lorsqu'une application est développée pour fonctionner avec le CSP et d'exploiter ses pleines capacités. Il existe donc des applications comme Amazon Prime Vidéo qui fonctionnaient principalement avec les Lambda mais depuis peu ils ont décidés de changer de paradigme de développement dû au coût élever des Lambda à cette échelle.

### TP 1 : Monter un site web
-> Monter une petite architecture basique db web code déjà fourni juste à installer nginx ect et ça tourne (à réfléchir) 

(Jour 2-3)
## 3. Le métier d'Ingénieur Cloud
### 3.1. C'est quoi le job d'un Ingénieur Cloud

Un ingénieur Cloud c'est un métier de l'IT spécialisé dans la conception, le déploiement, la maintenance et l'optimisation de l'utilisation de resources informatique sur un CSP. Souvent l'ingénieur cloud est spécialisé dans un CSP du fait du nombre de services qu'ils proposent. Le job principal et de récupérer le schéma d'architecture cloud réalisé par l'Architecte Cloud et de le tester dans un environnement de test puis de développer à partir du schéma l'infrastructure et déployer, optimiser ses performance et son coût. Il est en suite en charge de maintenir cette infrastructure et de la faire évoluée au grès des besoins.

### 3.2. Pas mal de DevOps quand même

Ce métier est très lié au mouvement DevOps. Il est donc récurrent de voir qu'un Ingénieur Cloud est aussi DevOps. Souvent l'ingénieur cloud va aussi s'occuper de la partie CI/CD et donc automatiser les déploiement des applications dans le Cloud. Cette double casquette est aussi valable pour des SysAdmin ou pour des Ingénieurs réseaux mais le plus commun reste le DevOps.

### 3.3. Et t'es payé combien ?

En 2024, pour un junior donc en sortant d'école vous pouvez essayer de vous positionner autour de 37K euros brut/ans donc ça fait un peu plus de 2000€ par mois après impôts sans compté les avantages en nature de votre entreprise (ticket restos, PEE, Actions, primes, ect...). Attention ce chiffre est différents en fonctions de vos profils et des recruteurs mais c'est un minimum à visé correct en dessous ne prenez pas le job. Le maximum que vous pourrez espérer serait environ 40k à 42k pour les plus talentueux ou les plus chanceux ! Attention plus ne veut pas dire mieux. Si votre entreprise vous embauche à 42k mais que votre valeur sur le marché est trop haute personne ne voudra vous prendre à ce salaire alors faites attentions dans votre carrière à ne pas coûter trop cher ou personne ne voudra de vous dans les entreprises qui vous intéressent !

Le plus important c'est d'aller dans une entreprise qui vous plaît vous aurez plein d'offres toutes votre carrière mais pour ça répondez aux recruteurs et écoutez ce qu'ils ont à dire et sachez que vous pouvez **TOUJOURS** dire non avant de signer si vous avez mieux ailleurs.

Si vous voulez en savoir plus allez voir ce blog très intéressant : [Les salaires de la tech par Denis Germain](https://blog.zwindler.fr/2024/01/05/salaires-dans-la-tech-quelques-ressources-externes-2023-2024/)

### 3.2. Les outils de l'Ingénieur Cloud

L'ingénieur Cloud utilise différents outils, d'abord les outils de déploiement comme Terraform qui permet de développer et déployer l'infrastructure sur le CSP et Ansible qui permet de configurer les OS et applications. Puis pour permettre d'automatiser ces déploiement on utilise des CI/CD comme Github Actions, Jenkins et des outils de GitOps. Mais l'outil le plus important c'est les guides de bonnes pratiques pour créer une infrastructure dans le Cloud. Vous n'irez pas construire votre maison sans savoir si vous devez utiliser des tuiles ou de la taule pour votre toit ? Pour l'ingénieur Cloud c'est pareil sauf qu'on parler de plusieurs centaines de milliers d'euros voir millions alors on utilise des guides pour bien faire nos infrastructures. Le plus connus c'est celui d'Amazon : The Well-Architected Framework.

## 4 Le Well-Architected Framework l'outil premier de l'Ingénieur Cloud

Le [Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc) est la bible des métiers du Cloud. Ce document existe aussi chez d'autre CSP mais ils se rejoignent tous sur ces six piliers :

- Operational Excellence
- Security
- Reliability
- Performance Efficiency
- Cost Optimization
- Sustainability

Il nous apporte les concepts clés et les bonnes pratiques d'une infrastructure dans le Cloud. Chaque pilier doit être respectés pour avoir une infrastructure la plus évolutive performante et économiquement viable car oui il est très facile de dépenser des milliers sans faire exprès. On va voir ensemble au fur et à mesures de nos séances les différents piliers.

### 4.1. Le pilier Operational Excellence



### 4.2. Le pilier de la Fiabilité
## 5. Infrastructure as Code
### TP 2 : Passer d'un schéma d'architecture au déploiement de l'app
-> Apprendre à utiliser TF et 
(Jour 3)
### 4.3. Le pilier de la Sécurité
### 4.4. Services de sécurité d'AWS
### TP 2 : Suite, on ajoute de la sécurité

## 3. Le métier d'Architecte Cloud
### 3.1. C'est quoi le job d'un Architecte Cloud
### 3.2. Pas mal de politique quand même
### 3.3. Et t'es payé combien ?
### 3.2. Les outils de l'Architecte Cloud

## Comprendre un besoin
### Pilier sustainability
### Pilier finops

