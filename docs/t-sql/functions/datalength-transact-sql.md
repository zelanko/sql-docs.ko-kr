---
description: DATALENGTH(Transact-SQL)
title: DATALENGTH(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2bb43434dd528a7937f854ce287953f748d50076
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422817"
---
# <a name="datalength-transact-sql"></a>DATALENGTH(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수에서는 식을 표시하는 데 사용된 바이트 수를 반환합니다.

> [!NOTE]
> 문자열 식의 문자 수를 반환하려면 [LEN](../../t-sql/functions/len-transact-sql.md) 함수를 사용합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
DATALENGTH ( expression )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*expression*  
임의 데이터 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.
  
## <a name="return-types"></a>반환 형식
*expression*의 데이터 형식이 **nvarchar(max)**, **varbinary(max)** 또는 **varchar(max)** 이면 **bigint**이고, 그렇지 않으면 **int**입니다.
  
## <a name="remarks"></a>설명  
`DATALENGTH`는 다음과 같이 가변 길이 데이터를 저장할 수 있는 데이터 형식과 함께 사용할 때 매우 유용합니다.
- **image**
- **ntext**
- **nvarchar**
- **text**
- **varbinary**
- **varchar**
  
`DATALENGTH`는 NULL 값에 대해 NULL을 반환합니다.
  
> [!NOTE]  
> 반환되는 값은 호환성 수준에 따라 달라질 수 있습니다. 호환성 수준에 대한 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  

> [!NOTE]
> 지정된 문자열 식으로 인코딩된 문자 수를 반환하려면 [LEN](../../t-sql/functions/len-transact-sql.md)을 사용하고, 지정된 문자열 식의 크기(바이트)를 반환하려면 [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md)를 사용합니다. 이러한 출력은 열에 사용되는 인코딩 유형 및 데이터 형식에 따라 다를 수 있습니다. 서로 다른 인코딩 유형의 스토리지 차이점에 대해 자세히 알아보려면 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.

## <a name="examples"></a>예  
이 예에서는 `Name` 테이블에서 `Product` 열의 길이를 찾아냅니다.
  
```sql
USE AdventureWorks2016  
GO
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[LEN&#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)
