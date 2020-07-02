---
title: dbo.sysproxysubsystem (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxysubsystem_TSQL
- dbo.sysproxysubsystem
- sysproxysubsystem_TSQL
- sysproxysubsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxysubsystem system table
ms.assetid: 6d7713f5-1253-4a19-b1fb-635c377c95c1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 04ffb0b8cd280566c77111cfba55319510237127
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750281"
---
# <a name="dbosysproxysubsystem-transact-sql"></a>dbo.sysproxysubsystem(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  각 프록시 계정에서 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 하위 시스템을 기록합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|하위 시스템의 ID입니다. 이 값은 **syssubsystems 시스템** 테이블의 **subsystem_id** 열에 해당 합니다.|  
|**proxy_id**|**int**|프록시 계정의 ID입니다. 이 값은 **sysproxies** 테이블의 **proxy_id** 열에 해당 합니다.|  
  
## <a name="remarks"></a>설명  
 **Sysadmin** 고정 서버 역할의 멤버만이 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [dbo.sys하위 시스템 &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)   
 [Transact-sql&#41;&#40;dbo.sys프록시](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
