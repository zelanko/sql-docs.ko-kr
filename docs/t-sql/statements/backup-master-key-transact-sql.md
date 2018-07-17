---
title: BACKUP MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BACKUP MASTER KEY
- DUMP_MASTER_KEY_TSQL
- BACKUP_MASTER_KEY_TSQL
- DUMP MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- BACKUP MASTER KEY statement
- exporting Database Master Keys
- encryption [SQL Server], Database Master Key
- cryptography [SQL Server], Database Master Key
- backing up master keys [SQL Server]
- database master key [SQL Server], exporting
ms.assetid: 0e25fe22-2536-4d7e-ba4a-1921e880f367
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 53de47b4c9b57ebdb6e77601c3600ddda4f16198
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37792134"
---
# <a name="backup-master-key-transact-sql"></a>BACKUP MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 마스터 키를 내보냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
BACKUP MASTER KEY TO FILE = 'path_to_file'   
    ENCRYPTION BY PASSWORD = 'password'  
```  
  
## <a name="arguments"></a>인수  
 FILE ='*path_to_file*'  
 마스터 키를 내보낼 파일에 대한 파일 이름을 포함한 전체 경로를 지정합니다. 이 경로는 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다.  
  
 PASSWORD ='*password*'  
 파일의 마스터 키를 암호화하는 데 사용되는 암호입니다. 이 암호의 복잡성을 확인해야 합니다. 자세한 내용은 [Password Policy](../../relational-databases/security/password-policy.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 마스터 키를 열어야 하기 때문에 백업하기 전에 암호를 해독해야 합니다. 서비스 마스터 키를 사용하여 암호화된 경우 마스터 키를 명시적으로 열 필요가 없습니다. 하지만 마스터 키가 암호로만 암호화된 경우 명시적으로 열어야 합니다.  
  
 마스터 키는 만들자 마자 백업하고 외부의 안전한 위치에 보관하는 것이 좋습니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 마스터 키의 백업을 만듭니다. 이 마스터 키는 서비스 마스터 키로 암호화되지 않았기 때문에 마스터 키를 열려면 암호를 지정해야 합니다.  
  
```  
USE AdventureWorks2012;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'sfj5300osdVdgwdfkli7';  
BACKUP MASTER KEY TO FILE = 'c:\temp\exportedmasterkey'   
    ENCRYPTION BY PASSWORD = 'sd092735kjn$&adsg';  
GO   
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
