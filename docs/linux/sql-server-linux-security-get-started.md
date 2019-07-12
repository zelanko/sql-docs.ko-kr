---
title: Linux의 SQL Server 보안 시작
description: 이 문서에서는 일반적인 보안 동작을 설명 합니다.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 9fe29cadaa14168871e7448350d41bc89afed05b
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834746"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Linux의 SQL Server의 보안 기능에 대 한 연습

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server의 새로운 Linux 사용자 인 경우 다음 작업을 안내 보안 작업의 일부입니다. 이러한 고유한 또는 Linux를 특정 아니지만 추가 조사를 위해 영역의 아이디어를 제공 하는 데 도움이 됩니다. 각 예제에서는 해당 영역에 대 한 자세한 설명서 링크가 제공 됩니다.

> [!NOTE]
>  다음 예에서는 합니다 **AdventureWorks2014** 샘플 데이터베이스. 이 샘플 데이터베이스를 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows에서 Linux에 SQL Server 데이터베이스를 복원](sql-server-linux-migrate-restore-database.md)합니다.


## <a name="create-a-login-and-a-database-user"></a>로그인 및 데이터베이스 사용자 만들기 

다른 로그인을 만들고 사용 하 여 master 데이터베이스에서 SQL Server에 대 한 액세스 부여 합니다 [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) 문입니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  항상 이전 명령에서 별표 대신 강력한 암호를 사용 합니다.

로그인은 SQL Server에 연결 하 고 (제한 된 권한)으로 master 데이터베이스에 액세스할 수 있습니다. 사용자가 사용자 데이터베이스에 연결 하려면 로그인 이라는 데이터베이스 사용자, 데이터베이스 수준에서 해당 id를 해야 합니다. 사용자가 각 데이터베이스에만 적용 되며 액세스 권한을 부여 하려면 각 데이터베이스에 개별적으로 만들어야 합니다. 다음 예제에서는 AdventureWorks2014 데이터베이스를 이동 하 고 사용 하 여는 [CREATE USER](../t-sql/statements/create-user-transact-sql.md) 문을 Larry 라는 로그인과 연결 된 Larry 이라는 사용자를 만듭니다. 로그인 및 사용자 (서로에 매핑됨) 관련 된, 경우에 다른 개체입니다. 로그인이는 서버 수준 보안 주체입니다. 사용자가 데이터베이스 수준 보안 주체입니다.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server 관리자 계정 데이터베이스에 연결할 수 있으며 자세한 로그인 및 사용자 데이터베이스에서 만들 수 있습니다.  
- 사용자 데이터베이스를 만들 때 해지기 데이터베이스 소유자는 데이터베이스에 연결할 수 있습니다. 데이터베이스 소유자는 더 많은 사용자를 만들 수 있습니다.

나중에 권한을 부여할 수 있습니다 부여 하 여 자세한 로그인을 만들려면 다른 로그인을 `ALTER ANY LOGIN` 권한. 데이터베이스 내에서 권한을 부여할 수 있습니다 다른 사용자가 부여 하 여 더 많은 사용자를 만들 수는 `ALTER ANY USER` 권한. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

Larry 로그인 자세한 로그인을 만들 수는 이제 만들어 사용자 Jerry 수 더 많은 사용자.


## <a name="granting-access-with-least-privileges"></a>최소 권한으로 액세스 권한 부여

사용자-데이터베이스에 연결할 첫 번째 사용자는 관리자 및 데이터베이스 소유자 계정이 됩니다. 그러나 이러한 사용자 데이터베이스에서 사용할 수 있는 모든 권한을 가집니다. 이것은 자세한 사용 권한 보다 대부분의 사용자에 게 있어야 합니다. 

바로 시작 하는, 하는 경우 기본 제공을 사용 하 여 사용 권한의 몇 가지 일반적인 범주를 할당할 수 있습니다 *고정 데이터베이스 역할*입니다. 예를 들어를 `db_datareader` 고정된 데이터베이스 역할을 데이터베이스의 모든 테이블을 읽을 수 있지만 변경 하지 않습니다. 사용 하 여 고정된 데이터베이스 역할의 멤버 자격을 부여 합니다 [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) 문입니다. 다음 예제에서는 사용자를 추가 `Jerry` 에 `db_datareader` 고정된 데이터베이스 역할.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

고정된 데이터베이스 역할의 목록을 참조 하세요 [데이터베이스 수준 역할](../relational-databases/security/authentication-access/database-level-roles.md)입니다.

(권장) 데이터를 보다 정밀 하 게 액세스를 구성 하려면 준비가 되었을 때 사용 하 여 고유한 사용자 정의 데이터베이스 역할을 만들려면 나중 [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) 문입니다. 그런 다음 특정 세부적인 권한을 할당 하면 사용자 지정 역할입니다.

예를 들어 다음 문은 라는 데이터베이스 역할을 만듭니다 `Sales`, 부여는 `Sales` 참조, 업데이트 및에서 행을 삭제 하는 기능 그룹을 `Orders` 테이블을 선택한 다음 사용자를 추가 `Jerry` 에 `Sales` 역할.   
   
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
보안 정책 SalesFilter 만들기   
필터 조건자 Security.fn_securitypredicate(SalesPersonID) 추가    
  Sales.SalesOrderHeader에   
차단 조건자 Security.fn_securitypredicate(SalesPersonID) 추가    
  Sales.SalesOrderHeader에   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
되돌리기; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
되돌리기;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
보안 정책 SalesFilter ALTER   
사용 하 여 (상태 = OFF).    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
사용 하 여 AdventureWorks2014; 이동 ALTER TABLE Person.EmailAddress     ALTER 열 EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
사용자 TestUser 만들 로그인 없이   
권한 부여 선택 ON Person.EmailAddress TestUser; 하려면    
 
EXECUTE AS USER = 'TestUser';   
선택 EmailAddressID, EmailAddress Person.EmailAddress;에서       
되돌리기;    
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
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

만들 인증서 MyServerCert SUBJECT = '내 데이터베이스 암호화 키 인증서';  
GO  

USE AdventureWorks2014;   GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
서버 인증서 MyServerCert; 암호화  
GO
  
ALTER DATABASE AdventureWorks2014  
입력 시 암호화 설정   
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
사용 하 여 마스터;   이동   인증서 BackupEncryptCert 만들기   SUBJECT = '데이터베이스 백업';   데이터베이스 백업 [AdventureWorks2014] 이동   디스크로 N'/var/opt/mssql/backups/AdventureWorks2014.bak ='  
의 모든 멘션을  
  압축  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   서버 인증서 BackupEncryptCert =  
   ),  
  STATS = 10  
GO  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
