---
title: 확장 저장된 프로시저를 새로운 저장된 프로시저로 xp_sqlagent_proxy_account의 사용을 바꾸기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- xp_sqlagent_proxy_account
ms.assetid: 0e3cc931-6237-41dd-bf0d-0c03f4d8fff2
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a35af2b28d8eb35d8db74f113ff8852ace1e82cb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184629"
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
  
  