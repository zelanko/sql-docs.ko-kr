---
title: "열 마스터 키 (Transact SQL) | Microsoft Docs"
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

  데이터베이스에서 열 마스터 키를 삭제합니다. 메타 데이터 작업입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP COLUMN MASTER KEY key_name;  
```  
  
## <a name="arguments"></a>인수  
 *key_name*  
 열 마스터 키의 이름입니다.  
  
## <a name="remarks"></a>주의  
 열 암호화 되지 않은 열 마스터 키로 암호화 된 키 값이 경우에 열 마스터 키를 삭제할 수 있습니다. 사용 하 여 열 암호화 키 값을 삭제 하려면는 [열 암호화 키 삭제](../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 문.  
  
## <a name="permissions"></a>Permissions  
 필요한 **ALTER ANY COLUMN MASTER KEY** 데이터베이스에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-column-master-key"></a>1. 열 마스터 키를 삭제 하는 중  
 다음 예에서는 라는 열 마스터 키를 삭제 `MyCMK`합니다.  
  
```  
DROP COLUMN MASTER KEY MyCMK;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [CREATE COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION key&#40; Transact SQL &#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)  
  
  
