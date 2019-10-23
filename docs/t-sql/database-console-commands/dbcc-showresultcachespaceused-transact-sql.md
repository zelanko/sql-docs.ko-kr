---
title: DBCC SHOWRESULTCACHESPACEUSED(Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 0a8e9207e22a0e9bb4fbb75d872697fc9d2ff76e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452836"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED(Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스에 대한 스토리지 공간 사용 결과 세트 캐싱을 보여 줍니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Remarks

`DBCC SHOWRESULTCACHESPACEUSED` 명령은 매개 변수를 사용하지 않으며 해당 명령이 실행되는 데이터베이스에서 사용하는 공간을 반환합니다.

## <a name="permissions"></a>사용 권한

VIEW SERVER STATE 권한이 필요합니다.
  
## <a name="result-sets"></a>결과 집합  
  
|Column|데이터 형식|설명|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|데이터베이스에 사용된 총 공간(KB)입니다. 이 값은 캐시된 결과 집합이 증가할 때 변경됩니다.|  
|data_space|BIGINT|데이터에 사용된 공간(KB)입니다.|  
|index_space|BIGINT|인덱스에 사용된 공간(KB)입니다.|  
|unused_space|BIGINT|예약된 공간이면서 사용되지 않은 공간(KB)입니다.|  


## <a name="see-also"></a>관련 항목:

[결과 집합 캐싱을 사용한 성능 조정](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)