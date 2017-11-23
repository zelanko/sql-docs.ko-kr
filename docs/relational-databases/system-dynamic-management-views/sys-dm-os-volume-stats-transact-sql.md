---
title: sys.dm_os_volume_stats (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_volume_stats_TSQL
- dm_os_volume_stats
- sys.dm_os_volume_stats
- sys.dm_os_volume_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_volume_stats dynamic management function
ms.assetid: fa1c58ad-8487-42ad-956c-983f2229025f
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 43d9ead206eb4f5a83d0006c3b23626346b04fe5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosvolumestats-transact-sql"></a>sys.dm_os_volume_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지정된 데이터베이스와 파일이 저장된 운영 체제 볼륨(디렉터리)에 대한 정보를 반환합니다. 이 동적 관리 함수를 사용하여 물리적 디스크 드라이브의 특성을 확인하거나 디렉터리에 대한 사용 가능한 공간 정보를 반환할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sys.dm_os_volume_stats (database_id, file_id)  
```  
  
##  <a name="Arguments"></a> 인수  
 *database_id*  
 데이터베이스의 ID입니다. *database_id* 은 **int**, 기본값은 없습니다. NULL이 될 수 없습니다.  
  
 *file_id*  
 파일의 ID입니다. *file_id* 은 **int**, 기본값은 없습니다. NULL이 될 수 없습니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
||||  
|-|-|-|  
|**열**|**데이터 형식**|**Description**|  
|**database_id**|**int**|데이터베이스의 ID입니다. null일 수 없습니다.|  
|**file_id**|**int**|파일의 ID입니다. null일 수 없습니다.|  
|**volume_mount_point**|**nvarchar(512)**|해당 볼륨이 루트 경로로 지정된 탑재 지점입니다. 빈 문자열을 반환할 수 있습니다.|  
|**volume_id**|**nvarchar(512)**|운영 체제 볼륨 ID입니다. 빈 문자열을 반환할 수 있습니다.|  
|**logical_volume_name**|**nvarchar(512)**|논리 볼륨 이름입니다. 빈 문자열을 반환할 수 있습니다.|  
|**file_system_type**|**nvarchar(512)**|파일 시스템 볼륨 유형(예: NTFS, FAT, RAW)입니다. 빈 문자열을 반환할 수 있습니다.|  
|**total_bytes**|**bigint**|볼륨의 전체 크기(바이트)입니다. null일 수 없습니다.|  
|**available_bytes**|**bigint**|볼륨의 사용 가능한 공간입니다. null일 수 없습니다.|  
|**supports_compression**|**bit**|볼륨에서 운영 체제 압축을 지원하는지 여부를 나타냅니다. null일 수 없습니다.|  
|**supports_alternate_streams**|**bit**|볼륨에서 대체 스트림을 지원하는지 여부를 나타냅니다. null일 수 없습니다.|  
|**supports_sparse_files**|**bit**|볼륨에서 스파스 파일을 지원하는지 여부를 나타냅니다.  null일 수 없습니다.|  
|**is_read_only**|**bit**|볼륨이 현재 읽기 전용으로 표시되어 있는지 여부를 나타냅니다. null일 수 없습니다.|  
|**is_compressed**|**bit**|이 볼륨이 현재 압축되었는지 여부를 나타냅니다. null일 수 없습니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-return-total-space-and-available-space-for-all-database-files"></a>1. 모든 데이터베이스 파일에 대해 전체 공간과 사용 가능한 공간 반환  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스 파일에 대해 전체 공간과 사용 가능한 공간(바이트)을 반환합니다.  
  
```  
SELECT f.database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.master_files AS f  
CROSS APPLY sys.dm_os_volume_stats(f.database_id, f.file_id);  
```  
  
### <a name="b-return-total-space-and-available-space-for-the-current-database"></a>2. 현재 데이터베이스에 대해 전체 공간과 사용 가능한 공간 반환  
 다음 예에서는 현재 데이터베이스의 데이터베이스 파일에 대해 전체 공간과 사용 가능한 공간(바이트)을 반환합니다.  
  
```  
SELECT database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.database_files AS f  
CROSS APPLY sys.dm_os_volume_stats(DB_ID(f.name), f.file_id);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.master_files&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
