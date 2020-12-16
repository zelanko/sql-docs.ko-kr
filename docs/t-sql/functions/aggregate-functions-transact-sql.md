---
description: 집계 함수(Transact-SQL)
title: 집계 함수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f2e6bc0650beed914c300e0a3fd021df7dbd626
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472134"
---
# <a name="aggregate-functions-transact-sql"></a>집계 함수(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

집계 함수는 값 집합에 대한 계산을 수행하고 단일 값을 반환합니다. `COUNT(*)`를 제외한 집계 함수는 Null 값을 무시합니다 집계 함수는 SELECT 문의 GROUP BY 절과 함께 사용되는 경우가 많습니다.
  
모든 집계 함수는 결정적입니다. 즉, 집계 함수는 특정 입력 값 집합을 사용하여 호출되는 경우 호출될 때마다 동일한 값을 반환합니다. 함수 결정성에 대한 자세한 내용은 [결정적 함수 및 비결정적 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요. [OVER 절](../../t-sql/queries/select-over-clause-transact-sql.md)은 STRING_AGG, GROUPING 또는 GROUPING_ID 함수를 제외한 모든 집계 함수에서 사용할 수 있습니다.
  
다음과 같은 경우에만 집계 함수를 식으로 사용합니다.
-   SELECT 문의 SELECT 목록(하위 쿼리 또는 외부 쿼리)  
-   HAVING 절  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)]에서는 다음 집계 함수를 제공합니다.

- [APPROX_COUNT_DISTINCT](../../t-sql/functions/approx-count-distinct-transact-sql.md)
- [AVG](../../t-sql/functions/avg-transact-sql.md)
- [CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)
- [COUNT](../../t-sql/functions/count-transact-sql.md)
- [COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)
- [GROUPING](../../t-sql/functions/grouping-transact-sql.md)
- [GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)
- [MAX](../../t-sql/functions/max-transact-sql.md)
- [MIN](../../t-sql/functions/min-transact-sql.md)
- [STDEV](../../t-sql/functions/stdev-transact-sql.md)
- [STDEVP](../../t-sql/functions/stdevp-transact-sql.md)
- [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md)
- [SUM](../../t-sql/functions/sum-transact-sql.md)
- [VAR](../../t-sql/functions/var-transact-sql.md)
- [VARP](../../t-sql/functions/varp-transact-sql.md)
  
## <a name="see-also"></a>참고 항목
[기본 제공 함수s&#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
