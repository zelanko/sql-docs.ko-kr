---
title: "집계 함수 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a97d68c641d2a3deb1d3fd3a674f65cafc3854c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions-transact-sql"></a>집계 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

집계 함수는 값 집합에 대한 계산을 수행하고 단일 값을 반환합니다. COUNT를 제외한 집계 함수는 Null 값을 무시합니다 집계 함수는 SELECT 문의 GROUP BY 절과 함께 사용하는 경우가 많습니다.
  
모든 집계 함수는 결정적입니다. 즉, 집계 함수는 특정 입력 값 집합을 사용하여 호출될 때 항상 동일한 값을 반환합니다. 함수 결정성에 대 한 자세한 내용은 참조 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)합니다. [OVER 절](../../t-sql/queries/select-over-clause-transact-sql.md) GROUPING 및 GROUPING_ID를 제외한 모든 집계 함수를 따를 수 있습니다.
  
집계 함수는 다음과 같은 식으로만 사용할 수 있습니다.
-   SELECT 문의 SELECT 목록(하위 쿼리 또는 외부 쿼리)  
-   HAVING 절  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)]에서는 다음 집계 함수를 제공합니다.
  
|||  
|-|-|  
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[MIN](../../t-sql/functions/min-transact-sql.md)|  
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[합계](../../t-sql/functions/sum-transact-sql.md)|  
|[개수](../../t-sql/functions/count-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|  
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|  
|[그룹화](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|  
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|  
|[최대](../../t-sql/functions/max-transact-sql.md)||  
  
## <a name="see-also"></a>참고 항목
[기본 제공 함수s&#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[절 &#40; 조치 Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

