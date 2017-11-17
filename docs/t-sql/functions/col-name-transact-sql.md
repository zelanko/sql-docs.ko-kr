---
title: COL_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COL_NAME
- COL_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- COL_NAME function
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 214144ab-f2bc-4052-83cf-caf0a85c4cc6
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: c697b619907bb3d80fbbff800b2ac29ef574af8d
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="colname-transact-sql"></a>COL_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정된 테이블 ID와 열 ID에서 열의 이름을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COL_NAME ( table_id , column_id )  
```  
  
## <a name="arguments"></a>인수  
*table_id*  
열이 포함된 테이블의 ID입니다. *table_id* 유형의 **int**합니다.
  
*column_id*  
열의 ID입니다. *column_id* 매개 변수는 형식 **int**합니다.
  
## <a name="return-types"></a>반환 형식
**sysname**
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.
  
사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 COL_NAME과 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.
  
## <a name="remarks"></a>주의  
*table_id* 및 *column_id* 매개 변수를 합치면 열 이름 문자열입니다.
  
테이블 및 열 식별 번호를 구입에 대 한 자세한 내용은 참조 [OBJECT_ID &#40; Transact SQL &#41; ](../../t-sql/functions/object-id-transact-sql.md).
  
## <a name="examples"></a>예  
다음 예제에서는 샘플의 첫 번째 열의 이름을 반환 `Employee` 테이블입니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 1) AS FirstColumnName,  
COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 2) AS SecondColumnName;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
ColumnName          
------------   
BusinessEntityID  
```  
  
## <a name="see-also"></a>참고 항목
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COLUMNPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
[COL_LENGTH &#40; Transact SQL &#41;](../../t-sql/functions/col-length-transact-sql.md)
  
  


