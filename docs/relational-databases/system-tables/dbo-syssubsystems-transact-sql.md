---
title: dbo.syssubsystems (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a7ed7d2c7d6e463234d853cf644b8c589caf9246
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 하위 시스템에 대한 정보를 포함합니다. **syssubsystems** 테이블에 저장 됩니다는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|하위 시스템의 ID입니다.|  
|**subsystem**|**nvarchar(40)**|하위 시스템의 이름입니다.|  
|**description_id**|**int**|메시지에 있는 행의 ID는 **sys.messages** 하위 시스템 설명이 포함 된 주는 카탈로그 뷰입니다.|  
|**subsystem_dll**|**nvarchar(255)**|하위 시스템 DLL의 위치입니다.|  
|**agent_exe**|**nvarchar(255)**|하위 시스템을 사용하는 실행 파일의 전체 경로입니다.|  
|**start_entry_point**|**nvarchar(30)**|하위 시스템이 초기화될 때 호출되는 함수입니다.|  
|**event_entry_point**|**nvarchar(30)**|하위 시스템 단계가 실행될 때 호출되는 함수입니다.|  
|**stop_entry_point**|**nvarchar(30)**|하위 시스템이 실행을 마칠 때 호출되는 함수입니다.|  
|**max_worker_threads**|**int**|지정된 하위 시스템의 최대 동시 단계 수입니다.|  
  
## <a name="remarks"></a>주의  
 구성원만는 **sysadmin** 고정된 서버 역할이이 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [dbo.sysproxysubsystem &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys.messages &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
