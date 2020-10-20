---
description: DBCC DROPRESULTSETCACHE(Transact-SQL)
title: DBCC DROPRESULTSETCACHE(Transact-SQL)
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
ms.openlocfilehash: e725124c49c5936567e0c7bd9272dceff7a7161d
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037431"
---
# <a name="dbcc-dropresultsetcache--transact-sql"></a>DBCC DROPRESULTSETCACHE(Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스에서 모든 결과 세트 캐시 항목을 제거합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DBCC DROPRESULTSETCACHE
[;]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="permissions"></a>사용 권한

DB_OWNER 고정 데이터베이스 역할의 멤버 자격이 필요합니다.

## <a name="remarks"></a>설명

- 이 명령은 모든 쿼리에 대한 결과 집합 캐시를 비웁니다.  

- 데이터베이스에 대한 결과 집합 캐시 기능을 꺼도 캐시된 결과가 모두 삭제됩니다.  

- 결과 집합 캐싱을 사용하도록 설정된 데이터베이스를 일시 중지하면 캐시된 결과가 삭제되지 않습니다.  

## <a name="see-also"></a>참고 항목

- [결과 집합 캐싱을 사용한 성능 조정](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
- [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../statements/alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)</br>
- [ALTER DATABASE&#40;Transact-SQL&#41;](../statements/alter-database-transact-sql.md?view=azure-sqldw-latest)</br>
- [SET RESULT SET CACHING &#40;Transact-SQL&#41;](../statements/set-result-set-caching-transact-sql.md)</br>
- [DBCC SHOWRESULTCACHESPACEUSED &#40;Transact-SQL&#41;](./dbcc-showresultcachespaceused-transact-sql.md)