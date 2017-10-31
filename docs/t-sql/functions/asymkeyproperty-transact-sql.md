---
title: ASYMKEYPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62ed19d07264d971045582c093a4c5ccdf6d8926
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

비대칭 키의 속성을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
ASYMKEYPROPERTY (Key_ID , 'algorithm_desc' | 'string_sid' | 'sid')  
```  
  
## <a name="arguments"></a>인수  
*Key_ID*  
데이터베이스에 있는 비대칭 키의 Key_ID입니다. 키 이름만 알고 있는 경우 Key_ID를 찾으려면 ASYMKEY_ID를 사용합니다. *Key_ID* 데이터 형식이 **int**합니다.
  
**'**algorithm_desc**'**  
출력에 비대칭 키의 알고리즘 설명이 반환되도록 지정합니다. EKM 모듈에서 생성된 비대칭 키에만 사용할 수 있습니다.
  
**'**string_sid**'**  
출력에 비대칭 키의 SID를 반환 하도록 지정 **nvarchar()** 형식입니다.
  
**'**sid**'**  
출력에 비대칭 키의 SID가 이진 형식으로 반환되도록 지정합니다.
  
## <a name="return-types"></a>반환 형식  
**sql_variant**
  
## <a name="permissions"></a>Permissions  
비대칭 키에 대한 일부 사용 권한이 필요하며 비대칭 키에 대한 호출자의 VIEW 권한이 거부되지 않아야 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 Key_ID가 256인 비대칭 키의 속성을 반환합니다.
  
```sql
SELECT   
ASYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm,  
ASYMKEYPROPERTY(256, 'string_sid') AS String_SID,  
ASYMKEYPROPERTY(256, 'sid') AS SID ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC key&#40; Transact SQL &#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC key&#40; Transact SQL &#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY&#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40; Transact SQL &#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[sys.asymmetric_keys &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEY_ID &#40; Transact SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
[SYMKEYPROPERTY &#40; Transact SQL &#41;](../../t-sql/functions/symkeyproperty-transact-sql.md)
  
  

