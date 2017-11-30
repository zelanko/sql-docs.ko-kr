---
title: sp_enum_sqlagent_subsystems (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a088866b645cacad3813ce7c2ae15e9e9831f299
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spenumsqlagentsubsystems-transact-sql"></a>sp_enum_sqlagent_subsystems(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 하위 시스템을 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>인수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**하위 시스템**|**nvarchar (40)**|하위 시스템의 이름입니다.|  
|**설명**|**nvarchar(512)**|하위 시스템에 대한 설명입니다.|  
|**subsystem_dll**|**nvarchar(510)**|하위 시스템을 포함하는 DLL 모듈입니다.|  
|**agent_exe**|**nvarchar(510)**|하위 시스템이 사용하는 실행 모듈입니다.|  
|**start_entry_point**|**nvarchar (30)**|작업 단계 실행 중 SQL Server 에이전트가 호출하는 프로시저입니다.|  
|**event_entry_point**|**nvarchar (30)**|작업 단계 실행 중 SQL Server 에이전트가 호출하는 프로시저입니다.|  
|**stop_entry_point**|**nvarchar (30)**|작업 단계 실행 중 SQL Server 에이전트가 호출하는 프로시저입니다.|  
|**max_worker_threads**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 이 하위 시스템에 대해 시작할 최대 스레드 수입니다.|  
|**subsystem_id**|**int**|하위 시스템에 대한 식별자입니다.|  
  
## <a name="remarks"></a>주의  
 이 프로시저는 인스턴스에 사용할 수 있는 하위 시스템을 나열합니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 **msdb** 데이터베이스의 **SQLAgentOperatorRole** 고정 데이터베이스 역할을 부여 받아야 합니다.  
  
 에 대 한 내용은 **SQLAgentOperatorRole**, 참조 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 보안 구현](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_add_jobstep&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
