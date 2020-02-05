---
title: IS_OBJECTSIGNED(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IS_OBJECTSIGNED
- IS_OBJECTSIGNED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IS_OBJECTSIGNED function
ms.assetid: afbc4f7f-8266-4ee6-9802-14a2dbe69ef6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 274e6128ba57a92f6f2e1e84e160424571742787
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71314608"
---
# <a name="is_objectsigned-transact-sql"></a>IS_OBJECTSIGNED(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  개체가 지정된 인증서 또는 비대칭 키로 서명되었는지를 나타냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
IS_OBJECTSIGNED (   
'OBJECT', @object_id, @class, @thumbprint  
  )   
```  
  
## <a name="arguments"></a>인수  
 **'OBJECT'**  
 보안 개체 클래스의 유형입니다.  
  
 *\@object_id*  
 테스트 중인 개체의 object_id입니다. *\@object_id*는 **int** 형식입니다.  
  
 *\@클래스*  
 개체의 클래스입니다.  
  
-   '인증서'  
  
-   '비대칭 키'  
  
 *\@클래스*는 **sysname**입니다.  
  
 *\@지문*  
 개체의 SHA 지문입니다. *\@지문*은 **varbinary(32)** 형식입니다.  
  
## <a name="returned-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>설명  
 IS_OBJECTSIGNED는 다음과 같은 값을 반환합니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|NULL|개체가 서명되지 않았거나 개체가 유효하지 않습니다.|  
|0|개체가 서명되었지만 서명이 유효하지 않습니다.|  
|1|개체가 서명되었습니다.|  
  
## <a name="permissions"></a>사용 권한  
 인증서 또는 비대칭 키에 대한 VIEW DEFINITION이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. 데이터베이스의 확장 속성 표시  
 다음 예에서는 **master** 데이터베이스의 spt_fallback_db 테이블이 스키마 서명 인증서로 서명되었는지를 테스트합니다.  
  
```  
USE master;  
-- Declare a variable to hold a thumbprint and an object name  
DECLARE @thumbprint varbinary(20), @objectname sysname;  
  
-- Populate the thumbprint variable with the thumbprint of   
-- the master database schema signing certificate  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%';  
  
-- Populate the object name variable with a table name in master  
SELECT @objectname = 'spt_fallback_db';  
  
-- Query to see if the table is signed by the thumbprint  
SELECT @objectname AS [object name],  
IS_OBJECTSIGNED(  
'OBJECT', OBJECT_ID(@objectname), 'certificate', @thumbprint  
) AS [Is the object signed?] ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.fn_check_object_signatures&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-check-object-signatures-transact-sql.md)  
  
  
