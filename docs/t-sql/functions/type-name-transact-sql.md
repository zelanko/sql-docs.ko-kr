---
title: TYPE_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TYPE_NAME_TSQL
- TYPE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- names [SQL Server], data types
- unqualified type names
- type names [SQL Server]
- data types [SQL Server], names
- TYPE_NAME function
ms.assetid: e4075a2e-5f70-440f-986b-9ec8434e07c1
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3d60bec3a21bb5b1127b0f18977d3485979f20b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="typename-transact-sql"></a>TYPE_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 형식 ID의 정규화되지 않은 형식 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
TYPE_NAME ( type_id )   
```  
  
## <a name="arguments"></a>인수  
 *type_id*  
 사용될 형식의 ID입니다. *type_id* 는 **int**, 하면 호출자가 액세스할 수 있는 권한이 있는 모든 스키마의 형식을 참조할 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **sysname**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자는 소유하고 있거나 사용 권한을 부여받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 TYPE_NAME과 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>주의  
 TYPE_NAME 돌아갑니다 인 경우 NULL *type_id* 유효 하지 호출자에 게 유형을 참조할 수 있는 충분 한 사용 권한을 없는 합니다.  
  
 TYPE_NAME은 시스템 데이터 형식에 사용할 수 있으며 사용자 정의 데이터 형식에도 사용할 수 있습니다. 형식은 모든 스키마에 포함될 수 있지만 항상 정규화되지 않은 형식 이름이 반환됩니다. 즉, 이름이 없는 *스키마***합니다.** 찾습니다.  
  
 시스템 함수는 선택 목록, WHERE 절 및 식이 허용되는 모든 곳에서 사용될 수 있습니다. 자세한 내용은 참조 [식 &#40; Transact SQL &#41; ](../../t-sql/language-elements/expressions-transact-sql.md) 및 [여기서 &#40; Transact SQL &#41; ](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `Vendor` 테이블에 있는 각 열의 개체 이름, 열 이름 및 형식 이름을 반환합니다.  
  
```  
SELECT o.name AS obj_name, c.name AS col_name,  
       TYPE_NAME(c.user_type_id) AS type_name  
FROM sys.objects AS o   
JOIN sys.columns AS c  ON o.object_id = c.object_id  
WHERE o.name = 'Vendor'  
ORDER BY col_name;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
obj_name        col_name                  type_name
--------------- ------------------------ --------------
Vendor          AccountNumber            AccountNumber
Vendor          ActiveFlag               Flag
Vendor          BusinessEntityID         int
Vendor          CreditRating             tinyint
Vendor          ModifiedDate             datetime
Vendor          Name                     Name
Vendor          PreferredVendorStatus    Flag
Vendor          PurchasingWebServiceURL  nvarchar

(8 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 반환 된 `TYPE ID` id 가진 데이터 형식에 대 한 `1`합니다.  
  
```  
SELECT TYPE_NAME(36) AS Type36, TYPE_NAME(239) AS Type239;  
GO  
```  
  
 형식의 목록, sys.types를 쿼리 합니다.  
  
```  
SELECT * FROM sys.types;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [TYPE_ID &#40; Transact SQL &#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPEPROPERTY &#40; Transact SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
  
  


