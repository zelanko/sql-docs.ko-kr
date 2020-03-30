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
ms.openlocfilehash: bcf14745af6da26cc625e928d75f510e0da9a2e8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70030359"
---
# <a name="data-type-precedence-transact-sql"></a>데이터 형식 우선 순위(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md.md](../../includes/tsql-appliesto-ss2012-all-md.md)]

연산자가 데이터 형식이 다른 두 식을 결합할 경우 우선순위가 낮은 데이터 형식이 먼저 우선순위가 높은 데이터 형식으로 변환됩니다. 변환이 지원되는 암시적 변환이 아닌 경우 오류가 반환됩니다. 동일한 데이터 형식을 갖는 피연산자 식을 결합하는 연산자의 경우 연산 결과는 해당 데이터 형식이 됩니다.
  
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
  
## <a name="see-also"></a>참고 항목
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
