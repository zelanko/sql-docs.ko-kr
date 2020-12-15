---
description: sys.dm_fts_outstanding_batches(Transact-SQL)
title: sys.dm_fts_outstanding_batches (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_outstanding_batches
- dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches
dev_langs:
- TSQL
helpviewer_keywords:
- troubleshooting [SQL Server], full-text search
- sys.dm_fts_outstanding_batches dynamic management view
ms.assetid: c4d697ed-c906-4c28-b137-036a25e13c84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4398bd8b24d4e9bf741371ad0f298dfb91ff13ab
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484655"
---
# <a name="sysdm_fts_outstanding_batches-transact-sql"></a>sys.dm_fts_outstanding_batches(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  각 전체 텍스트 인덱싱 일괄 처리에 대한 정보를 반환합니다.  
  
  |열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스의 ID입니다.|  
|catalog_id|**int**|전체 텍스트 카탈로그의 ID입니다.|  
|table_id|**int**|전체 텍스트 인덱스를 포함하는 테이블 ID의 ID입니다.|  
|batch_id|**int**|일괄 처리 ID|  
|memory_address|**varbinary(8)**|일괄 처리 개체의 메모리 주소입니다.|  
|crawl_memory_address|**varbinary(8)**|탐색 개체의 메모리 주소입니다(부모 개체).|  
|memregion_memory_address|**varbinary(8)**|필터 데몬 호스트(fdhost.exe)에 대한 아웃바운드 공유 메모리의 메모리 영역 메모리 주소입니다.|  
|hr_batch|**int**|일괄 처리에 대한 가장 최근의 오류 코드입니다.|  
|is_retry_batch|**bit**|다시 시도 일괄 처리인지 여부를 나타냅니다.<br /><br /> 0 = 아니요<br /><br /> 1 = 예|  
|retry_hints|**int**|일괄 처리에 필요한 다시 시도 작업의 유형입니다.<br /><br /> 0 = 다시 시도 안 함<br /><br /> 1 = 다중 스레드 다시 시도<br /><br /> 2 = 단일 스레드 다시 시도<br /><br /> 3 = 단일 및 다중 스레드 다시 시도<br /><br /> 5 = 다중 스레드 마지막 다시 시도<br /><br /> 6 = 단일 스레드 마지막 다시 시도<br /><br /> 7 = 단일 및 다중 스레드 마지막 다시 시도|  
|retry_hints_description|**nvarchar(120)**|필요한 다시 시도 작업의 유형에 대한 설명입니다.<br /><br /> 다시 시도 안 함<br /><br /> 다중 스레드 다시 시도<br /><br /> 단일 스레드 다시 시도<br /><br /> 단일 및 다중 스레드 다시 시도<br /><br /> 다중 스레드 마지막 다시 시도<br /><br /> 단일 스레드 마지막 다시 시도<br /><br /> 단일 및 다중 스레드 마지막 다시 시도|  
|doc_failed|**bigint**|일괄 처리에서 실패한 문서의 수입니다.|  
|batch_timestamp|**timestamp**|일괄 처리 생성 시 얻은 타임스탬프 값입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   
  
## <a name="examples"></a>예  
 다음 예에서는 서버 인스턴스에 있는 각 테이블에 대해 현재 처리되고 있는 일괄 처리 수를 구합니다.  
  
```  
SELECT database_id, table_id, COUNT(*) AS batch_count FROM sys.dm_fts_outstanding_batches GROUP BY database_id, table_id ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
