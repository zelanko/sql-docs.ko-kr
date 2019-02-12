---
title: 데이터 형식 우선 순위(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6bd65fe0ef44b672e689aebd99b5f166ce562d23
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020307"
---
# <a name="data-type-precedence-transact-sql"></a>데이터 형식 우선 순위(Transact-SQL)
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
1. **nvarchar**(**nvarchar(max)** 포함)  
1. **nchar**  
1. **varchar** (**varchar(max)** 포함)  
1. **char**  
1. **varbinary** (**varbinary(max)** 포함)  
1. **binary**(가장 낮음)  
  
## <a name="see-also"></a>관련 항목:
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
