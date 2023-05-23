# DB et Big Data

### Transaction

Création d'une transaction : 
```sql
DELIMITER $
CREATE PROCEDURE virement( IN source varchar(255), IN destination varchar(255), IN somme int)
BEGIN  
    START TRANSACTION;
        UPDATE Account SET Solde=Solde-somme WHERE LastName=source;
        UPDATE Account SET Solde=Solde+somme WHERE LastName=destination;
    COMMIT;
END$
DELIMITER ;
```
Plus d'info sur la page de [documentation](https://mariadb.com/kb/en/start-transaction/) (23.05.2023)

### Niveaux d'isolation
Il existe plusieurs niveaux d'isolation pour les transactions, ils possèdent chacun leurs avantages et inconvénients :
- READ UNCOMMITTED
- READ COMMITTED
- REPEATABLE READ
- SERIALIZABLE

#### Read Uncommited
Spécifie que les instructions peuvent lire des lignes qui ont été modifiées par d'autres transactions, mais pas encore validées.

Les transactions qui s’exécutent au niveau READ UNCOMMITTED ne génèrent pas de verrous partagés pour empêcher d’autres transactions de modifier des données lues par la transaction en cours. Par ailleurs, les transactions READ UNCOMMITTED ne sont pas bloquées par des verrous exclusifs qui empêcheraient la transaction active de lire des lignes modifiées, mais non validées, par d'autres transactions. Lorsque cette option est définie, vous avez la possibilité de lire des modifications non validées, appelées lectures incorrectes. Les valeurs peuvent changer dans les données et des lignes peuvent apparaître ou disparaître dans le dataset avant la fin de la transaction. Cette option a le même effet que l'activation de l'option NOLOCK dans toutes les tables de toutes les instructions SELECT d'une transaction. Il s'agit du niveau d'isolement le moins restrictif.

#### Read Committed
Spécifie que les instructions ne peuvent pas lire les données modifiées mais non validées par d'autres transactions. Cela permet d'éviter les lectures incorrectes. Les données peuvent être modifiées par d'autres transactions entre deux instructions au sein de la transaction active, ce qui aboutit à des lectures non renouvelables ou à des données fantômes. Cette option a la valeur par défaut SQL Server.

Le comportement de READ COMMITTED dépend de la valeur affectée à l'option de base de données READ_COMMITTED_SNAPSHOT :
- Si l’option READ_COMMITTED_SNAPSHOT a la valeur OFF (valeur par défaut sur SQL Server), le moteur de base de données utilise des verrous partagés pour empêcher d’autres transactions de modifier des lignes pendant que la transaction active exécute une opération de lecture. Les verrous partagés empêchent également l'instruction de lire des lignes modifiées par d'autres transactions, tant que celles-ci ne sont pas terminées. Le type du verrou partagé détermine quand il sera levé. Les verrous de ligne sont levés avant que la ligne suivante ne soit traitée. Les verrous de page sont levés quand la page suivante est lue et les verrous de table sont levés quand l’exécution de l’instruction se termine.
- Si READ_COMMITTED_SNAPSHOT a la valeur ON (valeur par défaut sur Azure SQL Database), le moteur de base de données utilise la gestion de versions de ligne pour présenter à chaque instruction un instantané cohérent des données (du point de vue transactionnel) telles qu’elles étaient au début de l’instruction. Les verrous ne sont pas utilisés pour protéger les données des mises à jour par d'autres transactions.

#### Repeatable Read
Spécifie que les instructions ne peuvent pas lire des données qui ont été modifiées mais pas encore validées par d'autres transactions, et qu'aucune autre transaction ne peut modifier les données lues par la transaction active tant que celle-ci n'est pas terminée.

Des verrous partagés sont placés sur toutes les données lues par chaque instruction de la transaction et maintenus jusqu'à la fin de la transaction. Cela évite que d'autres transactions modifient des lignes qui ont été lues par la transaction active. D'autres transactions peuvent insérer de nouvelles lignes lorsque celles-ci correspondent aux conditions de recherche des instructions émises par la transaction active. Si par la suite la transaction active réexécute l'instruction, elle récupère les nouvelles lignes, ce qui aboutit à des lectures fantômes. Comme les verrous partagés sont maintenus jusqu'à la fin d'une transaction au lieu d'être débloqués à la fin de chaque instruction, l'accès concurrentiel est moindre qu'avec le niveau d'isolation READ COMMITTED par défaut. Utilisez cette option uniquement si c'est nécessaire.

#### Serializable
Spécifie les indications suivantes :

- Les instructions ne peuvent pas lire des données qui ont été modifiées mais pas encore validées par d'autres transactions.
- Aucune autre transaction ne peut modifier des données qui ont été lues par la transaction active tant que celle-ci n'est pas terminée.
- Les autres transactions ne peuvent pas insérer de nouvelles lignes avec des valeurs de clés comprises dans le groupe de clés lues par des instructions de la transaction active, tant que celle-ci n'est pas terminée.

Des verrous de groupes sont placés dans les groupes de valeurs de clés qui correspondent aux conditions de recherche de chaque instruction exécutée dans une transaction. Cela empêche les autres transactions de mettre à jour ou d'insérer des lignes qui pourraient intervenir dans les instructions exécutées par la transaction active. Autrement dit, si l'une ou l'autre des instructions d'une transaction est exécutée une seconde fois, elle lira le même groupe de lignes. Les verrous de groupes sont conservés jusqu'au terme de la transaction. C'est le plus restrictif des niveaux d'isolation, parce qu'il verrouille des groupes de clés entiers et laisse les verrous en place jusqu'à la fin de la transaction. Comme l'accès concurrentiel est plus limité, utilisez cette option uniquement lorsque cela s'avère nécessaire. Cette option a le même effet que l'utilisation de l'option HOLDLOCK dans toutes les tables de toutes les instructions SELECT d'une transaction.

