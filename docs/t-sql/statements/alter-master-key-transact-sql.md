---
title: ALTER MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER MASTER KEY
- ALTER_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- ALTER MASTER KEY statement
- decryption [SQL Server], Database Master Key
- FORCE option
- encryption [SQL Server], Database Master Key
- database master key [SQL Server], modifying
- cryptography [SQL Server], Database Master Key
- modifying Database Master Key
- service master key [SQL Server], modifying
- DROP ENCRYPTION BY SERVICE MASTER KEY phrase
ms.assetid: 8ac501c3-4280-4d5b-b58a-1524fa715b50
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7190892a06eb7684b549e38d6cb417b8bddb6ff0
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361483"
---
# <a name="alter-master-key-transact-sql"></a>ALTER MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스 마스터 키의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Database
-- Note: DROP ENCRYPTION BY SERVICE MASTER KEY is not supported on Azure SQL Database.
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD ='password'<encryption_option> ::=  
    ADD ENCRYPTION BY SERVICE MASTER KEY   
    |   
    DROP ENCRYPTION BY SERVICE MASTER KEY  
```  
  
## <a name="arguments"></a>인수  
 PASSWORD ='*password*'  
 데이터베이스 마스터 키를 암호화하거나 암호 해독할 때 사용할 암호를 지정합니다. *password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다.  
  
## <a name="remarks"></a>Remarks  
 REGENERATE 옵션은 데이터베이스 마스터 키와 이 키가 보호하는 모든 키를 다시 만듭니다. 키는 먼저 이전 마스터 키로 암호 해독된 다음 새 마스터 키로 암호화됩니다. 마스터 키가 손상된 경우가 아니면 이 리소스를 많이 사용하는 작업은 사용량이 낮은 기간 동안에만 수행하도록 예약해야 합니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서는 AES 암호화 알고리즘을 사용하여 SMK(서비스 마스터 키) 및 DMK(데이터베이스 마스터 키)를 보호합니다. AES는 이전 버전에서 사용하는 3DES보다 최신 암호화 알고리즘입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 로 업그레이드한 후 SMK와 DMK를 다시 생성해야 마스터 키가 AES로 업그레이드됩니다. SMK를 다시 생성하는 방법은 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)를 참조하세요.  
  
 FORCE 옵션을 사용할 경우에는 마스터 키를 사용할 수 없거나 서버에서 모든 암호화된 개인 키의 암호를 해독할 수 없는 경우에도 키 다시 만들기 작업이 계속됩니다. 마스터 키를 열 수 없으면 [RESTORE MASTER KEY](../../t-sql/statements/restore-master-key-transact-sql.md) 문을 사용하여 백업에서 마스터 키를 복원합니다. 마스터 키를 검색할 수 없거나 암호 해독에 실패한 경우에만 FORCE 옵션을 사용합니다. 검색할 수 없는 키로만 암호화된 정보는 손실됩니다.  
  
 DROP ENCRYPTION BY SERVICE MASTER KEY 옵션은 서비스 마스터 키로 데이터베이스 마스터 키에 대한 암호화를 제거합니다.  
  
 ADD ENCRYPTION BY SERVICE MASTER KEY를 사용하면 마스터 키 복사본이 서비스 마스터 키를 사용하여 암호화되고 현재 데이터베이스와 master에 모두 저장됩니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CONTROL 권한이 필요합니다. 데이터베이스 마스터 키가 암호로 암호화된 경우 해당 암호도 알고 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks`에 대한 새 데이터베이스 마스터 키를 만들고 암호화 계층에서 아래에 있는 키를 다시 암호화합니다.  
  
```  
USE AdventureWorks2012;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `AdventureWorksPDW2012`에 대한 새 데이터베이스 마스터 키를 만들고 암호화 계층에서 아래에 있는 키를 다시 암호화합니다.  
  
```  
USE master;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

