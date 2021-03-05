# cours-api-symfony
Code du cours sur les API avec Symfony

# Installation

1. Clonez le dépot où vous voulez
2. Installez les dépendances : `composer install`
3. Jouez les migrations : `php bin/console d:m:m`
4. Jouez les fixtures : `php bin/console d:f:l --no-interaction`
5. Lancez le server : `symfony serve` ou `php -S localhost:3000 -t public`

# Erreurs :
**1** 
`but your php version (8.0.0) does not satisfy that requirement.`
* Spécifier la version php dans composer.json comme 8.0

**2** 
`- Root composer.json requires fzaninotto/faker ^1.9 -> satisfiable by fzaninotto/faker[v1.9.0, v1.9.1, v1.9.2].`
* Changer `"fzaninotto/faker": "^1.9"` dans composer.json avec 1.5

**3** 
`PHP Fatal error:  Could not check compatibility between App\DataFixtures\AppFixtures::load(Doctrine\Common\Persistence\ObjectManager $manager) and Doctrine\Common\DataFixtures\FixtureInterface::load(Doctrine\Persistence\ObjectManager $manager), because class Doctrine\Common\Persistence\ObjectManager is not available in C:\xampp\htdocs\cours-api-symfony\src\DataFixtures\AppFixtures.php on line 13`
* Changer `Doctrine\Common\Persistence\ObjectManager` avec `Doctrine\Persistence\ObjectManager $manager` dans AppFixtures.php

**4** 
`Executing script cache:clear [KO]
 [KO]
Script cache:clear returned with error code 1`
`!!
!!  Warning: Module "openssl" is already loaded in Unknown on line 0
!!
!!  In ArrayNode.php line 319:
!!  

!!    Unrecognized options "dir_name, namespace" under "doctrine_migrations". Available options are "all_or_nothing", "check_database_platform", "connection", "custom_template", "em", 
"
!!    factories", "migrations", "migrations_paths", "organize_migrations", "services", "storage".

!!  

!!
!!`
Script @auto-scripts was called via pocomposer req orm-pack --unpack
`>> composer require doctrine/doctrine-migrations-bundle "^2.0" `
* https://github.com/doctrine/DoctrineMigrationsBundle/blob/3.0.x/UPGRADE.md

* Changer
`doctrine_migrations:
    dir_name: '%kernel.project_dir%/src/Migrations'
    namespace: DoctrineMigrations`
    avec
    `doctrine_migrations:
    migrations_paths:
        'DoctrineMigrations': '%kernel.project_dir%/src/Migrations'`
dans symfony-api\config\packages\doctrine_migrations.yaml

Ensuite `composer update`
