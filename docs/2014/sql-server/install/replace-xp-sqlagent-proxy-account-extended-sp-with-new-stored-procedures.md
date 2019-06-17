---
title: 확장 저장된 프로시저를 새로운 저장된 프로시저로 xp_sqlagent_proxy_account의 사용을 대체 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- xp_sqlagent_proxy_account
ms.assetid: 0e3cc931-6237-41dd-bf0d-0c03f4d8fff2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4faff8420e318f7250cfc67dda173197d8028f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092756"
---
# <a name="replace-usage-of-the-xpsqlagentproxyaccount-extended-stored-procedure-with-new-stored-procedures"></a>xp_sqlagent_proxy_account 확장 저장 프로시저를 새로운 저장 프로시저로 대체합니다.
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 여러 프록시를 지원합니다. 새로운 저장 프로시저 집합을 사용하여 이러한 프록시를 정의할 수 있습니다. 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 저장 프로시저에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 다음 항목을 참조하십시오.  
  
-   "sp_add_proxy([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_delete_proxy([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_login_for_proxy([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_proxy_for_subsystem([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_sqlagent_subsystems([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_grant_proxy_to_subsystem([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_grant_login_to_proxy([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_help_proxy"([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_revoke_login_from_proxy([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_revoke_proxy_from_subsystem([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_update_proxy([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]로 업그레이드한 후에는 **xp_sqlagent_proxy_account** 확장 저장 프로시저를 사용하는 모든 문이 작동하지 않습니다. **xp_cmdshell** 에 대한 프록시를 설정하려면 **xp_sqlagent_proxy_account** 대신 **sp_xp_cmdshell_proxy_account**를 사용하십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 업그레이드 문제](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
