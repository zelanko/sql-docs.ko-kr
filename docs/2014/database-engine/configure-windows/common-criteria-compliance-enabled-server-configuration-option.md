---
title: common criteria compliance enabled 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- common criteria compliance
helpviewer_keywords:
- CC (common criteria) [Database Engine]
- common criteria compliance [Database Engine]
- Risidual Information Protection [Database Engine]
- RIP (Residual Information Protection)
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8fef699da6e63c534d19e0d66bfa076f85348d29
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62786642"
---
# <a name="common-criteria-compliance-enabled-server-configuration-option"></a>common criteria compliance enabled 서버 구성 옵션
  common criteria compliance enabled 옵션은 Common Criteria에 필요한 다음 요소를 사용할 수 있게 합니다.  
  
|조건|Description|  
|--------------|-----------------|  
|RIP(잔여 정보 보호)|RIP를 사용하는 경우 메모리를 새 리소스에 다시 할당하기 전에 알려진 비트 패턴을 사용하여 메모리 할당을 덮어써야 합니다. RIP 표준이 충족되면 보안이 향상될 수 있지만 메모리 할당을 덮어쓰는 동안 성능이 저하될 수 있습니다. common criteria compliance enabled 옵션을 설정하면 덮어쓰기가 수행됩니다.|  
|로그인 통계를 확인할 수 있는 기능|common criteria compliance enabled 옵션을 설정하면 로그인 감사를 사용할 수 있습니다. 사용자가 성공적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로그인할 때마다 마지막으로 성공한 로그인 시간, 마지막으로 실패한 로그인 시간 및 마지막으로 성공한 로그인 시간과 현재 로그인 시간 사이의 시도 횟수에 대한 정보를 사용할 수 있습니다. 이러한 로그인 통계는 [sys.dm_exec_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql) 동적 관리 뷰를 쿼리하여 볼 수 있습니다.|  
|열 GRANT가 테이블 DENY를 재정의하지 않아야 함|common criteria compliance enabled 옵션을 설정하면 테이블 수준 DENY가 열 수준 GRANT보다 우선 적용됩니다. 이 옵션을 설정하지 않으면 열 수준 GRANT가 테이블 수준 DENY보다 우선 적용됩니다.|  
  
 common criteria compliance enabled 옵션은 고급 옵션입니다. Common Criteria는 Enterprise Edition 및 Datacenter Edition에 대해서만 평가되고 인증됩니다. Common Criteria 인증의 최신 상태는 [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) 웹 사이트를 참조하세요.  
  
> [!IMPORTANT]  
>  common criteria compliance enabled 옵션을 설정하는 것 외에도 Common Criteria EAL4+(Evaluation Assurance Level 4+)를 준수하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성하는 스크립트를 다운로드하여 실행해야 합니다. 이 스크립트는 [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) 웹 사이트에서 다운로드할 수 있습니다.  
  
 sp_configure 시스템 저장 프로시저를 사용하여 설정을 변경하는 경우에는 show advanced options를 1로 설정할 때만 common criteria compliance enabled를 변경할 수 있습니다. 이 설정은 서버를 다시 시작한 후에 적용됩니다. 가능한 값은 0과 1입니다.  
  
-   0은 Common Criteria 준수를 설정하지 않음을 나타냅니다. 이것이 기본값입니다.  
  
-   1은 Common Criteria 준수를 설정함을 나타냅니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Common Criteria 준수를 설정합니다.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'common criteria compliance enabled', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
