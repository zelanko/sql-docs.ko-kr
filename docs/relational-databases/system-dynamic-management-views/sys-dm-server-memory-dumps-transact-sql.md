---
title: sys.dm_server_memory_dumps (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_server_memory_dumps_TSQL
- dm_server_memory_dumps_TSQL
- dm_server_memory_dumps
- sys.dm_server_memory_dumps
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_memory_dumps dynamic management view
ms.assetid: 41782719-f54d-4e11-941a-c050c7576e23
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dc01bf657dedabe839d0f6a6765e5f31adbe5662
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmservermemorydumps-transact-sql"></a>sys.dm_server_memory_dumps(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 생성된 각 메모리 덤프 파일에 대해 행을 하나씩 반환합니다. 이 동적 관리 뷰를 사용하여 잠재적인 문제를 해결할 수 있습니다.  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**filename**|**nvarchar(256)**|메모리 덤프 파일의 경로 및 이름입니다. null일 수 없습니다.|  
|**creation_time**|**datetimeoffset(7)**|파일을 만든 날짜와 시간입니다. null일 수 없습니다.|  
|**size_in_bytes**|**bigint**|파일의 크기(바이트)입니다. Null을 허용합니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 덤프 유형에는 미니덤프, 전체 스레드 덤프 또는 전체 덤프가 있습니다. 이 파일의 확장명은 .mdmp입니다.  
  
## <a name="security"></a>보안  
 덤프 파일에는 중요한 정보가 들어 있을 수 있습니다. 중요한 정보를 보호하려면 ACL(액세스 제어 목록)을 통해 파일에 대한 액세스를 제한하거나 파일을 액세스가 제한된 폴더에 복사합니다. 예를 들어 디버그 파일을 Microsoft 지원 서비스에 보내기 전에 중요한 정보나 기밀 정보를 제거하는 것이 좋습니다.  
  
### <a name="permissions"></a>Permissions  
 VIEW SERVER STATE 권한이 필요합니다.  
  
  
