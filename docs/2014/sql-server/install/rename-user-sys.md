---
title: Sys 사용자 이름 바꾸기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sys user names [SQL Server]
ms.assetid: d622d646-83e4-4b6f-9a21-77b301af04b5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce8656df63c9d415ca09b54ecb86b87aba8bd83a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092856"
---
# <a name="rename-user-sys"></a>sys 사용자 이름을 바꿉니다.
  업그레이드 관리자가 데이터베이스에서 **sys** 사용자 이름을 검색했습니다. 이 이름은 예약되어 있습니다. 업그레이드하기 전에 사용자 이름을 바꾸십시오. 사용자 이름을 바꾸지 않으면 업그레이드 후 데이터베이스가 주의 대상 상태가 되며 온라인 상태가 될 때까지 데이터베이스를 사용할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 
  **sys** 사용자는 예약되어 있습니다.  
  
## <a name="corrective-action"></a>수정 동작  
  
### <a name="before-upgrade-procedure"></a>업그레이드 전 절차  
 업그레이드하기 전에 **sys**사용자가 포함된 각 데이터베이스에서 다음을 수행하십시오.  
  
1.  새 사용자를 만듭니다.  
  
2.  다음 문을 사용하여 **sys** 사용자가 부여한 사용 권한과 **sys**사용자에게 부여된 사용 권한을 모두 표시합니다.  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  
  **sp_changeobjectowner** 를 사용하여 **sys**가 소유한 모든 개체의 소유권을 새 사용자로 전송합니다.  
  
4.  
  **sys**사용자를 삭제합니다.  
  
5.  GRANT 문의 AS *new_user* 절을 사용하여 2단계에서 캡처된 원래 사용 권한을 복원합니다.  
  
6.  새 사용자를 참조하도록 스크립트를 수정합니다. 예를 들어 `SELECT * FROM sys.my`_`table` 과 같은 문이 포함된 스크립트를 `SELECT * FROM new_user.my_table`로 변경해야 합니다.  
  
### <a name="after-upgrade-procedure"></a>업그레이드 후 절차  
 업그레이드하기 전에 **sys** 사용자의 이름을 바꾸지 않았다면 다음을 수행하십시오.  
  
1.  
  `ALTER DATABASE db_name SET ONLINE`문을 실행합니다. 데이터베이스는 SINGLE_USER 모드가 됩니다.  
  
2.  "업그레이드 전 절차" 섹션의 모든 단계를 수행합니다.  
  
3.  
  `ALTER DATABASE db_name SET MULTI_USER`문을 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
