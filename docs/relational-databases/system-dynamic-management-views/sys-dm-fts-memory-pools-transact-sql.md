---
title: sys.dm_fts_memory_pools (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools
- dm_fts_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_memory_pools dynamic management view
ms.assetid: 24747239-cd78-4d55-a00a-19233a457f42
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d45436070618e446921c610a9e82b0cc35271c8d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265912"
---
# <a name="sysdmftsmemorypools-transact-sql"></a>sys.dm_fts_memory_pools(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 탐색이나 전체 텍스트 탐색 범위에 대해 전체 텍스트 Gatherer 구성 요소에서 사용할 수 있는 공유 메모리 풀에 대한 정보를 반환합니다.  
   
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|할당된 메모리 풀의 ID입니다.<br /><br /> 0 = 작은 버퍼<br /><br /> 1 = 큰 버퍼|  
|**buffer_size**|**int**|메모리 풀에서 각 할당된 버퍼의 크기입니다.|  
|**min_buffer_limit**|**int**|메모리 풀에 허용된 최소 버퍼 수입니다.|  
|**max_buffer_limit**|**int**|메모리 풀에 허용된 최대 버퍼 수입니다.|  
|**buffer_count**|**int**|메모리 풀에 있는 현재 공유 메모리 버퍼 수입니다.|  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층 필요는 `VIEW DATABASE STATE` 데이터베이스의 권한. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에 필요 합니다 **서버 관리자** 요소나 **Azure Active Directory 관리자** 계정.   
 
## <a name="physical-joins"></a>물리적 조인  
 ![이 동적 관리 뷰의 유효 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-pools-1.gif "이 동적 관리 뷰의 유효 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|다 대 일|  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 프로세스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 Gatherer 구성 요소가 소유한 총 공유 메모리를 반환합니다.  
  
```  
SELECT SUM(buffer_size * buffer_count) AS "total memory"   
    FROM sys.dm_fts_memory_pools;  
```  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
