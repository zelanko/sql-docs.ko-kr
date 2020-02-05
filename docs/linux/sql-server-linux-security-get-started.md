---
title: Linux에서 SQL Server 보안 시작
description: 이 문서에서는 일반적인 보안 작업을 설명합니다.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 1e64ce76ef2528c96ecc0206b7a56b31d4c95ef7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68019504"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>SQL Server on Linux의 보안 기능 연습

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server를 처음 사용하는 Linux 사용자인 경우 다음 작업에서 몇 가지 보안 작업을 안내합니다. 이 보안 작업은 Linux에 고유하거나 특정하지 않으며 추가로 조사할 영역에 대한 아이디어를 제공하는 데 도움이 됩니다. 각 예제에서는 해당 영역의 자세한 설명서의 링크가 제공됩니다.

> [!NOTE]
>  다음 예제에서는 **AdventureWorks2014** 샘플 데이터베이스를 사용합니다. 이 샘플 데이터베이스를 구하여 설치하는 방법에 대한 지침은 [Windows에서 Linux로 SQL Server 데이터베이스 복원](sql-server-linux-migrate-restore-database.md)을 참조하세요.


## <a name="create-a-login-and-a-database-user"></a>로그인 및 데이터베이스 사용자 만들기 

[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) 문을 통해 master 데이터베이스에서 로그인을 만들어 SQL Server에 대한 액세스 권한을 다른 사용자에게 부여합니다. 다음은 그 예입니다.

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  이전 명령에서 별표 대신 항상 강력한 암호를 사용합니다.

로그인은 SQL Server에 연결하고 master 데이터베이스에 대한 액세스 권한을 가질 수 있습니다(제한적 권한). 사용자 데이터베이스에 연결하려면 데이터베이스 사용자라고도 하는 데이터베이스 수준의 해당 ID가 로그인에 필요합니다. 사용자는 각 데이터베이스에 관련되며 각 데이터베이스에서 개별적으로 만들어 액세스 권한을 부여해야 합니다. 다음 예제에서는 AdventureWorks2014 데이터베이스로 이동한 다음, [CREATE USER](../t-sql/statements/create-user-transact-sql.md) 문을 사용하여 Larry라는 로그인과 연결된 Jerry라는 사용자를 만듭니다. 로그인과 사용자는 관련되지만(서로에 매핑됨) 서로 다른 개체입니다. 로그인은 서버 수준 보안 주체입니다. 사용자는 데이터베이스 수준 보안 주체입니다.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server 관리자 계정은 모든 데이터베이스에 연결할 수 있으며 모든 데이터베이스에서 추가 로그인과 사용자를 만들 수 있습니다.  
- 사용자가 데이터베이스를 만들면 데이터베이스 소유자가 되며 해당 데이터베이스에 연결할 수 있습니다. 데이터베이스 소유자는 추가 사용자를 만들 수 있습니다.

나중에 다른 로그인에 `ALTER ANY LOGIN` 권한을 부여하여 추가 로그인을 만들 권한을 부여할 수 있습니다. 데이터베이스 내에서 다른 사용자에게 `ALTER ANY USER` 권한을 부여하여 추가 사용자를 만들 권한을 부여할 수 있습니다. 다음은 그 예입니다.   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

이제 로그인 Larry는 추가 로그인을 만들 수 있으며 사용자 Jerry는 추가 사용자를 만들 수 있습니다.


## <a name="granting-access-with-least-privileges"></a>최소 권한이 포함된 액세스 권한 부여

사용자 데이터베이스에 연결하는 첫 번째 사용자는 관리자 및 데이터베이스 소유자 계정이 됩니다. 그러나 이 사용자는 데이터베이스에서 사용할 수 있는 모든 권한을 가집니다. 이 권한은 대부분의 사용자가 가지는 것보다 많은 권한입니다. 

처음 시작하는 경우 기본 제공 ‘고정 데이터베이스 역할’을 사용하여 몇 가지 일반적인 권한 범주를 할당할 수 있습니다.  예를 들어 `db_datareader` 고정 데이터베이스 역할은 데이터베이스의 모든 테이블을 읽을 수 있지만 변경하지는 않습니다. [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) 문을 사용하여 고정 데이터베이스 역할의 멤버 자격을 부여합니다. 다음 예제에서는 `Jerry` 고정 데이터베이스 역할에 사용자 `db_datareader`를 추가합니다.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

고정 데이터베이스 역할 목록을 보려면 [데이터베이스 수준 역할](../relational-databases/security/authentication-access/database-level-roles.md)을 참조하세요.

나중에 데이터에 대한 보다 정확한 액세스를 구성할 준비가 되면(권장됨) [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) 문을 사용하여 사용자 정의 데이터베이스 역할을 만듭니다. 그런 다음, 사용자 지정 역할에 특정 세분화된 권한을 할당합니다.

예를 들어 다음 문은 `Sales`라는 데이터베이스 역할을 만들고, `Sales` 테이블의 행을 표시, 업데이트 및 삭제하는 기능을 `Orders` 그룹에 부여하고, 사용자 `Jerry`를 `Sales` 역할에 추가합니다.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

For more information about the permission system, see [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## Configure row-level security  

[Row-Level Security](../relational-databases/security/row-level-security.md) enables you to restrict access to rows in a database based on the user executing a query. This feature is useful for scenarios like ensuring that customers can only access their own data or that workers can only access data that is pertinent to their department.   

The following steps walk through setting up two Users with different row-level access to the `Sales.SalesOrderHeader` table. 

Create two user accounts to test the row level security:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Grant read access on the `Sales.SalesOrderHeader` table to both users:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Create a new schema and inline table-valued function. The function returns 1 when a row in the `SalesPersonID` column matches the ID of a `SalesPerson` login or if the user executing the query is the Manager user.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```   

Create a security policy adding the function as both a filter and a block predicate on the table:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
USE AdventureWorks2014; GO ALTER TABLE Person.EmailAddress     ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Verify that the masking function changes the email address in the first record from:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## Enable Transparent Data Encryption

One threat to your database is the risk that someone will steal the database files off of your hard-drive. This could happen with an intrusion that gets elevated access to your system, through the actions of a problem employee, or by theft of the computer containing the files (such as a laptop).

Transparent Data Encryption (TDE) encrypts the data files as they are stored on the hard drive. The master database of the SQL Server database engine has the encryption key, so that the database engine can manipulate the data. The database files cannot be read without access to the key. High-level administrators can manage, backup, and recreate the key, so the database can be moved, but only by selected people. When TDE is configured, the `tempdb` database is also automatically encrypted. 

Since the Database Engine can read the data, Transparent Data Encryption does not protect against unauthorized access by administrators of the computer who can directly read memory, or access SQL Server through an administrator account.

### Configure TDE

- Create a master key
- Create or obtain a certificate protected by the master key
- Create a database encryption key and protect it by the certificate
- Set the database to use encryption

Configuring TDE requires `CONTROL` permission on the master database and `CONTROL` permission on the user database. Typically an administrator configures TDE. 

The following example illustrates encrypting and decrypting the `AdventureWorks2014` database using a certificate installed on the server named `MyServerCert`.


```
USE master;  
이동  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
이동  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
이동  

USE AdventureWorks2014;   GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
이동
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

To remove TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

The encryption and decryption operations are scheduled on background threads by SQL Server. You can view the status of these operations using the catalog views and dynamic management views in the list that appears later in this topic.   

> [!WARNING]
>  Backup files of databases that have TDE enabled are also encrypted by using the database encryption key. As a result, when you restore these backups, the certificate protecting the database encryption key must be available. This means that in addition to backing up the database, you have to make sure that you maintain backups of the server certificates to prevent data loss. Data loss will result if the certificate is no longer available. For more information, see [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

For more information about TDE, see [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## Configure backup encryption
SQL Server has the ability to encrypt the data while creating a backup. By specifying the encryption algorithm and the encryptor (a certificate or asymmetric key) when creating a backup, you can create an encrypted backup file.    
  
> [!WARNING]  
>  It is very important to back up the certificate or asymmetric key, and preferably to a different location than the backup file it was used to encrypt. Without the certificate or asymmetric key, you cannot restore the backup, rendering the backup file unusable. 
 
 
The following example creates a certificate, and then creates a backup protected by the certificate.
```
USE master;   GO   CREATE CERTIFICATE BackupEncryptCert   WITH SUBJECT = 'Database backups';   GO BACKUP DATABASE [AdventureWorks2014]   TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
이동  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
