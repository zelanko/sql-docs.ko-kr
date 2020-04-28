---
title: dbo. syssubsystems 시스템 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syssubsystems
- syssubsystems
- syssubsystems_TSQL
- dbo.syssubsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syssubsystems system table
ms.assetid: 114b3d55-1ad6-4777-b868-8ef0c86ba596
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3f06182f06e92ff581dd02c072b63fc10962921a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68069080"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 하위 시스템에 대한 정보를 포함합니다. **Syssubsystems 시스템** 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|하위 시스템의 ID입니다.|  
|**하위**|**nvarchar(40)**|하위 시스템의 이름입니다.|  
|**description_id**|**int**|하위 시스템 설명을 포함 하는 행의 메시지 ID **입니다.**|  
|**subsystem_dll**|**nvarchar(255)**|하위 시스템 DLL의 위치입니다.|  
|**agent_exe**|**nvarchar(255)**|하위 시스템을 사용하는 실행 파일의 전체 경로입니다.|  
|**start_entry_point**|**nvarchar(30)**|하위 시스템이 초기화될 때 호출되는 함수입니다.|  
|**event_entry_point**|**nvarchar(30)**|하위 시스템 단계가 실행될 때 호출되는 함수입니다.|  
|**stop_entry_point**|**nvarchar(30)**|하위 시스템이 실행을 마칠 때 호출되는 함수입니다.|  
|**max_worker_threads**|**int**|지정된 하위 시스템의 최대 동시 단계 수입니다.|  
  
## <a name="remarks"></a>설명  
 **Sysadmin** 고정 서버 역할의 멤버만이 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [dbo. sysproxysubsystem &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [&#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
