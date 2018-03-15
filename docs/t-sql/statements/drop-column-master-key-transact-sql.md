---
title: DROP COLUMN MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/20/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP COLUMN MASTER KEY
- DROP_COLUMN_MASTER_KEY_TSQL
- DROP COLUMN MASTER
- DROP_COLUMN_MASTER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_keys catalog view
ms.assetid: fd5e77c8-a3ae-4795-bb46-b322c0500041
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 207fd618b0381f69a74bee00bf92b7df248b8aed
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스에서 열 마스터 키를 삭제합니다. 메타데이터 작업입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP COLUMN MASTER KEY key_name;  
```  
  
## <a name="arguments"></a>인수  
 *key_name*  
 열 마스터 키의 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 열 암호화 키를 사용해 암호화된 열 암호화 키 값이 없는 경우 열 마스터 키를 삭제할 수 있습니다. 열 암호화 키 값을 삭제하려면 [DROP COLUMN ENCRYPTION KEY](../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 문을 사용하세요.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 **ALTER ANY COLUMN MASTER KEY** 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-column-master-key"></a>1. 열 마스터 키 삭제  
 다음 예에서는 `MyCMK`이라고 하는 열 마스터 키를 삭제합니다.  
  
```  
DROP COLUMN MASTER KEY MyCMK;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [CREATE COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)  
  
  
