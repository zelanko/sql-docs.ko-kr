---
title: SYMKEYPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYMKEYPROPERTY_TSQL
- SYMKEYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- SYMKEYPROPERTY
ms.assetid: 3d1f7075-3a3c-4660-8cd0-ed938b86fecd
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 12eaae508f3e6874e02e67ef7ece84da070bbb28
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="symkeyproperty-transact-sql"></a>SYMKEYPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  EKM 모듈에서 생성된 대칭 키의 알고리즘을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SYMKEYPROPERTY ( Key_ID , 'algorithm_desc' | 'string_sid' | 'sid' )  
```  
  
## <a name="arguments"></a>인수  
 *Key_ID*  
 데이터베이스에 있는 대칭 키의 Key_ID입니다. 키 이름만 알고 있는 경우 Key_ID를 찾으려면 SYMKEY_ID를 사용합니다. *Key_ID* 데이터 형식이 **int**합니다.  
  
 **'**algorithm_desc**'**  
 출력에 대칭 키의 알고리즘 설명이 반환되도록 지정합니다. EKM 모듈에서 생성된 대칭 키에만 사용할 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **sql_variant**  
  
## <a name="permissions"></a>Permissions  
 대칭 키에 대한 일부 사용 권한이 필요하며 대칭 키에 대한 호출자의 VIEW 권한이 거부되지 않아야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Key_ID가 256인 대칭 키의 알고리즘을 반환합니다.  
  
```  
SELECT SYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ASYMKEY_ID &#40; Transact SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [ALTER SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.symmetric_keys &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [KEY_ID &#40; Transact SQL &#41;](../../t-sql/functions/key-id-transact-sql.md)   
 [ASYMKEYPROPERTY &#40; Transact SQL &#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
  
  
