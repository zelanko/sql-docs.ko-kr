---
description: sys.dm_fts_fdhosts(Transact-SQL)
title: sys.dm_fts_fdhosts (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_fdhosts
- dm_fts_fdhosts_TSQL
- sys.dm_fts_fdhosts
- sys.dm_fts_fdhosts_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_fdhosts dynamic management view
- troubleshooting [SQL Server], full-text search
ms.assetid: d42a6334-4362-4361-83da-f8324fe55ec7
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0b8463e0de839390130f53ea7fba4f09d10e6e21
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97324508"
---
# <a name="sysdm_fts_fdhosts-transact-sql"></a>sys.dm_fts_fdhosts(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  서버 인스턴스에 있는 필터 데몬 호스트의 현재 작업에 대한 정보를 반환합니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**int**|필터 데몬 호스트의 ID입니다.|  
|**fdhost_name**|**nvarchar(120)**|필터 데몬 호스트의 이름입니다.|  
|**fdhost_process_id**|**int**|필터 데몬 호스트의 Windows 프로세스 ID입니다.|  
|**fdhost_type**|**nvarchar(120)**|필터 데몬 호스트에서 처리 중인 문서 형식이며 다음 중 하나입니다.<br /><br /> 단일 스레드<br /><br /> 다중 스레드<br /><br /> 대용량 문서|  
|**max_thread**|**int**|필터 데몬 호스트의 최대 스레드 수입니다.|  
|**batch_count**|**int**|필터 데몬 호스트에서 처리 중인 일괄 처리 수입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   

## <a name="examples"></a>예제  
 다음 예에서는 필터 데몬 호스트의 이름과 이 호스트의 최대 스레드 수를 반환합니다. 또한 필터 데몬 호스트에서 현재 처리되고 있는 일괄 처리 수를 모니터링합니다. 이 정보를 사용하여 성능 문제를 진단할 수 있습니다.  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
