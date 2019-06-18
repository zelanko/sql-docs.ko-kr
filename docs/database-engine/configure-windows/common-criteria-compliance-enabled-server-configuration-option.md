---
title: Common Criteria Compliance Enabled 구성 | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2018
ms.prod: sql
ms.prod_service: high-availability
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
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 533cdfe3b83b8b759129a27a6dc1699298dd3f13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62817970"
---
# <a name="common-criteria-compliance-enabled-server-configuration"></a>Common Criteria Compliance Enabled 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

common criteria compliance enabled 옵션은 [정보 기술 보안 평가에 대한 Common Criteria](https://www.commoncriteriaportal.org/)에 필요한 다음 요소를 사용할 수 있게 합니다.  
  
|조건|설명|  
|--------------|-----------------|  
|RIP(잔여 정보 보호)|RIP를 사용하는 경우 메모리를 새 리소스에 다시 할당하기 전에 알려진 비트 패턴을 사용하여 메모리 할당을 덮어써야 합니다. RIP 표준이 충족되면 보안이 향상될 수 있지만 메모리 할당을 덮어쓰는 동안 성능이 저하될 수 있습니다. common criteria compliance enabled 옵션을 설정하면 덮어쓰기가 수행됩니다.|  
|로그인 통계를 확인할 수 있는 기능|common criteria compliance enabled 옵션을 설정하면 로그인 감사를 사용할 수 있습니다. 사용자가 성공적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로그인할 때마다 마지막으로 성공한 로그인 시간, 마지막으로 실패한 로그인 시간 및 마지막으로 성공한 로그인 시간과 현재 로그인 시간 사이의 시도 횟수에 대한 정보를 사용할 수 있습니다. 이러한 로그인 통계는 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 동적 관리 뷰를 쿼리하여 볼 수 있습니다.|  
|`GRANT` 열에서 `DENY`테이블을 재정의하지 않아야 함|common criteria compliance enabled 옵션을 사용하도록 설정하면 테이블 수준 `DENY`가 열 수준 `GRANT`보다 우선 적용됩니다. 이 옵션을 사용하지 않도록 설정하면 열 수준 `GRANT`가 테이블 수준 `DENY`보다 우선 적용됩니다.|  
  
 common criteria compliance enabled 옵션은 고급 옵션입니다. Common Criteria는 Enterprise Edition 및 Datacenter Edition에 대해서만 평가되고 인증됩니다. Common Criteria 인증의 최신 상태는 [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) 웹 사이트를 참조하세요.  
  
> [!IMPORTANT]  
>  common criteria compliance enabled 옵션을 설정하는 것 외에도 Common Criteria EAL4+(Evaluation Assurance Level 4+)를 준수하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성하는 스크립트를 다운로드하여 실행해야 합니다. 이 스크립트는 [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) 웹 사이트에서 다운로드할 수 있습니다.  
  
 `sp_configure` 시스템 저장 프로시저를 사용하여 설정을 변경하는 경우 show advanced options가 1로 설정되었을 때만 common criteria compliance enabled를 변경할 수 있습니다. 이 설정은 서버를 다시 시작한 후에 적용됩니다. 가능한 값은 0과 1입니다.  
  
-   0은 Common Criteria 준수를 설정하지 않음을 나타냅니다. 기본값입니다.  
  
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
RECONFIGURE WITH OVERRIDE; 
GO  
```  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 다시 시작합니다.
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
