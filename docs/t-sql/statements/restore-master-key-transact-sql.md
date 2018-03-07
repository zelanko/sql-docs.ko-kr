---
title: RESTORE MASTER KEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE_MASTER_KEY_TSQL
- RESTORE MASTER KEY
- LOAD_MASTER_KEY_TSQL
- LOAD MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- database master key [SQL Server], importing
- encryption [SQL Server], Database Master Key
- copying Database Master Keys
- importing Database Master Keys
- cryptography [SQL Server], Database Master Key
- transferring Database Master Keys
- RESTORE MASTER KEY statement
ms.assetid: 70ceb951-31a2-4fc4-a0c1-e6c18eeb3ae7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 63c0d492da379f3cb0d982e5f35a2a110a3a6dda
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="restore-master-key-transact-sql"></a>RESTORE MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  백업 파일로부터 데이터베이스 마스터 키를 가져옵니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
RESTORE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password'  
    ENCRYPTION BY PASSWORD = 'password'  
    [ FORCE ]  
```  
  
## <a name="arguments"></a>인수  
 파일 ='*path_to_file*'  
 저장된 데이터베이스 마스터 키에 대해 파일 이름을 포함한 전체 경로를 지정합니다. *path_to_file* 로컬 경로 또는 UNC 경로를 네트워크 위치 일 수 있습니다.  
  
 DECRYPTION BY PASSWORD ='*암호*'  
 파일로부터 가져올 데이터베이스 마스터 키의 암호를 해독하는 데 필요한 암호를 지정합니다.  
  
 ENCRYPTION BY PASSWORD ='*암호*'  
 데이터베이스 마스터 키를 데이터베이스에 로드한 다음 암호화하는 데 사용되는 암호를 지정합니다.  
  
 FORCE  
 현재 데이터베이스 마스터 키가 열려 있지 않거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 이 키로 암호화된 일부 개인 키의 암호를 해독할 수 없는 경우에도 RESTORE 프로세스가 계속되도록 지정합니다.  
  
## <a name="remarks"></a>주의  
 마스터 키가 복원되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 현재 사용 중인 마스터 키로 암호화된 모든 키의 암호를 해독한 다음 복원된 마스터 키를 사용하여 이러한 키를 암호화합니다. 이 리소스를 많이 사용하는 작업은 사용량이 낮은 기간 동안에만 수행하도록 예약해야 합니다. 현재 데이터베이스 마스터 키가 열려 있지 않거나 열 수 없는 경우 또는 이 키를 사용하여 암호화된 일부 키의 암호를 해독할 수 없는 경우 복원 작업이 실패합니다.  
  
 마스터 키를 검색할 수 없거나 암호 해독에 실패한 경우에만 FORCE 옵션을 사용합니다. 검색할 수 없는 키로만 암호화된 정보는 손실됩니다.  
  
 서비스 마스터 키로 마스터 키가 암호화된 경우 복원된 마스터 키는 서비스 마스터 키로도 암호화할 수 있습니다.  
  
 현재 데이터베이스에 마스터 키가 없는 경우 RESTORE MASTER KEY가 마스터 키를 만듭니다. 새 마스터 키는 서비스 마스터 키로 자동으로 암호화되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 데이터베이스의 데이터베이스 마스터 키를 복원합니다.  
  
```  
USE AdventureWorks2012;  
RESTORE MASTER KEY   
    FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
    ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
