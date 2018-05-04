---
title: dbo.syssessions (Transact SQL) | Microsoft Docs
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
- dbo.syssessions_TSQL
- dbo.syssessions
- syssessions_TSQL
- syssessions
dev_langs:
- TSQL
helpviewer_keywords:
- syssessions system table
ms.assetid: 187819b6-c7f4-4a26-b74c-0a89e96695cf
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 213570dfbd6e426251389cf5aae8df4edd5a1d9f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 시작할 때마다 새 세션을 만듭니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 세션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 다시 시작되거나 갑자기 중지될 경우 작업 상태를 보존할 수 있습니다. 각 행은 **syssessions** 테이블에 대 한 한 세션 정보가 포함 되어 있습니다. 사용 하 여는 **sysjobactivity** 테이블의 각 세션 후에 작업 상태를 볼 수 있습니다.  
  
 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 세션의 ID입니다.|  
|**agent_start_date**|**datetime**|이 세션에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 시작된 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>주의  
 구성원 인 사용자만의 **sysadmin** 고정된 서버 역할이이 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [dbo.sysjobactivity &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
