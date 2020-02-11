---
title: sys. dm_fts_memory_pools (Transact-sql) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68265912"
---
# <a name="sysdm_fts_memory_pools-transact-sql"></a>sys.dm_fts_memory_pools(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 탐색이나 전체 텍스트 탐색 범위에 대해 전체 텍스트 Gatherer 구성 요소에서 사용할 수 있는 공유 메모리 풀에 대한 정보를 반환합니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|할당된 메모리 풀의 ID입니다.<br /><br /> 0 = 작은 버퍼<br /><br /> 1 = 큰 버퍼|  
|**buffer_size**|**int**|메모리 풀에서 각 할당된 버퍼의 크기입니다.|  
|**min_buffer_limit**|**int**|메모리 풀에 허용된 최소 버퍼 수입니다.|  
|**max_buffer_limit**|**int**|메모리 풀에 허용된 최대 버퍼 수입니다.|  
|**buffer_count**|**int**|메모리 풀에 있는 현재 공유 메모리 버퍼 수입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 계층에서는 데이터베이스에 대 `VIEW DATABASE STATE` 한 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
 
## <a name="physical-joins"></a>물리적 조인  
 ![이 동적 관리 뷰의 유효 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-pools-1.gif "이 동적 관리 뷰의 유효 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|원본|수행할 작업|관계|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|다 대 일|  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 프로세스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 Gatherer 구성 요소가 소유한 총 공유 메모리를 반환합니다.  
  
```  
SELECT SUM(buffer_size * buffer_count) AS "total memory"   
    FROM sys.dm_fts_memory_pools;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
