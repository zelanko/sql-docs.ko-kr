---
title: DATALENGTH (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: d8887c50cb482e27bce63e08aa18b8ca54616faa
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="datalength-transact-sql"></a>DATALENGTH(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

식을 표시하는 데 사용된 바이트 수를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>인수  
*expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 모든 데이터 형식의 합니다.
  
## <a name="return-types"></a>반환 형식
**bigint** 경우 *식* 입니다는 **varchar (max)**, **nvarchar (max)** 또는 **varbinary (max)** 데이터 형식입니다. 그렇지 않으면 **int**합니다.
  
## <a name="remarks"></a>주의  
DATALENGTH은 특히 유용 **varchar**, **varbinary**, **텍스트**, **이미지**, **nvarchar**, 및 **ntext** 이러한 데이터 형식은 가변 길이 데이터를 저장할 수 때문에 데이터 형식입니다.
  
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
  
## <a name="see-also"></a>참고 항목
[Len 함수 &#40; Transact SQL &#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[시스템 함수 &#40; Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  


