---
title: SQL Server 6.5 유휴 로그인은 업그레이드할 수 없습니다 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- passwords [SQL Server], dormant logins
- dormant logins
- logins [SQL Server], upgrading dormant logins
- identifying dormant logins
- password hashes [SQL Server]
ms.assetid: ebe18a74-0375-4df4-b894-239f8fdabb64
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2e2865607f058c077fc3d12c2e3c2f778450511d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095399"
---
# <a name="dormant-sql-server-65-logins-cannot-be-upgraded"></a>SQL Server 6.5 유휴 로그인은 업그레이드할 수 없습니다.
  업그레이드 관리자에서 해당 암호를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 직접 업그레이드할 수 없는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 로그인이 검색되었습니다.  
  
 이 로그인을 설정하려면 암호를 다시 설정해야 합니다. ALTER LOGIN을 사용하여 암호를 다시 설정할 수 있습니다.  
  
```  
ALTER LOGIN <login name> WITH PASSWORD = '<new password>' MUST_CHANGE  
```  
  
 정책 확인이 설정된 경우 시스템의 암호 복잡성 정책에 따라 새 암호의 유효성을 검사합니다. 복잡한 암호를 사용하고 정책 확인을 해제하지 않는 것이 좋습니다. MUST_CHANGE 옵션을 설정하면 사용자가 새 암호를 선택해야 합니다. 이것은 필수 사항은 아니지만 권장 사항입니다.  
  
 다음 쿼리를 사용하여 유휴 로그인을 확인할 수 있습니다.  
  
```  
SELECT * FROM sysxlogins WHERE (xstatus & 2048) = 2048;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
