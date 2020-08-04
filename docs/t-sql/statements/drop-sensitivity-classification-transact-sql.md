---
title: DROP SENSITIVITY CLASSIFICATION(Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.author: giladm
author: giladmit
f1_keywords:
- DROP SENSITIVITY CLASSIFICATION
- DROP_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SENSITIVITY CLASSIFICATION statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d70e4a10601ab7c9171ddccf41a9ab9e5b2395c7
ms.sourcegitcommit: bc10ec0be5ddfc5f0bc220a9ac36c77dd6b80f1d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544323"
---
# <a name="drop-sensitivity-classification-transact-sql"></a>DROP SENSITIVITY CLASSIFICATION(Transact-SQL)
[!INCLUDE [asdb-asdbmi-asa](../../includes/applies-to-version/asdb-asdbmi-asa.md)]

하나 이상의 데이터베이스 열에서 민감도 분류 메타데이터를 삭제합니다.

## <a name="syntax"></a>구문

```syntaxsql
DROP SENSITIVITY CLASSIFICATION FROM
    <object_name> [, ...n ]

<object_name> ::=
{
    [schema_name.]table_name.column_name
}
```  

## <a name="arguments"></a>인수  

*object_name*([schema_name.]table_name.column_name)

분류를 제거할 데이터베이스 열의 이름입니다. 현재는 열 분류만 지원됩니다.
    - *schema_name*(선택 사항) - 분류된 열이 속한 스키마의 이름입니다.
    - *table_name* - 분류된 열이 속한 테이블의 이름입니다.
    - *column_name* - 분류를 삭제할 열의 이름입니다.

## <a name="remarks"></a>설명  

- 여러 개체 분류는 단일 'DROP SENSITIVITY CLASSIFICATION' 문을 사용하여 삭제할 수 있습니다.

## <a name="permissions"></a>사용 권한  

ALTER ANY SENSITIVITY CLASSIFICATION 권한이 필요합니다. ALTER ANY SENSITIVITY CLASSIFICATION은 데이터베이스 권한 ALTER 또는 서버 권한 CONTROL SERVER에 포함됩니다.


## <a name="examples"></a>예  


### <a name="a-dropping-classification-from-a-single-column"></a>A. 단일 열에서 분류 삭제

다음 예제에서는 `dbo.sales.price` 열에서 분류를 제거합니다.  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price
```

### <a name="b-dropping-classification-from-multiple-columns"></a>B. 여러 열에서 분류 삭제

다음 예제에서는 `dbo.sales.price`, `dbo.sales.discount` 및 `SalesLT.Customer.Phone` 열에서 분류를 제거합니다.  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price, dbo.sales.discount, SalesLT.Customer.Phone  
```

## <a name="see-also"></a>참고 항목  

[ADD SENSITIVITY CLASSIFICATION(Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications(Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[SQL Information Protection 시작](https://aka.ms/sqlip)
