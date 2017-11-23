---
title: "Linux에서 SQL Server 보안 시작 | Microsoft Docs"
description: "이 항목에서는 일반적인 보안 동작을 설명 합니다."
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: 
ms.workload: Inactive
ms.openlocfilehash: faf7903fc945fc1ce966d6bf6560f55c8d494314
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Linux에서 SQL Server의 보안 기능에 대 한 연습

SQL Server에 새로운 Linux 사용자 인 경우 다음 작업에 관한 일부의 보안 작업입니다. 이러한 설정은 고유 하거나 Linux 특정 아니지만 알 수 있는 영역의 추가로 조사를 수행 하는 데 도움이 됩니다. 각 예제에 해당 영역에 대 한 심도 있는 문서에는 링크가 제공 됩니다.

>  [!NOTE]
>  다음 예에서는 사용 된 **AdventureWorks2014** 예제 데이터베이스. 이 예제 데이터베이스를 설치 하는 방법에 지침은 [Linux에 Windows에서 SQL Server 데이터베이스를 복원](sql-server-linux-migrate-restore-database.md)합니다.


## <a name="create-a-login-and-a-database-user"></a>로그인 및 데이터베이스 사용자 만들기 

다른 로그인을 사용 하 여 master 데이터베이스에서 생성 하 여 SQL Server에 대 한 액세스 부여는 [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) 문. 예를 들어

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

>  [!NOTE]
>  항상 위 별표 대신 강력한 암호를 사용 합니다.

로그인은 SQL Server에 연결 및 (제한 된 권한)으로 master 데이터베이스에 액세스할 수 있습니다. 사용자 데이터베이스를 연결 하려면 로그인을 데이터베이스 사용자를 호출 하는 데이터베이스 수준에서 해당 id를 필요 합니다. 사용자가 각 데이터베이스에만 되며 액세스 권한을 부여 하려면 각 데이터베이스에서 개별적으로 만들어야 합니다. 다음 예제에서는 AdventureWorks2014 데이터베이스에 사용자를 이동 하 고 다음 사용 하 여는 [CREATE USER](../t-sql/statements/create-user-transact-sql.md) 문을 Larry Larry 이라는 로그인과 연결 된 명명 된 사용자를 만듭니다. 경우에 로그인과 사용자 (서로 매핑) 관련 된, 서로 다른 개체입니다. 로그인은 서버 수준 원칙입니다. 사용자가 데이터베이스 수준의 보안 주체입니다.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server 관리자 계정 모든 데이터베이스에 연결할 수 있으며 모든 데이터베이스에 더 많은 로그인 및 사용자가 만들 수 있습니다.  
- 다른 사용자가 데이터베이스를 만들 때 해지기 데이터베이스 소유자에 해당 데이터베이스에 연결할 수 있습니다. 데이터베이스 소유자는 더 많은 사용자가 만들 수 있습니다.

나중에 권한을 부여할 수 있습니다 다른 로그인에 부여 하 여 더 많은 로그인을 만들고 사용자는 `ALTER ANY LOGIN` 권한. 데이터베이스 내의 다른 사용자가 부여 하 여 더 많은 사용자가 만들 수를 권한을 부여할 수는 `ALTER ANY USER` 권한. 예를 들어   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

이제 로그인 Jerry 수 로그인 이상 만들고 사용자 Jerry 수 있는 더 많은 사용자가 만들 합니다.


## <a name="granting-access-with-least-privileges"></a>최소 권한으로 액세스 권한 부여

사용자 데이터베이스에 연결 하는 데 첫 번째 사용자는 관리자 및 데이터베이스 소유자 계정 됩니다. 그러나 이러한 사용자가 모든는 데이터베이스에서 사용할 수 있는 권한입니다. 이것은 더 많은 사용 권한 보다 대부분의 사용자가 있어야 합니다. 

바로 시작 하는 때 기본 제공을 사용 하 여 몇 가지 일반적인 사용 권한 범주의 할당할 수 있습니다 *고정 데이터베이스 역할*합니다. 예를 들어는 `db_datareader` 고정된 데이터베이스 역할은 데이터베이스의 모든 테이블을 읽을 수 있지만 변경 하지 않습니다. 사용 하 여 고정된 데이터베이스 역할의 멤버 자격을 부여는 [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) 문. 다음 예제에서는 사용자를 추가 `Jerry` 에 `db_datareader` 고정된 데이터베이스 역할입니다.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

고정된 데이터베이스 역할의 목록을 보려면 참조 [데이터베이스 수준 역할](../relational-databases/security/authentication-access/database-level-roles.md)합니다.

(권장 사항) 데이터를 보다 정확 하 게 액세스를 구성 하려면 준비가 되 면 사용 하 여 사용자 고유의 사용자 정의 데이터베이스 역할을 만들 나중 [역할 만들기](../t-sql/statements/create-role-transact-sql.md) 문. 그런 다음 특정 세분화 된 사용 권한을 할당 하면 사용자 지정 역할입니다.

예를 들어 다음 문은 라는 데이터베이스 역할을 만듭니다 `Sales`, 부여는 `Sales` 그룹 참조, 업데이트 및 행을 삭제할 수 있는 권한을 `Orders` 테이블을 선택한 다음 사용자를 추가 `Jerry` 에 `Sales` 역할입니다.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

권한 시스템에 대 한 자세한 내용은 참조 [데이터베이스 엔진 권한 시작](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)합니다.


## <a name="configure-row-level-security"></a>행 수준 보안을 구성 합니다.  

[행 수준 보안](../relational-databases/security/row-level-security.md) 쿼리를 실행 하는 사용자에 따라 데이터베이스의 행에 대 한 액세스를 제한할 수 있습니다. 이 기능은 고객만 자신의 데이터를 액세스할 수 있도록 하거나 작업 자가 해당 부서에 관련 된 데이터에만 액세스할 수와 같은 시나리오에 유용 합니다.   

서로 다른 두 사용자가을 설정 하 여 워크 아래 단계 행 수준에 대 한 액세스는 `Sales.SalesOrderHeader` 테이블입니다. 

행 수준 보안을 테스트 하려면 두 개의 사용자 계정을 만듭니다.    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

읽기 액세스 권한을 부여는 `Sales.SalesOrderHeader` 두 사용자에 게 테이블:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
새 스키마 및 인라인 테이블 반환 함수를 만듭니다. 함수에 1을 반환 합니다.는 `SalesPersonID` 열 ID와 일치 한 `SalesPerson` 로그인 또는 쿼리를 실행 하는 사용자가 Manager 사용자 경우.   
   
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

필터 및 테이블에는 블록 조건자로 함수를 추가 하는 보안 정책을 만듭니다.  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

다음 쿼리를 실행 하는 `SalesOrderHeader` 각 사용자 테이블. 확인 `SalesPerson280` 의 95 하 고 자신의 판매 행만 봅니다는 `Manager` 테이블의 모든 행을 볼 수 있습니다.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
정책을 사용하지 않도록 보안 정책을 변경합니다.  이제 두 사용자가 모든 행을 액세스할 수 있습니다. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>동적 데이터 마스킹을 사용 하도록 설정

[동적 데이터 마스킹](../relational-databases/security/dynamic-data-masking.md) 완전히 또는 부분적으로 특정 열을 가장 하 여 응용 프로그램의 사용자에 게 중요 한 데이터의 노출을 제한할 수 있습니다. 

사용 하 여 프로그램 `ALTER TABLE` 문에 마스킹 함수를 추가 하는 `EmailAddress` 열에는 `Person.EmailAddress` 테이블: 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
새 사용자 만들기 `TestUser` 와 `SELECT` 테이블에 대 한 권한으로 쿼리를 실행 합니다 `TestUser` 마스크 된 데이터를 보려면:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
마스킹 함수에서 첫 번째 레코드에 전자 메일 주소 변경 되는지 확인 합니다.
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1. |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1. |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>투명한 데이터 암호화 사용

데이터베이스에 한 위협에는 하드 드라이브에서 데이터베이스 파일을 도용 합니다 누군가가 위험이 있습니다. 이 시스템에 대 한 액세스 권한 (예: 랩톱) 파일을 포함 하는 컴퓨터의 도용 또는 문제가 직원의 동작을 통해 가져오는 침입와 발생할 수 있습니다.

투명 한 데이터 암호화 (TDE)는 하드 드라이브에 저장 된 데이터 파일을 암호화 합니다. Master 데이터베이스는 SQL Server 데이터베이스 엔진에 암호화 키를 있으므로 데이터베이스 엔진 데이터를 조작할 수 있습니다. 키에 액세스 하지 않고 데이터베이스 파일을 읽을 수 없습니다. 높은 수준의 관리자 관리, 백업 하 고 데이터베이스를 이동할 수 있도록 하지만 된 선택한 사용자만 키를 다시 만들 수 있습니다. TDE를 구성 하는 경우는 `tempdb` 데이터베이스도 자동으로 암호화 됩니다. 

데이터베이스 엔진의 데이터를 읽을 수 있으므로 투명 한 데이터 암호화 직접 메모리를 읽을 하거나 관리자 계정을 통해 SQL Server에 액세스할 수 있는 컴퓨터의 관리자가 무단된 액세스 로부터 보호 하지 않습니다.

### <a name="configure-tde"></a>TDE를 구성

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

TDE를 제거 하려면 실행`ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

암호화 및 해독 작업은 SQL Server가 백그라운드 스레드로 예약 됩니다. 이 항목의 뒷부분에 나오는 카탈로그 뷰 및 동적 관리 뷰를 사용하여 이러한 작업의 상태를 볼 수 있습니다.   

>  [!WARNING]
>  TDE가 사용된 데이터베이스의 백업 파일도 데이터베이스 암호화 키를 사용하여 암호화됩니다. 따라서 이러한 백업 파일을 복원하려면 데이터베이스 암호화 키를 보호하는 인증서를 사용할 수 있어야 합니다. 즉, 데이터베이스 백업뿐만 아니라 데이터 손실을 방지하기 위해 서버 인증서의 백업도 유지 관리해야 합니다. 인증서를 더 이상 사용할 수 없을 경우 데이터 손실이 발생합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  

TDE에 대 한 자세한 내용은 참조 [투명 한 데이터 암호화 (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md)합니다.   


## <a name="configure-backup-encryption"></a>백업 암호화 구성
SQL Server에는 백업을 만드는 동안 데이터를 암호화 하는 기능. 암호화 알고리즘과 암호기 (인증서 또는 비대칭 키)를 지정 하 여 백업을 만들 때 암호화 된 백업 파일을 만들 수 있습니다.    
  
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

자세한 내용은 참조 [백업 암호화](../relational-databases/backup-restore/backup-encryption.md)합니다.


## <a name="next-steps"></a>다음 단계

SQL Server의 보안 기능에 대 한 자세한 내용은 참조 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대 한 보안 센터](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)합니다.
