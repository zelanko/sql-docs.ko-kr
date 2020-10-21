---
description: DBCC SHOWRESULTCACHESPACEUSED(Transact-SQL)
title: DBCC SHOWRESULTCACHESPACEUSED(Transact-SQL)
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 3bf7994b1b7091bb95800ab1d8e3034f4bafef76
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037746"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED(Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스에 대한 스토리지 공간 사용 결과 세트 캐싱을 보여 줍니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="remarks"></a>설명

`DBCC SHOWRESULTCACHESPACEUSED` 명령은 매개 변수를 사용하지 않으며 해당 명령이 실행되는 데이터베이스에서 사용하는 공간을 반환합니다.

## <a name="permissions"></a>사용 권한

VIEW SERVER STATE 권한이 필요합니다.
  
## <a name="result-sets"></a>결과 집합  
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|reserved_space|bigint|데이터베이스에 사용된 총 공간(KB)입니다. 이 값은 캐시된 결과 집합이 증가할 때 변경됩니다.|  
|data_space|bigint|데이터에 사용된 공간(KB)입니다.|  
|index_space|bigint|인덱스에 사용된 공간(KB)입니다.|  
|unused_space|bigint|예약된 공간이면서 사용되지 않은 공간(KB)입니다.|  

## <a name="see-also"></a>참고 항목

[결과 집합 캐싱을 사용한 성능 조정](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../statements/alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)</br>
[ALTER DATABASE&#40;Transact-SQL&#41;](../statements/alter-database-transact-sql.md?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](../statements/set-result-set-caching-transact-sql.md)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](./dbcc-dropresultsetcache-transact-sql.md)