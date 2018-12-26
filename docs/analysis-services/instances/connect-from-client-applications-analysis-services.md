---
title: 클라이언트 응용 프로그램 (Analysis Services)에서 연결 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d71320fad55b9a0d052ad1bb9c9fd25ab861246c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019590"
---
# <a name="connect-from-client-applications-analysis-services"></a>클라이언트 애플리케이션에서 연결(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services를 처음 접하는 경우 이 항목의 정보를 사용하여 일반 도구 및 애플리케이션을 통해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 기존 인스턴스에 연결할 수 있습니다. 이 항목에서는 테스트를 위해 서로 다른 사용자 ID로 연결하는 방법에 대해서도 설명합니다.  
  
-   [SQL Server Management Studio를 사용하여 연결(SSMS)](#bkmk_SSMS)  
  
-   [Excel을 사용하여 연결](#bkmk_excel)  
  
-   [SQL Server Data Tools를 사용하여 연결](#bkmk_SSDT)  
  
-   [연결 테스트](#bkmk_tshoot)  
  
 연결 문자열 참조 설명서는 별도로 제공됩니다. 자세한 내용은 [연결 문자열 속성&#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)을 참조하세요.  
  
 성공적인 연결은 올바른 포트 구성과 적절한 사용자 권한에 달려 있습니다. 각 요구 사항에 대해 자세히 알아보려면 다음 링크를 클릭하십시오.  
  
-   [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [개체 및 작업 & #40;에 대 한 권한 부여 액세스 Analysis Services & #41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_SSMS"></a> SQL Server Management Studio를 사용하여 연결(SSMS)  
 SSMS에서 Analysis Services에 연결하여 서버 인스턴스와 데이터베이스를 대화형으로 관리할 수 있습니다. 또한 XMLA 또는 MDX 쿼리를 실행하여 관리 작업을 수행하거나 데이터를 검색할 수도 있습니다. 쿼리가 전송될 때 데이터베이스만 로드하는 다른 도구 및 애플리케이션과 달리 SSMS는 데이터베이스를 볼 수 있는 권한이 있다는 가정하에 서버에 연결할 때 모든 데이터베이스를 로드합니다. 즉, 서버에 수많은 테이블 형식 데이터베이스가 있는 경우 SSMS를 사용하여 연결할 때 모든 테이블 형식 데이터베이스가 시스템 메모리에 로드됩니다.  
  
 특정 사용자 ID로 SSMS를 실행하여 사용 권한을 테스트한 다음 해당 사용자로 Analysis Services에 연결할 수 있습니다.  
  
 Shift 키를 누른 상태에서 **SQL Server Management Studio** 바로 가기를 마우스 오른쪽 단추로 클릭하여 **다른 사용자로 실행** 옵션에 액세스합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작합니다. **서버에 연결** 대화 상자에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 유형을 선택합니다.  
  
2.  로그인 탭에서 서버가 실행 중인 컴퓨터의 이름을 입력하여 서버 이름을 입력합니다. 해당 네트워크 이름 또는 정규화된 도메인 이름을 사용하여 서버를 지정할 수 있습니다.  
  
     명명된 된 인스턴스의 경우 서버 이름을 servername\instance 이름 형식으로 지정해야 합니다. 예를 들어 네트워크 이름이 ADV-SRV062이고 Analysis Services가 Finance라는 명명된 인스턴스로 설치된 서버의 경우 이 명명 규칙은 ADV-SRV062\Finance일 수 있습니다.  
  
     장애 조치(failover) 클러스터에 배포된 서버의 경우 SSAS 클러스터의 네트워크 이름을 사용하여 연결합니다. 이 이름은 SQL Server를 설치하는 동안 **SQL Server 네트워크 이름**으로 지정됩니다. SSAS를 WSFC(Windows Server 장애 조치(Failover) 클러스터)에서 명명된 인스턴스로 설치한 경우 연결에서 인스턴스 이름을 추가할 수 없습니다. 이 방법은 SSAS에 고유한 반면, 클러스터형 관계형 데이터베이스 엔진의 명명된 인스턴스에는 인스턴스 이름이 포함되지 않습니다. 예를 들어, SQL-CLU의 SQL Server 네트워크 이름을 사용하여 SSAS 및 데이터베이스 엔진을 명명된 인스턴스(Contoso-Accounting)로 설치하는 경우 "SQL-CLU"를 사용하여 SSAS에 연결하고 "SQL-CLU\Contoso-Accounting"으로 데이터베이스 엔진에 연결합니다. 자세한 내용 및 예제는 [SQL Server Analysis Services를 클러스터링하는 방법](http://go.microsoft.com/fwlink/p/?LinkId=396548) 을 참조하십시오.  
  
     네트워크 부하 부산 클러스터에서 배포된 서버의 경우 NLB의 가상 서버 이름을 사용하여 연결합니다.  
  
3.  인증은 항상 Windows 인증이며, 사용자 ID는 항상 Management Studio를 통해 연결하는 Windows 사용자입니다.  
  
     연결에 성공하려면 서버 또는 서버의 데이터베이스에 액세스할 수 있는 권한이 있어야 합니다. Management Studio에서 수행하려는 대부분의 작업에는 관리 권한이 필요합니다. 연결하는 데 사용하는 계정이 서버 관리자 역할의 멤버인지 확인해야 합니다. 자세한 내용은 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)를 참조하세요.  
  
4.  **연결 속성** 을 클릭하여 특정 데이터베이스를 지정하고 제한 시간 값 또는 암호화 옵션을 설정합니다. 선택적 연결 정보에는 현재 연결에만 사용되는 연결 속성이 포함됩니다.  
  
5.  **추가 연결 매개 변수** 탭을 클릭하여 서버에 연결 대화 상자에서 사용할 수 없는 연결 속성을 설정합니다. 예를 들어 텍스트 상자에 `Roles=Reader` 를 입력할 수 있습니다.  
  
     이보다 낮은 수준의 권한을 가진 역할을 통해 연결하면 해당 역할이 적용될 때 데이터베이스 동작을 테스트할 수 있습니다.  
  
    ```  
    Provider=MSOLAP; Data Source=SERVERNAME; Initial Catalog=AdventureWorks2012; Roles=READER  
    ```  
  
##  <a name="bkmk_excel"></a> Excel을 사용하여 연결  
 Microsoft Excel은 일반적으로 비즈니스 데이터를 분석하는 데 사용됩니다. Excel 설치 시 Office는 네트워크 서버의 데이터를 보다 쉽게 사용할 수 있도록 Analysis Services OLE DB 공급자(MSOLAP DLL), ADOMD.NET 및 기타 데이터 공급자를 설치합니다. 이전 버전의 Excel과 함께 최신 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 사용 중인 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 연결하는 각 워크스테이션에서 최신 데이터 공급자를 설치해야 할 수 있습니다. 자세한 내용은 [Analysis Services 연결에 사용되는 데이터 공급자](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md) 를 참조하세요.  
  
 Analysis Services 큐브 또는 테이블 형식 model 데이터베이스에 대한 연결을 설정하면 Excel에서 나중에 사용할 수 있도록 연결 정보를 .odc 파일에 저장합니다. 연결은 현재 Windows 사용자의 보안 컨텍스트에서 수행됩니다. 연결에 성공하려면 사용자 계정에 데이터베이스에 대한 읽기 권한이 있어야 합니다.  
  
 Excel 통합 문서에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터를 사용하는 경우 쿼리 요청 기간 동안 연결이 유지됩니다. 이로 인해 Excel에서 쿼리 작업을 모니터링할 때 각 세션에 대해 매우 짧은 시간 동안 유지되는 수많은 연결이 표시될 가능성이 많아집니다.  
  
 특정 사용자 ID로 Excel을 시작하여 사용 권한을 테스트할 수 있습니다.  
  
 Shift 키를 누른 상태에서 **Excel** 바로 가기를 마우스 오른쪽 단추로 클릭하여 **다른 사용자로 실행** 옵션에 액세스합니다.  
  
1.  Excel의 데이터 탭에서 **기타 원본**을 클릭한 다음 **Analysis Services**를 클릭합니다. 서버 이름을 입력한 다음 쿼리할 큐브 또는 큐브 뷰를 선택합니다.  
  
     부하 분산된 클러스터에 배포된 서버의 경우 클러스터에 할당된 가상 서버 이름을 사용합니다.  
  
2.  Excel에서 연결을 설정할 때 데이터 연결 마법사의 마지막 페이지에서 Excel 서비스에 대한 인증 설정을 지정할 수 있습니다. 이러한 설정은 Excel 서비스가 있는 SharePoint 서버에 업로드해야 하는 통합 문서의 속성을 설정하는 데 사용됩니다. 설정은 데이터 새로 고침 작업에 사용됩니다. 옵션에는 **Windows 인증**, **SSS(보안 저장소 서비스)** 및 **없음**이 있습니다.  
  
     **없음**은 사용하지 않는 것이 좋습니다. Analysis Services에서는 HTTP 액세스용으로 구성된 서버에 연결하지 않는 한 연결 문자열에서 사용자 이름 및 암호를 지정할 수 없습니다. 마찬가지로 SSS 대상 애플리케이션 ID가 Analysis Services 데이터베이스에 대한 사용자 액세스 권한이 있는 Windows 사용자 자격 증명 집합에 매핑되어 있음을 이미 알고 있지 않는 경우에는 SSS를 사용하지 마십시오. 대부분의 시나리오에서는 Excel에서 Analysis Services에 연결할 때 기본 옵션인 Windows 인증을 사용하는 것이 가장 좋습니다.  
  
 자세한 내용은 [SQL Server Analysis Services에 연결 또는 데이터 가져오기](http://go.microsoft.com/fwlink/?linkID=215150)를 참조하십시오.  
  
##  <a name="bkmk_SSDT"></a> SQL Server Data Tools를 사용하여 연결  
 SQL Server Data Tools는 Analysis Services 모델, Reporting Services 보고서 및 SSIS 패키지를 비롯한 BI 솔루션을 구축하는 데 사용됩니다. 보고서나 패키지를 작성할 때 Analysis Services에 대한 연결을 지정해야 할 수 있습니다.  
  
 다음 링크에서는 보고서 서버 프로젝트 또는 Integration Services 프로젝트에서 Analysis Services에 연결하는 방법에 대해 설명합니다.  
  
-   [MDX용 Analysis Services 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
-   [Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
> [!NOTE]  
>  SQL Server Data Tools를 사용하여 기존 Analysis Services 프로젝트에서 작업하는 경우, 로컬 또는 버전 제어 프로젝트를 사용하여 오프라인으로 연결하거나 온라인 모드로 연결하여 데이터베이스가 실행 중인 동안 Analysis Services 개체를 업데이트할 수 있습니다. 자세한 내용은 [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)을 참조하세요. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서의 연결은 대부분 프로젝트 모드로 실행되는데, 이때 프로젝트를 명시적으로 배포한 경우에만 변경 내용이 데이터베이스에 배포됩니다.  
  
##  <a name="bkmk_tshoot"></a> 연결 테스트  
 SQL Server Profiler를 사용하여 Analysis Services에 대한 연결을 모니터링할 수 있습니다. Audit Login 및 Audit Logout 이벤트는 연결의 증거를 제공합니다. ID 열은 연결이 설정되는 보안 컨텍스트를 나타냅니다.  
  
1.  Analysis Services 인스턴스에서 **SQL Server Profiler** 를 시작한 다음 새 추적을 시작합니다.  
  
2.  이벤트 선택에서 **Audit Login** 및 **Audit Logout** 이 보안 감사 섹션에서 선택되었는지 확인합니다.  
  
3.  원격 클라이언트 컴퓨터에서 애플리케이션 서비스(예: SharePoint 또는 Reporting Services)를 통해 Analysis Services에 연결합니다. Audit Login 이벤트는 Analysis Services에 연결하는 사용자의 ID를 보여 줍니다.  
  
 연결 오류는 흔히 불완전하거나 잘못된 서버 구성으로 추적됩니다. 항상 다음과 같이 서버 구성을 먼저 확인하십시오.  
  
-   원격 컴퓨터에서 서버를 ping하여 서버에서 원격 연결을 허용하는지 확인합니다.  
  
-   **서버의 방화벽 규칙이 동일한 도메인에 있는 클라이언트에서의 인바운드 연결을 허용합니다.**  
  
     SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 제외하고 원격 서버에 대한 모든 연결에서는 Analysis Services에서 수신하는 포트에 대한 액세스를 허용하도록 방화벽을 구성해야 합니다. 연결 오류가 발생한 경우 포트에 액세스할 수 있는지, 그리고 적절한 데이터베이스에 대한 사용자 권한이 부여되었는지를 확인합니다.  
  
     테스트하려면 원격 컴퓨터에서 Excel 또는 SSMS를 사용하여 Analysis Services 인스턴스에서 사용하는 IP 주소 및 포트를 지정합니다. 연결할 수 있으면 방화벽 규칙이 인스턴스에 대해 올바르며 인스턴스에서 원격 연결을 허용하는 것입니다.  
  
     또한 연결 프로토콜에 TCP/IP를 사용하는 경우 Analysis Services에서는 클라이언트 연결이 동일한 도메인이나 트러스트된 도메인에서 설정되도록 요구합니다. 연결이 보안 경계를 넘어 이동하는 경우 대부분 HTTP 액세스를 구성해야 합니다. 자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하십시오.  
  
-   특정 도구를 사용해서만 연결할 수 있습니까? 문제는 잘못된 클라이언트 라이브러리 버전일 수 있습니다. SQL Server 기능 팩 다운로드 페이지에서 클라이언트 라이브러리를 얻을 수 있습니다.  
  
 연결 실패를 해결하는 데 도움이 될 수 있는 리소스는 다음과 같습니다.  
  
 [SQL Server 2005 Analysis Services 연결 시나리오의 일반적인 연결 문제 해결](http://technet.microsoft.com/library/cc917670.aspx). 이 문서는 몇 년 전에 작성되었지만 정보와 방법은 여전히 유효합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에 연결](../../analysis-services/instances/connect-to-analysis-services.md)   
 [Analysis Services에서 지 원하는 인증 방법](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [가장](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   
 [데이터 원본 & #40; 만들기 SSAS 다차원 & #41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
