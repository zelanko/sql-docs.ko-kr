---
title: dbo.syssessions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2ad2ccc2505c3bb72b8d2efc02afbc5ef5aebaf0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470562"
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 시작할 때마다 새 세션을 만듭니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 세션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 다시 시작되거나 갑자기 중지될 경우 작업 상태를 보존할 수 있습니다. 각 행을 **syssessions** 테이블 하나에 대 한 세션 정보가 들어 있습니다. 사용 된 **sysjobactivity** 각 세션이 끝날 때 작업 상태를 보려면 테이블입니다.  
  
 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 세션의 ID입니다.|  
|**agent_start_date**|**datetime**|이 세션에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 시작된 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>Remarks  
 구성원 인 사용자만의 합니다 **sysadmin** 고정된 서버 역할이이 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [dbo.sysjobactivity &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
