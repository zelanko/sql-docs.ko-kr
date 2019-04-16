---
title: 고정된 서버 역할 이름과 일치 하는 로그인 이름을 바꾸십시오. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- user-defined login names [SQL Server]
- fixed server roles [SQL Server]
- renamed logins [SQL Server]
- logins [SQL Server], names
ms.assetid: 10a1d77c-3153-474f-a6a0-969556794467
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa2e74dfc1afdfe25058657d910315a3fb626f1c
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582078"
---
# <a name="rename-logins-matching-fixed-server-role-names"></a>고정 서버 역할 이름과 일치하는 로그인 이름을 바꿉니다.
  업그레이드 관리자가 고정 서버 역할 이름과 일치하는 하나 이상의 사용자 정의 로그인 이름을 검색했습니다. 고정 서버 역할 이름은 예약되어 있습니다. 업그레이드하기 전에 로그인 이름을 바꾸십시오  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 다음과 같은 고정 서버 역할 이름은 예약되어 있으므로 사용자 정의 로그인 이름으로 사용할 수 없습니다.  
  
-   **sysadmin**  
  
-   **serveradmin**  
  
-   **setupadmin**  
  
-   **securityadmin**  
  
-   **processadmin**  
  
-   **dbcreator**  
  
-   **diskadmin**  
  
-   **bulkadmin**  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드하기 전에 다음 단계를 수행합니다.  
  
1.  다음 문을 실행하여 로그인의 SID(보안 ID)를 기록합니다.  
  
    ```  
    SELECT name, sid   
    FROM master.dbo.syslogins   
    WHERE name IN('sysadmin', 'serveradmin','setupadmin', 'securityadmin','processadmin', 'dbcreator','diskadmin','bulkadmin')  
    ```  
  
2.  로그인을 삭제합니다.  
  
3.  사용 된 **sp_addlogin** 시스템 프로시저를 새 로그인을 만듭니다. 1 단계에서 반환 된 SID를 지정 합니다 **@sid** 각 해당 로그인에 대 한 매개 변수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
