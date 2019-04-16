---
title: 사용 되지 않는 시스템 저장 프로시저에 대 한 참조를 제거 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system stored procedures [SQL Server]
- system stored procedures [SQL Server]
ms.assetid: 487d24fc-41d5-495e-843c-0ac974ec472f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f87cb9160925ccc813ee62737662f85f430f28b
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582866"
---
# <a name="remove-references-to-deprecated-system-stored-procedures"></a>더 이상 사용되지 않는 시스템 저장 프로시저에 대한 참조를 제거합니다.
  업그레이드 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 더 이상 사용할 수 없는 문서화되지 않은 시스템 저장 프로시저 및 확장 저장 프로시저를 참조하는 문을 발견했습니다. 이러한 개체를 참조하는 문은 실패합니다. 문서화되지 않은 시스템 개체나 API는 이후 릴리스에서 알림 표시 없이 변경되거나 제거될 수 있으므로 사용하지 마십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
  
### <a name="documented-system-stored-procedures"></a>문서화된 시스템 저장 프로시저  
 다음 문서화된 시스템 저장 프로시저가 제거되었습니다.  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
### <a name="undocumented-system-stored-procedures"></a>문서화되지 않은 시스템 저장 프로시저  
 다음 문서화되지 않은 시스템 저장 프로시저 및 확장 저장 프로시저가 제거되었습니다.  
  
-   sp_articlesynctranprocs  
  
-   sp_diskdefault  
  
-   sp_EventLog  
  
-   sp_GetMBCSCharLen  
  
-   sp_helplog  
  
-   sp_helpsql  
  
-   sp_IsMBCSLeadByte  
  
-   sp_lock2  
  
-   sp_MSget_current_activity  
  
-   sp_MSset_current_activity  
  
-   sp_MSobjessearch  
  
-   xp_enum_ActiveScriptEngines  
  
-   xp_eventlog  
  
-   xp_GetAdminGroupName  
  
-   xp_GetFileDetails  
  
-   xp_GetLocalSystemAccountName  
  
-   xp_IsNTAdmin  
  
-   xp_MSLocalSystem  
  
-   xp_MSnt2000  
  
-   xp_MSplatform  
  
-   xp_SetSecurity  
  
-   xp_varbintohexstr  
  
## <a name="corrective-action"></a>수정 동작  
  
### <a name="documented-system-stored-procedures"></a>문서화된 시스템 저장 프로시저  
 다음 표에 따라 애플리케이션을 수정합니다.  
  
|이전|단계|  
|----------------|-------------|  
|sp_addalias|별칭을 사용자 계정 및 데이터베이스 역할의 조합으로 대체해야 합니다. 자세한 내용은 SQL Server 온라인 설명서의 "CREATE USER(Transact-SQL)" 및 "CREATE ROLE(Transact-SQL)"을 참조하십시오. 업그레이드된 데이터베이스에서는 sp_dropalias를 사용하여 별칭을 제거합니다.|  
|sp_addgroupsp_changegroup<br /><br /> sp_dropgroup<br /><br /> sp_helpgroup|역할을 사용합니다. 자세한 내용은 SQL Server 온라인 설명서의 "서버 수준 역할" 및 "데이터베이스 수준 역할"을 참조하십시오.|  
  
### <a name="undocmented-system-stored-procedures"></a>문서화되지 않은 시스템 저장 프로시저  
 동일한 기능이 있는 CLR 저장 프로시저를 만들어 문서화되지 않은 시스템 저장 프로시저를 대체할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서에서 "CLR 저장 프로시저"를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
