---
title: 업그레이드 문제 해결 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Upgrade Advisor [SQL Server], reference
- component issue resolution [Upgrade Advisor]
- resolving upgrade issues
- upgrade blocks [Upgrade Advisor]
- detecting upgrade issues
- finding upgrade issues
- Upgrade Advisor [SQL Server], blocking issues
- configurations preventing upgrading [Upgrade Advisor]
- locating upgrade issues
- blocking issues [Upgrade Advisor]
- issues preventing upgrading [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, reference
- analyzing system [Upgrade Advisor], resolving issues
- settings preventing upgrading [Upgrade Advisor]
- upgrade issue reference [Upgrade Advisor]
- identifying upgrade issues
- fixing upgrade issues [Upgrade Advisor]
ms.assetid: 113eb435-8d36-4ed6-9790-b5e4c14809c8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85de606ecea93aba80714d4266e9897dd856879f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092495"
---
# <a name="resolving-upgrade-issues"></a>업그레이드 문제 해결
  이 섹션의 항목에서는 검색 가능 여부에 관계없이 업그레이드 또는 업그레이드 이후 환경에 영향을 줄 수 있는 업그레이드 문제에 대해 설명합니다. 문제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소별로 구성됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [최신 업그레이드 문제](../../../2014/sql-server/install/late-breaking-upgrade-issues.md)  
  
-   [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
-   [전체 텍스트 Search 업그레이드 문제](../../../2014/sql-server/install/full-text-search-upgrade-issues.md)  
  
-   [복제 업그레이드 문제](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
-   [업그레이드 관리자를 &#40;업그레이드 문제를 Reporting Services&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
-   [SQL Server 에이전트 업그레이드 문제](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
## <a name="issues-that-prevent-upgrading"></a>업그레이드를 방해하는 문제  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 일부 구성 또는 설정이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하는 것을 방해할 수 있습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치할 때 이러한 문제가 검색되면 설치 프로그램에서는 업그레이드 프로세스가 중지되고 업그레이드 관리자를 실행하고 차단 문제를 모두 해결하도록 요청합니다.  
  
### [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
 다음 태스크가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 업그레이드 보고서에 나열되면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하기 전에 필요한 동작을 수행해야 합니다.  
  
-   [데이터베이스 ID 32767 분리](../../../2014/sql-server/install/detach-database-id-32767.md)  
  
-   [고정 서버 역할 이름과 일치하는 로그인 이름을 바꿉니다.](../../../2014/sql-server/install/rename-logins-matching-fixed-server-role-names.md)  
  
-   [sys 사용자 이름을 바꿉니다.](../../../2014/sql-server/install/rename-user-sys.md)  
  
-   [sp_rename을 사용하여 중복 인덱스 이름을 바꿉니다.](../../../2014/sql-server/install/use-sp-rename-to-rename-duplicate-index-name.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
