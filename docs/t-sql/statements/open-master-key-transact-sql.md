---
title: OPEN MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPEN MASTER KEY DECRYPTION BY PASSWORD
- OPEN_MASTER_KEY_DECRYPTION_BY_PASSWORD_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- OPEN_MASTER_KEY_TSQL
- MASTER KEY DECRYPTION
- OPEN MASTER KEY
- MASTER_KEY_DECRYPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- opening Database Master Keys
- encryption [SQL Server], Database Master Key
- cryptography [SQL Server], Database Master Key
- master key decryption
- OPEN MASTER KEY statement
- database master key [SQL Server], opening
ms.assetid: 1674753e-ca1e-4913-9ba4-b442e7106121
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 36db19a5eec90bad3b52542e0141200949fdcf5b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="open-master-key-transact-sql"></a>OPEN MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스의 데이터베이스 마스터 키를 엽니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>인수  
 '*password*'  
 데이터베이스 마스터 키를 암호화할 때 사용한 암호입니다.  
  
## <a name="remarks"></a>Remarks  
 서비스 마스터 키를 사용하여 암호화한 데이터베이스 마스터 키의 경우 해독 또는 암호화를 위해 필요할 때 자동으로 열립니다. 이 경우에는 **OPEN MASTER KEY** 문을 사용할 필요가 없습니다.  
  
 데이터베이스가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 처음으로 연결되거나 복원될 때 데이터베이스 마스터 키(서비스 마스터 키로 암호화됨)의 복사본은 서버에 아직 저장되지 않은 상태입니다. 데이터베이스 마스터 키를 암호 해독하려면 **OPEN MASTER KEY** 문을 사용해야 합니다. DMK를 암호 해독한 후에는 **ALTER MASTER KEY REGENERATE** 문을 사용하여 SMK(서비스 마스터 키)로 암호화된 DMK의 복사본을 서버에 프로비전함으로써 앞으로 자동 암호 해독을 사용하도록 설정할 수 있습니다. 데이터베이스가 이전 버전에서 업그레이드되지 않은 경우에는 DMK를 다시 생성해야 최신 AES 알고리즘을 사용할 수 있습니다. DMK를 다시 생성하는 방법은 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 데 소요되는 시간은 DMK에서 보호하는 개체 수에 따라 달라집니다. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 작업은 한 번만 필요하며 키 회전 전략의 일부로 이후에 수행하는 다시 생성 작업에 영향을 주지 않습니다.  
  
 ALTER MASTER KEY 문에 DROP ENCRYPTION BY SERVICE MASTER KEY 옵션을 사용하면 특정 데이터베이스의 데이터베이스 마스터 키를 자동 키 관리에서 제외할 수 있습니다. 이후부터 해당 데이터베이스 마스터 키는 암호를 사용하여 명시적으로 열어야 합니다.  
  
 데이터베이스 마스터 키를 명시적으로 연 트랜잭션이 롤백되면 이 키는 열린 상태로 남게 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 암호로 암호화된 `AdventureWorks2012` 데이터베이스의 데이터베이스 마스터 키를 엽니다.  
  
```  
USE AdventureWorks2012;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 암호로 암호화된 데이터베이스 마스터 키를 엽니다.  
  
```  
USE master;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO  
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

