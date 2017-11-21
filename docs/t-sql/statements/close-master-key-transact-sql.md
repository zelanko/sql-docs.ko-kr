---
title: CLOSE MASTER KEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/15/2017
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
- CLOSE MASTER KEY
- CLOSE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- CLOSE MASTER KEY statement
- database master key [SQL Server], closing
- cryptography [SQL Server], Database Master Key
- closing Database Master Keys
ms.assetid: bb04ef7a-9f3a-437e-a6f9-ba0204082cb9
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e1337667bc7dd03d9943f7b7f76f8a313eeb125
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="close-master-key-transact-sql"></a>CLOSE MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스의 마스터 키를 닫습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CLOSE MASTER KEY  
```  
  
## <a name="arguments"></a>인수  
 인수가 필요하지 않습니다.  
  
## <a name="remarks"></a>주의  
 이 문은 OPEN MASTER KEY로 수행한 작업을 반대로 수행합니다. CLOSE MASTER KEY는 OPEN MASTER KEY 문을 사용하여 현재 세션에서 데이터베이스 마스터 키를 연 경우에만 성공합니다.  
  
## <a name="permissions"></a>Permissions  
 사용 권한이 필요 없습니다.  
  
## <a name="examples"></a>예  
  
```  
USE AdventureWorks2012;  
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```  
USE master;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO   
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [MASTER key&#40; 열기 Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


