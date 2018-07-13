---
title: 노출 영역 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reducing attackable surface area
- upgrading SQL Server, security
- surface area configuration [SQL Server]
- surface area configuration [SQL Server], about surface area configuration
- attackable surface area [SQL Server]
- installing SQL Server, security
ms.assetid: f741169c-1453-4ad2-830b-bf2be27d712f
caps.latest.revision: 79
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7032966cb0fb1975b65847ac1e6e0a6c5dc43b1d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172194"
---
# <a name="surface-area-configuration"></a>노출 영역 구성
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]새로 설치의 기본 구성에서는 많은 기능이 활성화되어 있지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 악의적인 사용자로부터 공격 대상이 될 수 있는 기능 수를 최소화하기 위해 주요 서비스와 기능만 필요에 따라 설치하고 시작합니다. 시스템 관리자는 설치 시 이러한 기본값을 변경할 수 있으며 필요에 따라 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 기능을 활성화 또는 비활성화할 수 있습니다. 또한 다른 컴퓨터에서 연결하는 경우 일부 구성 요소는 프로토콜을 구성해야만 사용할 수 있습니다.  
  
> [!NOTE]  
>  새로 설치와 달리 업그레이드 중에는 기존 서비스 또는 기능이 해제되지 않지만 추가 노출 영역 구성 옵션은 업그레이드가 완료된 후에 적용할 수 있습니다.  
  
## <a name="protocols-connection-and-startup-options"></a>프로토콜, 연결 및 시작 옵션  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 서비스를 시작/중지하고 시작 옵션을 구성하고 프로토콜 및 기타 연결 옵션을 설정할 수 있습니다.  
  
#### <a name="to-start-sql-server-configuration-manager"></a>SQL Server 구성 관리자를 시작하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
    -   **SQL Server 서비스** 영역을 사용하여 구성 요소를 시작하고 자동 시작 옵션을 구성합니다.  
  
    -   **SQL Server 네트워크 구성** 영역에서 연결 프로토콜, 고정 TCP/IP 포트와 같은 연결 옵션 또는 암호화 사용을 설정합니다.  
  
 자세한 내용은 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)을 참조하세요. 원격 연결도 올바른 방화벽 구성에 따라 달라질 수 있습니다. 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
## <a name="enabling-and-disabling-features"></a>기능 설정 및 해제  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능의 설정 및 해제는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 패싯을 사용하여 구성할 수 있습니다.  
  
#### <a name="to-configure-surface-area-using-facets"></a>패싯을 사용하여 노출 영역을 구성하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성 요소에 연결합니다.  
  
2.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **패싯**을 클릭합니다.  
  
3.  **패싯 보기** 대화 상자에서 **패싯** 목록을 확장하고 적절한 **노출 영역 구성** 패싯(**노출 영역 구성**, **Analysis Services에 대한 노출 영역 구성**또는 **Reporting Services에 대한 노출 영역 구성**)을 선택합니다.  
  
4.  **패싯 속성** 영역에서 각 속성에 대해 원하는 값을 선택합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 정책 기반 관리를 사용하여 패싯 구성을 주기적으로 확인할 수 있습니다. 정책 기반 관리에 대한 자세한 내용은 [정책 기반 관리를 사용하여 서버 관리](../policy-based-management/administer-servers-by-using-policy-based-management.md)를 참조하세요.  
  
 `sp_configure` 저장 프로시저를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 옵션을 설정할 수도 있습니다. 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
 **의** EnableIntegratedSecurity [!INCLUDE[ssRS](../../includes/ssrs-md.md)]속성을 변경하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 속성 설정을 사용합니다. **예약 이벤트 및 보고서 배달** 속성과 **웹 서비스 및 HTTP 액세스** 속성을 변경하려면 **RSReportServer.config** 구성 파일을 편집합니다.  
  
## <a name="command-prompt-options"></a>명령 프롬프트 옵션  
 **Invoke-PolicyEvaluation**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell cmdlet을 사용하여 노출 영역 구성 정책을 호출할 수 있습니다. 자세한 내용은 [데이터베이스 엔진 cmdlet 사용](../../database-engine/use-the-database-engine-cmdlets.md)을 참조하세요.  
  
## <a name="soap-and-service-broker-endpoints"></a>SOAP 및 Service Broker 끝점  
 끝점을 끄려면 정책 기반 관리를 사용하고 끝점의 속성을 만들고 변경하려면 [CREATE ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql) 및 [ALTER ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)를 사용합니다.  
  
## <a name="related-content"></a>관련 내용  
 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
