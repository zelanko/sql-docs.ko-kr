---
title: "데이터 형식 우선 순위 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- precedence [SQL Server]
- data types [SQL Server], converting
- data types [SQL Server], precedence
- converting data types [SQL Server], precedence
- precedence [SQL Server], data types
ms.assetid: f4c804ab-ed3f-43b1-a024-c9ac6944b66b
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f39337e00dfdbcd4a6bb01a00093a61f46a79fa
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-precedence-transact-sql"></a>데이터 형식 우선 순위 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

연산자로 데이터 형식이 다른 두 식을 결합할 경우 데이터 형식 우선 순위 규칙에 따라 우선 순위가 낮은 데이터 형식이 우선 순위가 높은 데이터 형식으로 변환됩니다. 이때 변환이 암시적으로 지원되지 않으면 오류가 반환됩니다. 피연산자 식이 같은 데이터 형식일 경우에는 연산 결과도 같은 데이터 형식이 됩니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 데이터 형식에 다음 우선 순위를 사용합니다.
  
1.  사용자 정의 데이터 형식(가장 높음)  
1.  **sql_variant**  
1.  **xml**  
1.  **datetimeoffset**  
1.  **datetime2**  
1.  **datetime**  
1.  **smalldatetime**  
1.  **date**  
1. **time**  
1. **float**  
1. **real**  
1. **decimal**  
1. **money**  
1. **smallmoney**  
1. **bigint**  
1. **int**  
1. **smallint**  
1. **tinyint**  
1. **bit**  
1. **ntext**  
1. **text**  
1. **image**  
1. **timestamp**  
1. **uniqueidentifier**  
1. **nvarchar** (포함 하 여 **nvarchar (max)** )  
1. **nchar**  
1. **varchar** (포함 하 여 **varchar (max)** )  
1. **char**  
1. **varbinary** (포함 하 여 **varbinary (max)** )  
1. **이진** (가장 낮음)  
  
## <a name="see-also"></a>참고 항목
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

