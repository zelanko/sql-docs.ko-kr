---
title: 서비스 계정(데이터베이스 미러링 보안 구성 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 457a5b4bf517dcff91458740e53bacf3434bf7fd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>서비스 계정(데이터베이스 미러링 보안 구성 마법사)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Windows 인증을 사용할 때 서버 인스턴스가 다른 계정을 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 서비스 계정을 지정합니다. 이러한 서비스 계정은 모두 같은 도메인 또는 트러스트된 도메인에 있는 도메인 계정이어야 합니다.  
  
 모든 서버 인스턴스가 동일한 도메인 계정을 사용하거나 인증서 기반 인증을 사용하는 경우 필드를 비워 둡니다. **마침**을 클릭하기만 하면 마법사가 자동으로 현재 마법사 계정을 기반으로 계정을 구성합니다.  
  
> [!IMPORTANT]  
>  서버 인스턴스의 데이터베이스 미러링 끝점에서 인증서를 사용하도록 구성되어 있는 경우에는 서비스 계정 필드를 비워 두어야 합니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 구성하려면**  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>변수  
 **주 서버**  
 주 서버 인스턴스의 서비스 계정을 지정합니다. 도메인 이름을 대문자로 입력합니다.  
  
 *DOMAINNAME*\\*username*  
  
 **미러**  
 미러 서버 인스턴스의 서비스 계정을 지정합니다. 도메인 이름을 대문자로 입력합니다.  
  
 *DOMAINNAME*\\*username*  
  
 **미러링 모니터**  
 미러링 모니터 서버 인스턴스의 서비스 계정을 지정합니다. 도메인 이름을 대문자로 입력합니다.  
  
 *DOMAINNAME*\\*username*  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 속성&#40;미러링 페이지&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 또는 Always On 가용성 그룹에 대한 로그인 계정 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
