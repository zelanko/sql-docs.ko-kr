---
title: "MDS(Master Data Services) 업그레이드 | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
caps.latest.revision: "31"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 28d67eed4c978e9f8c3b37752c8096fa00eec104
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="upgrade-master-data-services"></a>MDS(Master Data Services) 업그레이드
  다음은 Microsoft [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Master Data Services를 업그레이드하는 시나리오입니다.  
  
-   [데이터베이스 엔진 업그레이드 없이 업그레이드](../../database-engine/install-windows/upgrade-master-data-services.md#noengine)  
  
-   [데이터베이스 엔진 업그레이드를 사용해서 업그레이드](../../database-engine/install-windows/upgrade-master-data-services.md#engine)  
  
-   [두 컴퓨터에서의 업그레이드 시나리오](../../database-engine/install-windows/upgrade-master-data-services.md#twocomputer)  
  
-   [백업에서 데이터베이스를 복원하여 업그레이드](../../database-engine/install-windows/upgrade-master-data-services.md#restore)  
  
> [!IMPORTANT]  
> -   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 릴리스에서 CTP2 릴리스로 업그레이드할 수는 없습니다.  
> -   업그레이드를 수행하기 전에 데이터베이스를 백업합니다.  
> -   업그레이드 프로세스는 저장 프로시저를 다시 만들고 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]에서 사용되는 테이블을 업그레이드합니다. 이러한 구성 요소에 사용자 지정된 내용은 손실될 수 있습니다.  
> -   모델 배포 패키지는 해당 패키지를 만드는 데 사용한 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서만 사용할 수 있습니다. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에서 만든 모델 배포 패키지는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 배포할 수 없습니다.  
> -   Data Quality Services 및 MDS(Master Data Services)를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후 이전 버전의 모든 Excel용 MDS(Master Data Services) 추가 기능은 더 이상 작동하지 않습니다. Excel용 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Master Data Services 추가 기능은 [Microsoft Excel용 Master Data Services 추가 기능](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md) 에서 다운로드할 수 있습니다.  
  
##  <a name="fileLocation"></a> 파일 위치  
  
-   [!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]의 경우 파일은 기본적으로 *드라이브*:\Program Files\Microsoft SQL Server\140\Master Data Services에 설치됩니다.  

-   기본적으로 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 경우 파일은 *드라이브*:\Program Files\Microsoft SQL Server\130\Master Data Services에 설치됩니다.  
  
-   기본적으로 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 파일은 *드라이브*:\Program Files\Microsoft SQL Server\120\Master Data Services에 설치됩니다.  
  
-   기본적으로 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 경우 파일은 *드라이브*:\Program Files\Microsoft SQL Server\110\Master Data Services에 설치됩니다.  
  
-   기본적으로 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]의 경우 파일은 *드라이브*:\Program Files\Microsoft SQL Server\Master Data Services에 설치됩니다.  
  
##  <a name="noengine"></a> 데이터베이스 엔진 업그레이드 없이 업그레이드  
 이 시나리오에서는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]를 계속 사용하여 MDS 데이터베이스를 호스팅합니다. 그러나 MDS 데이터베이스의 스키마를 업그레이드한 다음 현재 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 웹 응용 프로그램을 만들어 MDS 데이터베이스에 액세스해야 합니다. 업그레이드 후에는 이전 웹 응용 프로그램에서 더 이상 MDS 데이터베이스에 액세스할 수 없습니다.  
  
 현재 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 및 이전 버전의 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]를 동일한 컴퓨터에 설치할 수 있습니다. [파일 위치](#fileLocation)에 표시된 대로 파일은 다른 위치에 설치됩니다.  
  
 **데이터베이스 엔진 업그레이드 없이 업그레이드하려면**  
  
1.  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 및 원하는 다른 기능을 설치합니다.  
  
    1.  [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 설치 마법사를 엽니다.  
  
    2.  왼쪽 창에서 **설치**를 클릭합니다.  
  
    3.  오른쪽 창에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
    4.  **기능 선택** 페이지에서 **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 및 설치할 다른 기능을 선택합니다.  
  
    5.  마법사를 완료합니다.  
  
2.  MDS 데이터베이스 스키마를 업그레이드합니다.  
  
    1.  현재 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 엽니다.  
  
        > [!IMPORTANT]  
        >  MDS 데이터베이스 스키마를 업그레이드하려면 MDS 데이터베이스를 만들 때 지정한 관리자 계정으로 로그인해야 합니다. MDS 데이터베이스의 mdm.tblUser에서 이 사용자의 **ID** 값은 **1**입니다.  
  
    2.  왼쪽 창에서 **데이터베이스 구성**을 클릭합니다.  
  
    3.  오른쪽 창에서 **데이터베이스 선택**을 클릭하고 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 데이터베이스 인스턴스에 대한 정보를 지정합니다.  
  
    4.  **데이터베이스 업그레이드** 를 클릭하여 **데이터베이스 업그레이드 마법사**를 시작합니다. 자세한 내용은 [데이터베이스 업그레이드 마법사&#40;Master Data Services 구성 관리자&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)를 참조하세요.  
  
3.  웹 응용 프로그램을 만듭니다.  
  
    1.  현재 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 엽니다.  
  
    2.  왼쪽 창에서 **웹 구성**을 클릭합니다.  
  
    3.  오른쪽 창의 **웹 사이트** 목록에서 다음 옵션 중 하나를 선택합니다.  
  
        -   **기본 웹 사이트**를 선택하고 **응용 프로그램 만들기**를 클릭합니다.  
  
        -   **새 사이트 만들기**를 선택합니다. 새 웹 사이트를 만들면 새 웹 응용 프로그램이 자동으로 만들어집니다.  
  
        > [!IMPORTANT]  
        >  이전 버전의 SQL Server([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])에 있는 기존 MDS 웹 응용 프로그램은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 Master Data Services 구성 관리자에서 선택할 수 있습니다. 기존 웹 응용 프로그램을 선택하는 대신 MDS용 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 웹 응용 프로그램을 만들어야 합니다. 이렇게 하지 않으면 웹 응용 프로그램을 업그레이드된 MDS 데이터베이스와 연결하려고 할 때 요청된 페이지의 관련 구성 데이터가 잘못되었기 때문에 해당 페이지에 액세스할 수 없다는 오류 메시지가 나타납니다.  
        >   
        >  MDS 웹 응용 프로그램에 기존([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) 웹 응용 프로그램과 동일한 이름(별칭)을 사용하려면, 먼저 IIS에서 웹 응용 프로그램과 관련 응용 프로그램 풀을 삭제한 다음, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 버전의 Master Data Services 구성 관리자를 사용하여 동일한 이름의 웹 응용 프로그램을 만들어야 합니다. 웹 응용 프로그램과 응용 프로그램 풀을 IIS에서 제거하는 방법은 [응용 프로그램 제거(IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) 및 [응용 프로그램 풀 제거(IIS)](http://go.microsoft.com/fwlink/?LinkId=323538)를 참조하세요.  
  
4.  새 웹 응용 프로그램을 업그레이드된 MDS 데이터베이스와 연결합니다.  
  
    1.  **응용 프로그램을 데이터베이스에 연결** 섹션에서 **선택**을 클릭합니다.  
  
    2.  MDS 데이터베이스를 선택합니다.  
  
    3.  **적용**을 클릭합니다.  
  
##  <a name="engine"></a> 데이터베이스 엔진 업그레이드를 사용해서 업그레이드  
 이 시나리오에서는 데이터베이스 엔진과 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 응용 프로그램을 모두 이전 버전에서 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 또는 [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)]로 업그레이드합니다.  
  
 **데이터베이스 엔진 업그레이드를 사용해서 업그레이드하려면**  
  
1.  **[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]의 경우에만**: **제어판** > **프로그램 및 기능**을 열고 Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 제거합니다.  
  
2.  데이터베이스 엔진을 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 또는 [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)]로 업그레이드합니다. 자세한 내용은 [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)을(를) 참조하세요.  
  
3.  [데이터베이스 엔진 업그레이드 없이 업그레이드](#noengine) 에서 모든 단계를 완료합니다.  
  
##  <a name="twocomputer"></a> 두 컴퓨터에서의 업그레이드 시나리오  
 이 시나리오에서는 두 컴퓨터에 SQL Server, 즉 하나에는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 또는 [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)], 다른 하나에는 이전 버전의 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]가 설치된 시스템을 업그레이드합니다.  
  
 이전 버전의 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]가 설치된 경우 이전 버전을 계속 사용하여 한 컴퓨터에서 MDS 데이터베이스를 호스팅합니다. 그러나 MDS 데이터베이스의 스키마를 업그레이드한 다음 각각 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 또는 [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] 웹 응용 프로그램을 사용하여 MDS 데이터베이스에 액세스해야 합니다. MDS 데이터베이스는 이전 버전의 웹 응용 프로그램에서 더 이상 액세스할 수 없습니다.  
  
 **두 컴퓨터 시나리오에서 업그레이드하려면**  
  
-   [데이터베이스 엔진 업그레이드 없이 업그레이드](#noengine)에서 모든 단계를 완료합니다.  
  
##  <a name="restore"></a> 백업에서 데이터베이스를 복원하여 업그레이드  
 이 시나리오에서는 동일한 컴퓨터 또는 서로 다른 두 컴퓨터에 이전 버전과 함께 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 또는 [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)]이 설치됩니다. 데이터베이스는 업그레이드하기 전에 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 또는 [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] 릴리스 이전의 버전에서 백업되었으며 이 데이터베이스를 복원해야 합니다.  
  
 **백업에서 데이터베이스를 복원하여 업그레이드하려면**  
  
1.  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 및 원하는 다른 기능을 설치합니다.  
  
    1.  [!INCLUDE[sssnoversion](../../includes/ssnoversion-md.md)] 설치 마법사를 엽니다.  
  
    2.  왼쪽 창에서 **설치**를 클릭합니다.  
  
    3.  오른쪽 창에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
    4.  **기능 선택** 페이지에서 **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 및 설치할 다른 기능을 선택합니다.  
  
    5.  마법사를 완료합니다.  
  
2.  백업한 데이터베이스를 복원합니다.  
  
3.  MDS 데이터베이스 스키마를 업그레이드하고 웹 응용 프로그램을 만들고 새 웹 응용 프로그램을 업그레이드된 MDS 데이터베이스와 연결합니다. 지침은 [데이터베이스 엔진 업그레이드 없이 업그레이드](#noengine)의 2-4단계를 참조하세요.  
  
## <a name="troubleshooting"></a>문제 해결  
 **문제:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 웹 응용 프로그램을 열면 "클라이언트 버전이 데이터베이스 버전과 호환되지 않습니다."라는 오류 메시지가 표시됩니다.  
  
 **해결 방법:** 이 문제는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 마스터 데이터 관리자 웹 응용 프로그램이 [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] Master Data Services로 업그레이드된 데이터베이스에 액세스하려고 할 때 발생합니다. [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] 웹 응용 프로그램을 대신 사용해야 합니다.  
  
 MDS 데이터베이스 스키마를 업그레이드할 때 IIS에서 **MDS 응용 프로그램 풀** 을 정지하고 다시 시작하지 않은 경우에도 이 문제가 발생할 수 있습니다. **MDS 응용 프로그램 풀** 을 다시 시작하여 문제를 해결합니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md)  
  
  