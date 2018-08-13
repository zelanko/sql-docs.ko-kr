---
title: sys.dm_fts_memory_buffers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_memory_buffers
- dm_fts_memory_buffers_TSQL
- dm_fts_memory_buffers
- sys.dm_fts_memory_buffers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_memory_buffers dynamic management view
ms.assetid: 56895fe5-e8df-4d75-9adc-c1f7757cdef8
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 91a0949d70898a470e3f5b57e7d42d0befedc38f
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556523"
---
# <a name="sysdmftsmemorybuffers-transact-sql"></a>sys.dm_fts_memory_buffers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 탐색이나 전체 텍스트 탐색 범위의 일부로 사용되는 특정 메모리 풀에 속한 메모리 버퍼에 대한 정보를 반환합니다.  
  
> [!NOTE]
> 이후 릴리스에서 다음 열이 제거 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **row_count**합니다. 향후 개발 작업에서는 이 열을 사용하지 않도록 하고 현재 이러한 열을 사용하는 응용 프로그램은 수정하십시오.  

  
|Column|데이터 형식|Description|  
|------------|---------------|-----------------|  
|**pool_id**|**int**|할당된 메모리 풀의 ID입니다.<br /><br /> 0 = 작은 버퍼<br /><br /> 1 = 큰 버퍼|  
|**memory_address**|**varbinary(8)**|할당된 메모리 풀의 주소입니다.|  
|**name**|**nvarchar(4000)**|할당이 이루어진 공유 메모리 버퍼의 이름입니다.|  
|**is_free**|**bit**|메모리 버퍼의 현재 상태입니다.<br /><br /> 0 = 비어 있음<br /><br /> 1 = 사용 중|  
|**row_count**|**int**|이 버퍼에서 현재 처리하고 있는 행 수입니다.|  
|**bytes_used**|**int**|이 버퍼에서 사용 중인 메모리(바이트)입니다.|  
|**percent_used**|**int**|할당된 메모리 중 사용된 메모리의 비율입니다.|  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
  
## <a name="physical-joins"></a>물리적 조인  
 ![이 동적 관리 뷰의 유효 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-buffers-1.gif "이 동적 관리 뷰의 유효 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|다 대 일|  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

