---
title: DATALENGTH(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 346b5aada1a16e84aa3e74019e83dd7a74d9914a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="datalength-transact-sql"></a>DATALENGTH(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

식을 표시하는 데 사용된 바이트 수를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>인수  
*expression*  
임의 데이터 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.
  
## <a name="return-types"></a>반환 형식
*식*이 **varchar(max)**, **nvarchar(max)** 또는 **varbinary(max)** 데이터 유형이면 **bigint**, 그렇지 않으면 **int**입니다.
  
## <a name="remarks"></a>Remarks  
DATALENGTH는 가변 길이 데이터를 저장할 수 있는 **varchar**, **varbinary**, **text**, **image**, **nvarchar** 및 **ntext** 데이터 형식에서 특히 유용합니다.
  
NULL의 DATALENGTH는 NULL입니다.
  
> [!NOTE]  
>  반환되는 값은 호환성 수준에 따라 달라질 수 있습니다. 호환성 수준에 대한 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
## <a name="examples"></a>예  
다음 예에서는 `Name` 테이블에서 `Product` 열의 길이를 찾아냅니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:
[LEN&#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  

