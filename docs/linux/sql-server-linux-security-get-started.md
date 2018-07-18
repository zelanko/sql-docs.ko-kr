---
title: Linux의 SQL Server 보안 시작 | Microsoft Docs
description: 이 문서에서는 일반적인 보안 동작을 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: sql-linux
ms.openlocfilehash: 0d7f2244a20f117d2886cdee59d54adfa4029721
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020336"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Linux의 SQL Server의 보안 기능에 대 한 연습

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server의 새로운 Linux 사용자 인 경우 다음 작업을 안내 보안 작업의 일부입니다. 이러한 고유한 또는 Linux를 특정 아니지만 추가 조사를 위해 영역의 아이디어를 제공 하는 데 도움이 됩니다. 각 예제에서는 해당 영역에 대 한 자세한 설명서 링크가 제공 됩니다.

>  [!NOTE]
>  다음 예에서는 합니다 **AdventureWorks2014** 샘플 데이터베이스. 이 샘플 데이터베이스를 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows에서 Linux에 SQL Server 데이터베이스를 복원](sql-server-linux-migrate-restore-database.md)합니다.


## <a name="create-a-login-and-a-database-user"></a>로그인 및 데이터베이스 사용자 만들기 

다른 로그인을 만들고 사용 하 여 master 데이터베이스에서 SQL Server에 대 한 액세스 부여 합니다 [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) 문입니다. 예를 들어:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

>  [!NOTE]
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

나중에 권한을 부여할 수 있습니다 부여 하 여 자세한 로그인을 만들려면 다른 로그인을 `ALTER ANY LOGIN` 권한. 데이터베이스 내에서 권한을 부여할 수 있습니다 다른 사용자가 부여 하 여 더 많은 사용자를 만들 수는 `ALTER ANY USER` 권한. 예를 들어:   

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

사용자-데이터베이스에 연결할 첫 번째 사용자는 관리자 및 데이터베이스 소유자 계정이 됩니다. 그러나 이러한 사용자가 모든는 데이터베이스에서 사용할 수 있는 권한입니다. 이것은 자세한 사용 권한 보다 대부분의 사용자에 게 있어야 합니다. 

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

사용 권한 시스템에 대 한 자세한 내용은 참조 하세요. [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)합니다.


## <a name="configure-row-level-security"></a>행 수준 보안 구성  

[행 수준 보안](../relational-databases/security/row-level-security.md) 쿼리를 실행 하는 사용자에 따라 데이터베이스의 행에 대 한 액세스를 제한할 수 있도록 합니다. 이 기능은 고객은 자신의 데이터에만 액세스할 수 있습니다 또는 작업 자가 자신의 부서에 관련 된 데이터에만 액세스할 수 있습니다와 같은 시나리오에 유용 합니다.   

다음 단계에서는 두 명의 사용자가 다른 행 수준 액세스를 사용 하 여 설정 하 여 `Sales.SalesOrderHeader` 테이블입니다. 

행 수준 보안을 테스트 하려면 두 개의 사용자 계정을 만듭니다.    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

읽기 액세스 권한을 부여 합니다 `Sales.SalesOrderHeader` 테이블 모두에 게:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
새 스키마 및 인라인 테이블 반환 함수를 만듭니다. 에 1을 반환 하는 함수를 `SalesPersonID` 열 ID와 일치할는 `SalesPerson` 로그인 또는 쿼리를 실행 하는 사용자가 Manager 사용자 경우.   
   
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

필터 및 테이블에 대 한 차단 조건자로 함수를 추가 하는 보안 정책을 만듭니다.  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

다음 쿼리를 실행 합니다 `SalesOrderHeader` 각 사용자 테이블입니다. 확인 `SalesPerson280` 95는 자신의 판매 하 고 있는 행만 표시 합니다 `Manager` 테이블의 모든 행을 볼 수 있습니다.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
정책을 사용하지 않도록 보안 정책을 변경합니다.  이제 두 사용자는 모든 행을 액세스할 수 있습니다. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>동적 데이터 마스킹 설정

[동적 데이터 마스킹](../relational-databases/security/dynamic-data-masking.md) 완전히 또는 부분적으로 특정 열을 마스킹하 여 응용 프로그램의 사용자에 게 중요 한 데이터 노출을 제한할 수 있습니다. 

사용 하 여는 `ALTER TABLE` 문에 추가 하는 마스킹 함수를 추가 합니다 `EmailAddress` 열에는 `Person.EmailAddress` 테이블: 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
새 사용자를 만듭니다 `TestUser` 사용 하 여 `SELECT` 테이블에 대 한 권한으로 쿼리를 실행 한 다음 `TestUser` 마스킹된 데이터를 보려면:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
마스킹 함수에서 첫 번째 레코드에 메일 주소 변경 되는지 확인 합니다.
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>투명한 데이터 암호화 사용

데이터베이스에 대 한 위협을 하드 드라이브에서 데이터베이스 파일을 도용는 누군가가 위험이 초래 됩니다. 이 파일 (예: 랩톱)를 포함 하는 컴퓨터의 도용 또는 문제 직원의 동작을 통해 시스템에 대 한 관리자 권한 액세스를 가져오는 경우가 침입을 사용 하 여 발생할 수 있습니다.

Transparent Data Encryption (TDE)는 하드 드라이브에 저장 된 데이터 파일을 암호화 합니다. Master 데이터베이스는 SQL Server 데이터베이스 엔진에 암호화 키를 있으므로 데이터베이스 엔진 데이터를 조작할 수 있습니다. 키에 액세스 하지 않고 데이터베이스 파일을 읽을 수 없습니다. 고급 관리자를 관리 하 고 백업 하 고 데이터베이스를 이동할 수 있지만 선택한 사람에 의해서만 키를 다시 만들 수 있습니다. TDE를 구성 하는 경우는 `tempdb` 데이터베이스도 자동으로 암호화 됩니다. 

데이터베이스 엔진 데이터를 읽을 수 있으므로 투명 한 데이터 암호화 직접 메모리를 읽을 하거나 관리자 계정을 통해 SQL Server에 액세스할 수 있는 컴퓨터의 관리자가 무단된 액세스 로부터 보호 하지 않습니다.

### <a name="configure-tde"></a>TDE를 구성 합니다.

- 마스터 키 만들기
- 마스터 키로 보호되는 인증서를 만들거나 얻기
- 데이터베이스 암호화 키를 만들고 인증서로 키 보호
- 암호화를 사용하도록 데이터베이스 설정

TDE를 구성 하려면 `CONTROL` master 데이터베이스에 대 한 권한 및 `CONTROL` 사용자 데이터베이스에 대 한 권한이 있습니다. 일반적으로 관리자는 TDE를 구성합니다. 

다음 예에서는 `AdventureWorks2014` 라는 서버에 설치된 인증서를 사용하여 `MyServerCert`데이터베이스를 암호화하고 암호를 해독하는 방법을 보여 줍니다.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;  
GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

TDE를 제거 하려면 실행 `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

암호화 및 암호 해독 작업은 SQL Server가 백그라운드 스레드에서 예약 됩니다. 이 항목의 뒷부분에 나오는 카탈로그 뷰 및 동적 관리 뷰를 사용하여 이러한 작업의 상태를 볼 수 있습니다.   

>  [!WARNING]
>  TDE가 사용된 데이터베이스의 백업 파일도 데이터베이스 암호화 키를 사용하여 암호화됩니다. 따라서 이러한 백업 파일을 복원하려면 데이터베이스 암호화 키를 보호하는 인증서를 사용할 수 있어야 합니다. 즉, 데이터베이스 백업뿐만 아니라 데이터 손실을 방지하기 위해 서버 인증서의 백업도 유지 관리해야 합니다. 인증서를 더 이상 사용할 수 없을 경우 데이터 손실이 발생합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  

TDE에 대 한 자세한 내용은 참조 하세요. [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md)합니다.   


## <a name="configure-backup-encryption"></a>백업 암호화를 구성 합니다.
SQL Server에는 백업을 만드는 동안 데이터를 암호화 하는 기능이 있습니다. 암호화 알고리즘 및 암호기 (인증서 또는 비대칭 키)를 지정 하 여 백업을 만들 경우에 암호화 된 백업 파일을 만들 수 있습니다.    
  
> [!WARNING]  
>  인증서나 비대칭 키를 백업하는 것이 매우 중요하며, 이때 가급적이면 인증서나 비대칭 키를 사용하여 암호화한 백업 파일과 다른 위치에 백업하는 것이 좋습니다. 인증서나 비대칭 키가 없으면 백업을 복원할 수 없으므로 백업 파일을 사용할 수 없게 됩니다. 
 
 
다음 예제에서는 인증서를 만들고 인증서로 보호 되는 백업을 만듭니다.
```
USE master;  
GO  
CREATE CERTIFICATE BackupEncryptCert   
   WITH SUBJECT = 'Database backups';  
GO 
BACKUP DATABASE [AdventureWorks2014]  
TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

자세한 내용은 [백업 암호화](../relational-databases/backup-restore/backup-encryption.md)합니다.


## <a name="next-steps"></a>다음 단계

SQL Server의 보안 기능에 대 한 자세한 내용은 참조 [SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대 한 보안 센터](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)합니다.
