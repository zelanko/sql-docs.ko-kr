---
title: ALTER MASTER KEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 638449f85daf7b13abc37c5750eb32ec5603d7ef
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-master-key-transact-sql"></a>ALTER MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

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
 암호 ='*암호*'  
 데이터베이스 마스터 키를 암호화하거나 암호 해독할 때 사용할 암호를 지정합니다. *암호* 의 인스턴스를 실행 하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="remarks"></a>주의  
 REGENERATE 옵션은 데이터베이스 마스터 키와 이 키가 보호하는 모든 키를 다시 만듭니다. 키는 먼저 이전 마스터 키로 암호 해독된 다음 새 마스터 키로 암호화됩니다. 마스터 키가 손상된 경우가 아니면 이 리소스를 많이 사용하는 작업은 사용량이 낮은 기간 동안에만 수행하도록 예약해야 합니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서는 AES 암호화 알고리즘을 사용하여 SMK(서비스 마스터 키) 및 DMK(데이터베이스 마스터 키)를 보호합니다. AES는 이전 버전에서 사용하는 3DES보다 최신 암호화 알고리즘입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]로 업그레이드한 후 SMK와 DMK를 다시 생성해야 마스터 키가 AES로 업그레이드됩니다. SMK를 다시 생성 하는 방법에 대 한 자세한 내용은 참조 [ALTER SERVICE MASTER key&#40; Transact SQL &#41; ](../../t-sql/statements/alter-service-master-key-transact-sql.md).  
  
 FORCE 옵션을 사용할 경우에는 마스터 키를 사용할 수 없거나 서버에서 모든 암호화된 개인 키의 암호를 해독할 수 없는 경우에도 키 다시 만들기 작업이 계속됩니다. 사용 하 여 마스터 키를 열 수 없는 경우는 [RESTORE MASTER KEY](../../t-sql/statements/restore-master-key-transact-sql.md) 백업에서 마스터 키를 복원 하는 문입니다. 마스터 키를 검색할 수 없거나 암호 해독에 실패한 경우에만 FORCE 옵션을 사용합니다. 검색할 수 없는 키로만 암호화된 정보는 손실됩니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 새 데이터베이스 마스터 키에 대 한 `AdventureWorksPDW2012` 하 고 다시 암호화 계층의 아래에 있는 키를 암호화 합니다.  
  
```  
USE master;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [MASTER key&#40; 열기 Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER key&#40; Transact SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER key&#40; Transact SQL &#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER key&#40; Transact SQL &#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [DROP MASTER key&#40; Transact SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  


