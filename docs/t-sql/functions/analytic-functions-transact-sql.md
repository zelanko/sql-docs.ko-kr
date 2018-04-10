---
title: 분석 함수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 60fbff84-673b-48ea-9254-6ecdad20e7fe
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 31f0f35840908b96ad9254c0e297cd55ad5b5226
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="analytic-functions-transact-sql"></a>분석 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

SQL Server는 다음과 같은 분석 함수를 지원합니다.
  
|||  
|-|-|  
|[CUME_DIST&#40;Transact-SQL&#41;](../../t-sql/functions/cume-dist-transact-sql.md)|[LEAD&#40;Transact-SQL&#41;](../../t-sql/functions/lead-transact-sql.md)|  
|[FIRST_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/first-value-transact-sql.md)|[PERCENTILE_CONT&#40;Transact-SQL&#41;](../../t-sql/functions/percentile-cont-transact-sql.md)|  
|[LAG&#40;Transact-SQL&#41;](../../t-sql/functions/lag-transact-sql.md)|[PERCENTILE_DISC&#40;Transact-SQL&#41;](../../t-sql/functions/percentile-disc-transact-sql.md)|  
|[LAST_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/last-value-transact-sql.md)|[PERCENT_RANK&#40;Transact-SQL&#41;](../../t-sql/functions/percent-rank-transact-sql.md)|  
  
분석 함수는 행 그룹을 기반으로 집계 값을 계산합니다. 그러나 집계 함수와 달리 분석 함수는 각 그룹에 대해 여러 행을 반환할 수 있습니다. 분석 함수를 사용하면 이동 평균, 누계, 백분율 또는 그룹 내 상위 N개 결과를 계산할 수 있습니다.
 
## <a name="see-also"></a>관련 항목:
[OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
