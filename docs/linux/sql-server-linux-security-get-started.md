---
title: Linux에서 SQL Server 보안 시작
description: 추가로 조사할 영역에 대한 아이디어를 얻을 수 있도록 SQL Server on Linux의 보안 기능을 살펴봅니다.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 4a9137ad71947d222d246df046c6ab573fb4500d
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115816"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>SQL Server on Linux의 보안 기능 연습

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

SQL Server를 처음 사용하는 Linux 사용자인 경우 다음 작업에서 몇 가지 보안 작업을 안내합니다. 이 보안 작업은 Linux에 고유하거나 특정하지 않으며 추가로 조사할 영역에 대한 아이디어를 제공하는 데 도움이 됩니다. 각 예제에서는 해당 영역의 자세한 설명서의 링크가 제공됩니다.

> [!NOTE]
>  다음 예제에서는 **AdventureWorks2014** 샘플 데이터베이스를 사용합니다. 이 샘플 데이터베이스를 구하여 설치하는 방법에 대한 지침은 [Windows에서 Linux로 SQL Server 데이터베이스 복원](sql-server-linux-migrate-restore-database.md)을 참조하세요.


## <a name="create-a-login-and-a-database-user"></a>로그인 및 데이터베이스 사용자 만들기 

[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) 문을 통해 master 데이터베이스에서 로그인을 만들어 SQL Server에 대한 액세스 권한을 다른 사용자에게 부여합니다. 예를 들면 다음과 같습니다.

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

나중에 다른 로그인에 `ALTER ANY LOGIN` 권한을 부여하여 추가 로그인을 만들 권한을 부여할 수 있습니다. 데이터베이스 내에서 다른 사용자에게 `ALTER ANY USER` 권한을 부여하여 추가 사용자를 만들 권한을 부여할 수 있습니다. 예를 들면 다음과 같습니다.   

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

처음 시작하는 경우 기본 제공 ‘고정 데이터베이스 역할’을 사용하여 몇 가지 일반적인 권한 범주를 할당할 수 있습니다. 예를 들어 `db_datareader` 고정 데이터베이스 역할은 데이터베이스의 모든 테이블을 읽을 수 있지만 변경하지는 않습니다. [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) 문을 사용하여 고정 데이터베이스 역할의 멤버 자격을 부여합니다. 다음 예제에서는 `db_datareader` 고정 데이터베이스 역할에 사용자 `Jerry`를 추가합니다.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

고정 데이터베이스 역할 목록을 보려면 [데이터베이스 수준 역할](../relational-databases/security/authentication-access/database-level-roles.md)을 참조하세요.

나중에 데이터에 대한 보다 정확한 액세스를 구성할 준비가 되면(권장됨) [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) 문을 사용하여 사용자 정의 데이터베이스 역할을 만듭니다. 그런 다음, 사용자 지정 역할에 특정 세분화된 권한을 할당합니다.

예를 들어 다음 문은 `Sales`라는 데이터베이스 역할을 만들고, `Orders` 테이블의 행을 표시, 업데이트 및 삭제하는 기능을 `Sales` 그룹에 부여하고, 사용자 `Jerry`를 `Sales` 역할에 추가합니다.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```

권한 시스템에 대한 자세한 내용은 [데이터베이스 엔진 권한 시작](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을 참조하세요.


## <a name="configure-row-level-security"></a>행 수준 보안 구성  

[행 수준 보안](../relational-databases/security/row-level-security.md)을 사용하면 쿼리를 실행하는 사용자를 기반으로 데이터베이스의 행에 대한 액세스를 제한할 수 있습니다. 이 기능은 고객이 자신의 데이터에만 액세스할 수 있도록 하거나 작업자가 소속 부서와 관련된 데이터에만 액세스할 수 있도록 하는 시나리오에 유용합니다.   

다음 단계에서는 `Sales.SalesOrderHeader` 테이블에 대한 행 수준 액세스 권한이 서로 다른 두 사용자를 설정하는 방법을 안내합니다. 

행 수준 보안을 테스트할 사용자 계정을 두 개 만듭니다.    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```

두 명의 사용자에게 `Sales.SalesOrderHeader` 테이블에 대한 읽기 액세스 권한을 부여합니다.    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;
```
   
새 스키마 및 인라인 테이블 반환 함수를 만듭니다. 이 함수는 `SalesPersonID` 열의 행이 `SalesPerson` 로그인의 ID와 일치하거나 쿼리를 실행하는 사용자가 Manager 사용자인 경우 1을 반환합니다.   
   
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

테이블에서 필터 및 차단 조건자로 이 함수를 추가하는 보안 정책을 만듭니다.  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

다음을 실행하여 `SalesOrderHeader` 테이블을 각 사용자로 쿼리합니다. `SalesPerson280`은 자신의 판매에서 95개의 행만 보고 `Manager`는 테이블에서 모든 행을 볼 수 있는지 확인합니다.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
정책을 사용하지 않도록 보안 정책을 변경합니다.  이제 두 사용자 모두 모든 행에 액세스할 수 있습니다. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>동적 데이터 마스킹 사용

[동적 데이터 마스킹](../relational-databases/security/dynamic-data-masking.md)을 사용하면 특정 열을 완전히 또는 부분적으로 마스킹하여 중요한 데이터가 애플리케이션 사용자에게 노출되는 것을 제한할 수 있습니다. 

`ALTER TABLE` 문을 사용하여 `Person.EmailAddress` 테이블의 `EmailAddress` 열에 마스킹 함수를 추가합니다. 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
테이블에 대한 `SELECT` 권한이 있는 새 사용자 `TestUser`를 만든 다음 `TestUser`로 쿼리를 실행하여 마스킹된 데이터를 봅니다.   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
마스킹 함수가 첫 번째 레코드에 있는 이메일 주소를 변경하는지 확인합니다.
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>투명한 데이터 암호화 활성화

데이터베이스에 대한 한 가지 위협은 하드 드라이브에서 데이터베이스 파일이 도난당할 위험입니다. 이것은 문제 직원의 행동이나 파일이 들어 있는 컴퓨터(랩톱 등) 도난에 의해 시스템에 대한 관리자 액세스 권한을 획득한 침입이 있는 경우 발생할 수 있습니다.

TDE(투명한 데이터 암호화)는 하드 드라이브에 저장되어 있는 데이터 파일을 암호화합니다. SQL Server 데이터베이스 엔진의 master 데이터베이스에는 암호화 키가 있으므로 데이터베이스 엔진이 데이터를 조작할 수 있습니다. 키에 대한 액세스 권한이 없으면 데이터베이스 파일을 읽을 수 없습니다. 고급 관리자는 키를 관리 및 백업하고 다시 만들 수 있으므로 데이터베이스를 이동할 수 있지만 선택된 사용자만 가능합니다. TDE를 구성하면 `tempdb` 데이터베이스도 자동으로 암호화됩니다. 

데이터베이스 엔진은 데이터를 읽을 수 있으므로 투명한 데이터 암호화는 메모리를 직접 읽을 수 있거나 관리자 계정을 통해 SQL Server에 액세스할 수 있는 컴퓨터의 관리자에 의한 무단 액세스로부터는 보호하지 않습니다.

### <a name="configure-tde"></a>TDE 구성

- 마스터 키 만들기
- 마스터 키로 보호되는 인증서를 만들거나 얻기
- 데이터베이스 암호화 키를 만들고 인증서로 키 보호
- 암호화를 사용하도록 데이터베이스 설정

TDE를 구성하려면 master 데이터베이스에 대한 `CONTROL` 권한 및 사용자 데이터베이스에 대한 `CONTROL` 권한이 필요합니다. 일반적으로 관리자가 TDE를 구성합니다. 

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

TDE를 제거하려면 `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`를 실행합니다.   

암호화 및 암호 해독 작업은 SQL Server에 의해 백그라운드 스레드로 예약됩니다. 이 항목의 뒷부분에 나오는 카탈로그 뷰 및 동적 관리 뷰를 사용하여 이러한 작업의 상태를 볼 수 있습니다.   

> [!WARNING]
>  TDE가 사용된 데이터베이스의 백업 파일도 데이터베이스 암호화 키를 사용하여 암호화됩니다. 따라서 이러한 백업 파일을 복원하려면 데이터베이스 암호화 키를 보호하는 인증서를 사용할 수 있어야 합니다. 즉, 데이터베이스 백업뿐만 아니라 데이터 손실을 방지하기 위해 서버 인증서의 백업도 유지 관리해야 합니다. 인증서를 더 이상 사용할 수 없을 경우 데이터 손실이 발생합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  

TDE에 대한 자세한 내용은 [TDE(투명한 데이터 암호화)](../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요.   


## <a name="configure-backup-encryption"></a>백업 암호화 구성
SQL Server에는 백업을 만드는 동안 데이터를 암호화하는 기능이 있습니다. 백업을 만들 때 암호화 알고리즘과 암호기(인증서 또는 비대칭 키)를 지정하여 암호화된 백업 파일을 만들 수 있습니다.    
  
> [!WARNING]
> 인증서나 비대칭 키를 백업하는 것이 매우 중요하며, 이때 가급적이면 인증서나 비대칭 키를 사용하여 암호화한 백업 파일과 다른 위치에 백업하는 것이 좋습니다. 인증서나 비대칭 키가 없으면 백업을 복원할 수 없으므로 백업 파일을 사용할 수 없게 됩니다. 
 
 
다음 예에서는 인증서를 만든 다음 인증서로 보호되는 백업을 만듭니다.

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

자세한 내용은 [Backup 암호화](../relational-databases/backup-restore/backup-encryption.md)를 참조하세요.


## <a name="next-steps"></a>다음 단계

SQL Server의 보안 기능에 대한 자세한 내용은 [SQL Server 데이터베이스 엔진 및 Azure SQL Database 보안 센터](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)를 참조하세요.