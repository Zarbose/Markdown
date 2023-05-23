# DB et Big Data

### Installation
```bash
sudo apt install mariadb-server
```

### Initialisation (MariaDB)
```bash
sudo mysql
create database banque;
use banque;
```

### Procédures, fonctions, trigger

#### Procédure
Création d'une table de test : 
```sql
CREATE TABLE Account(
    id int auto_increment,
	LastName varchar(255),
	Solde int,
    primary key (id)
);
```
Ajout de valeurs : 
```sql
INSERT INTO Account (LastName,Solde) VALUES ("Simon",1667);
INSERT INTO Account (LastName,Solde) VALUES ("Heloise",300);
INSERT INTO Account (LastName,Solde) VALUES ("Leopold",0);
```

Création de la procédure ```virement``` : 
```sql
DELIMITER $
CREATE PROCEDURE virement( IN source varchar(255), IN destination varchar(255), IN somme int)
BEGIN	
    	UPDATE Account SET Solde=Solde-somme WHERE LastName=source;
    	UPDATE Account SET Solde=Solde+somme WHERE LastName=destination;
END$
DELIMITER ;
```

Quelque commande sur les procédures : 
```sql
SHOW PROCEDURE STATUS;
DROP PROCEDURE virement;
```

##### Test de la procédure ```virement```  
**Avant**
```sql
MariaDB [banque]> select * from Account;
+----+----------+-------+
| id | LastName | Solde |
+----+----------+-------+
|  1 | Simon    |  1667 |
|  2 | Heloise  |   300 |
|  3 | Leopold  |     0 |
+----+----------+-------+
3 rows in set (0,001 sec)
```
On effectue un virement de 10 euros de ```Simon``` à ```Heloise``` :
```sql
CALL virement("Simon","Heloise",10);
```

**Après**
```sql
MariaDB [banque]> select * from Account;
+----+----------+-------+
| id | LastName | Solde |
+----+----------+-------+
|  1 | Simon    |  1657 |
|  2 | Heloise  |   310 |
|  3 | Leopold  |     0 |
+----+----------+-------+
3 rows in set (0,001 sec)
```
