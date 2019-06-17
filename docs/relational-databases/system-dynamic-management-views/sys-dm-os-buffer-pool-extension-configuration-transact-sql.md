---
title: sys.dm_os_buffer_pool_extension_configuration (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_buffer_pool_extension_configuration
- sys.dm_os_buffer_pool_extension_configuration_TSQL
- dm_os_buffer_pool_extension_configuration_TSQL
- sys.dm_os_buffer_pool_extension_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_pool_extension_configuration dynamic management view
ms.assetid: d52cc481-4d29-4f33-b63d-231ec35d092f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d6d647fc2a1a4d5f88a85ec5917125527004570c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62503803"
---
# <a name="sysdmosbufferpoolextensionconfiguration-transact-sql"></a>sys.dm_os_buffer_pool_extension_configuration(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 버퍼 풀 확장에 대한 구성 정보를 반환합니다. 각 버퍼 풀 확장 파일에 대해 하나의 행을 반환합니다.  
  

  
| 열 이름 | 데이터 형식 | Description |
| :---------- | :-------- | :---------- |
|path|**nvarchar**(256)|버퍼 풀 확장 캐시의 경로 및 파일 이름입니다. Null을 허용합니다.|  
|file_id|**int**|버퍼 풀 확장 파일의 ID입니다. Null을 허용하지 않습니다.|  
|state|**int**|버퍼 풀 확장 기능의 상태입니다. Null을 허용하지 않습니다.<br /><br /> 0 - 버퍼 풀 확장을 사용하지 않도록 설정됨<br /><br /> 1 - 버퍼 풀 확장을 사용하지 않도록 설정하는 중<br /><br /> 2-사용 하도록 예약<br /><br /> 3 - 버퍼 풀 확장을 사용하도록 설정하는 중<br /><br /> 4 - 나중에 사용하도록 예약되었습니다.<br /><br /> 5 - 버퍼 풀 확장을 사용하도록 설정됨|  
|state_description|**nvarchar**(60)|버퍼 풀 확장 기능의 상태를 설명합니다. Null을 허용합니다.<br /><br /> 0 = BUFFER POOL EXTENSION DISABLED<br /><br /> 5 = 버퍼 풀 확장을 사용 하도록 설정|
|current_size_in_kb|**bigint**|버퍼 풀 확장 파일의 현재 크기입니다. Null을 허용하지 않습니다.|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-configuration-buffer-pool-extension-information"></a>1\. 구성 버퍼 풀 확장 정보 반환  
 다음 예에서는 sys.dm_os_buffer_pool_extension_configruation DMV에서 모든 열을 반환합니다.  
  
```sql  
SELECT path, file_id, state, state_description, current_size_in_kb  
FROM sys.dm_os_buffer_pool_extension_configuration;  
```  
  
### <a name="b-returning-the-number-of-cached-pages-in-the-buffer-pool-extension-file"></a>2\. 버퍼 풀 확장 파일에서 캐시된 페이지 수 반환  
 다음 예에서는 각 버퍼 풀 확장 파일에 있는 캐시된 페이지 수를 반환합니다.  
  
```sql  
SELECT COUNT(*) AS cached_pages_count  
FROM sys.dm_os_buffer_descriptors  
WHERE is_in_bpool_extension <> 0  
;  
```  
  
## <a name="see-also"></a>관련 항목  
 [버퍼 풀 확장](../../database-engine/configure-windows/buffer-pool-extension.md)   
 [sys.dm_os_buffer_descriptors&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
  
