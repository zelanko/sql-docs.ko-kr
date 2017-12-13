---
title: "샘플 데이터 및 프로젝트 설치 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: fc475b25-cbb2-408a-901f-9299299538c5
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: e0372941de7d139b7e91f8e03a3ce6b903d05a9f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="install-sample-data-and-projects"></a>샘플 데이터 및 프로젝트 설치 
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]지침 및이 항목에서 제공 하는 링크를 사용 하 여 모든 Analysis Services 자습서에 사용 되는 데이터 및 프로젝트 파일을 설치할 수 있습니다.  
  
## <a name="step-1-install-sql-server-software"></a>1단계: SQL Server 소프트웨어 설치  
이 자습서의 단원에서는 다음 소프트웨어가 설치되어 있다고 가정합니다. 다음 소프트웨어는 모두 SQL Server 설치 미디어를 사용하여 설치됩니다. 배포를 간단하게 하기 위해 모든 기능을 단일 컴퓨터에 설치할 수도 있습니다. 이러한 기능을 설치하려면 SQL Server 설치 프로그램을 실행하고 기능 선택 페이지에서 해당 기능을 선택합니다. 자세한 내용은 [설치 마법사에서 SQL Server 2016 설치&#40;설치 프로그램&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)를 참조하세요.  
  
-   데이터베이스 엔진  
  
-   Analysis Services  
  
    Analysis Services는 Evaluation, Enterprise, Business Intelligence, Standard 버전에서만 사용할 수 있습니다.  
  
    SQL Server Express 버전에는 Analysis Services가 포함되어 있지 않습니다. 소프트웨어를 무료로 사용해 보려면[평가판 버전을 다운로드하세요](http://go.microsoft.com/fwlink/?LinkId=392824) .  
  
    기본적으로 Analysis Services는 다차원 인스턴스로 설치되며 설치 마법사의 서버 구성 페이지에서 테이블 형식 서버 모드를 선택하여 재정의할 수 있습니다. 두 서버 모드를 모두 실행하려는 경우 동일한 컴퓨터의 SQL Server 설치 프로그램을 다시 실행하여 다른 모드에서 Analysis Services의 두 번째 인스턴스를 실행하십시오.  
  
-   SQL Server Management Studio  
  
필요에 따라 자습서를 진행할 때 Excel을 설치하여 다차원 데이터를 검색하는 것이 좋습니다. Excel을 설치하면 작성하려는 큐브에 연결되어 있는 피벗 테이블 필드를 사용하여 Excel을 시작하는 **Excel에서 분석** 기능이 사용하도록 설정됩니다. 데이터와 상호 작용할 수 있도록 피벗 보고서를 빨리 작성할 수 있으므로 Excel을 사용하여 데이터를 검색하는 것이 좋습니다.  
  
또는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 기본 제공되는 MDX 쿼리 디자이너를 사용하여 데이터를 검색할 수 있습니다. 쿼리 디자이너는 데이터가 플랫 행 집합으로 제공된다는 점을 제외하면 동일한 데이터를 반환합니다.  
  
## <a name="step-2-download-sql-server-data-tools-for-visual-studio-2015"></a>2단계: Visual Studio 2015용 SQL Server Data Tools 다운로드  
이 릴리스에서는 SQL Server Data Tools가 다른 SQL Server 기능과 별도로 다운로드 및 설치됩니다. BI 모델 및 보고서를 만드는 데 사용되는 디자이너 및 프로젝트 템플릿이 무료 웹 다운로드로 제공됩니다.  
  
-   [SQL Server Data Tools 다운로드](http://go.microsoft.com/fwlink/?LinkID=827542). 파일은 Downloads 폴더에 저장됩니다. 설치 프로그램을 실행하여 도구를 설치합니다.  
  
    컴퓨터를 다시 부팅하여 설치를 완료합니다.  
  
## <a name="step-3-install-databases"></a>3단계: 데이터베이스 설치  
Analysis Services 다차원 모델에서는 관계형 데이터베이스 관리 시스템에서 가져오는 트랜잭션 데이터를 사용합니다. 이 자습서에서는 다음 관계형 데이터베이스를 데이터 원본으로 사용합니다.  
  
-   **AdventureWorksDW2012** – 데이터베이스 엔진 인스턴스에서 실행되는 관계형 데이터 웨어하우스입니다. 이 데이터베이스는 자습서 전체에서 작성하고 배포하는 Analysis Services 데이터베이스 및 프로젝트에 사용할 원본 데이터를 제공합니다.  
  
    [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 이 예제 데이터베이스를 사용할 수 있습니다.  
  
이 데이터베이스를 설치하려면 다음을 수행합니다.  
  
1.  codeplex의 제품 샘플 페이지에서 [AdventureWorkDW2012](http://go.microsoft.com/fwlink/p/?LinkID=221770) 데이터베이스를 다운로드합니다.  
  
    데이터베이스 파일이름은 AdvntureWorksDW2012_Data.mdf입니다. 이 파일은 컴퓨터의 Downloads 폴더에 있어야 합니다.  
  
2.  AdventureWorksDW2012_Data.mdf 파일을 로컬 SQL Server 데이터베이스 엔진 인스턴스의 데이터 디렉터리로 복사합니다. 기본적으로 이 파일은 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data에 있습니다.  
  
3.  Microsoft SQL Server Management Studio를 시작하고 데이터베이스 엔진 인스턴스에 연결합니다.  
  
4.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **연결**을 클릭합니다.  
  
5.  **추가**를 클릭합니다.  
  
6.  **AdventureWorksDW2012_Data.mdf** 데이터베이스 파일을 선택하고 **확인**을 클릭합니다. 이 파일이 목록에 없으면 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data 폴더에 해당 파일이 있는지 확인합니다.  
  
7.  데이터베이스 정보에서 로그 파일 항목을 제거합니다. 예제에는 로그 파일이 없지만 설치 프로그램에서는 로그 파일이 있다고 가정합니다. 데이터베이스를 연결하면 자동으로 새 로그 파일이 만들어집니다. 로그 파일을 선택하고 **제거**를 클릭한 다음 **확인** 을 클릭하여 주 데이터베이스 파일만 연결합니다.  
  
## <a name="step-4-grant-database-permissions"></a>4단계: 데이터베이스 사용 권한 부여  
예제 프로젝트에서는 데이터를 가져오거나 처리하는 데 사용되는 보안 컨텍스트를 지정하는 데이터 원본 가장을 사용합니다. 기본적으로 가장 설정은 데이터 액세스에 사용할 Analysis Services 서비스 계정을 지정합니다. 이 기본 설정을 사용하려면 Analysis Services를 실행하는 데 사용되는 서비스 계정에 **AdventureWorksDW2012** 데이터베이스에 대한 데이터 읽기 권한이 있는지 확인해야 합니다.  
  
> [!NOTE]  
> 학습 목적으로 기본 서비스 계정 가장 옵션을 사용하고 SQL Server의 서비스 계정에 데이터 판독기 사용 권한을 부여하는 것이 좋습니다. 다른 가장 옵션을 사용할 수 있는 경우에도 모든 옵션이 작업 처리에 적합하지는 않습니다. 특히 현재 사용자의 자격 증명 사용을 위한 옵션은 처리에 지원되지 않습니다.  
  
1.  서비스 계정을 확인합니다. SQL Server 구성 관리자 또는 서비스 콘솔 응용 프로그램을 사용하여 계정 정보를 볼 수 있습니다. 기본 계정을 사용하여 Analysis Services를 기본 인스턴스로 설치한 경우 서비스가 **NT Service\MSSQLServerOLAPService**로 실행됩니다.  
  
2.  Management Studio에서 데이터베이스 엔진 인스턴스에 연결합니다.  
  
3.  보안 폴더를 확장하고 로그인을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.  
  
4.  일반 페이지의 로그인 이름에 **NT Service\MSSQLServerOLAPService** 또는 서비스를 실행할 계정을 입력합니다.  
  
5.  **사용자 매핑**을 클릭합니다.  
  
6.  **AdventureWorksDW2012** 데이터베이스 옆에 있는 확인란을 선택합니다. 역할 멤버 자격에 **db_datareader** 및 **public**이 자동으로 포함됩니다. **확인** 을 클릭하여 기본값을 적용합니다.  
  
## <a name="step-5-install-projects"></a>5단계: 프로젝트 설치  
이 자습서에는 작업 결과를 완료된 프로젝트와 비교하거나 시퀀스에서 더 많이 진행된 단원을 시작할 수 있도록 예제 프로젝트가 포함되어 있습니다.  
  
4단원용 프로젝트 파일은 해당 단원뿐 아니라 이후 모든 단원의 기초를 제공하므로 특히 중요합니다. 자습서의 단계를 수행하면 완료된 프로젝트 파일의 정확한 복사본이 생성되는 이전 프로젝트 파일과 달리 4단원의 예제 프로젝트에는 1단원부터 3단원까지 작성한 모델에는 없는 새로운 모델 정보가 포함되어 있습니다. 4단원에서는 다음 다운로드를 통해 사용할 수 있는 예제 프로젝트 파일을 사용하여 시작한다고 가정합니다.  
  
1.  codeplex의 제품 샘플 페이지에서 [Analysis Services Tutorial SQL Server 2012](http://go.microsoft.com/fwlink/p/?LinkID=221866) 를 다운로드합니다.  
  
    2012 자습서를 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 릴리스에 사용할 수 있습니다.  
  
    "Analysis Services Tutorial SQL Server 2012.zip" 파일은 컴퓨터의 Downloads 폴더에 저장됩니다.  
  
2.  .zip 파일을 루트 드라이브 바로 아래 폴더(예: C:\Tutorial)로 이동합니다. 이 단계를 수행하면 Downloads 폴더에 파일 압축을 풀 경우 가끔 발생하는 "경로가 너무 길다"는 의미의 오류가 줄어듭니다.  
  
3.  이 파일을 마우스 오른쪽 단추로 클릭하고 **압축 풀기**를 선택하여 샘플 프로젝트의 압축을 풉니다. 파일 압축을 푼 후 다음 프로젝트를 컴퓨터에 설치해야 합니다.  
  
    -   1단원 완료  
  
    -   2단원 완료  
  
    -   3단원 완료  
  
    -   4단원 완료  
  
    -   4단원 시작  
  
    -   5단원 완료  
  
    -   6단원 완료  
  
    -   7단원 완료  
  
    -   8단원 완료  
  
    -   9단원 완료  
  
    -   10단원 완료  
  
4.  이러한 파일에서 읽기 전용 권한을 제거합니다. 부모 폴더인 "Analysis Services Tutorial SQL Server 2012"를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 후 **읽기 전용**확인란의 선택을 취소합니다. **확인**을 클릭합니다. 이 폴더, 하위 폴더 및 파일에 변경 내용을 적용합니다.  
  
5.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 시작합니다.  
  
6.  사용할 단원에 해당하는 솔루션 파일(.sln)을 엽니다. 예를 들어 "Lesson 1 Complete" 폴더에서 Analysis Services Tutorial.sln 파일을 엽니다.  
  
7.  솔루션을 배포하여 데이터베이스 사용 권한과 서버 위치 정보가 올바르게 설정되어 있는지 확인합니다.  
  
    Analysis Services와 데이터베이스 엔진이 기본 인스턴스(MSSQLServer)로 설치되어 있고 모든 소프트웨어가 같은 컴퓨터에서 실행되고 있는 경우 빌드 메뉴에서 **솔루션 배포** 를 클릭하여 샘플 프로젝트를 빌드하고 해당 프로젝트를 로컬 Analysis Services 인스턴스에 배포할 수 있습니다. 배포하는 중에 로컬 데이터베이스 엔진 인스턴스의 **AdventureWorksDW2012** 데이터베이스에서 데이터를 처리하거나 가져옵니다. 데이터베이스 엔진에서 가져온 데이터가 포함된 Analysis Services 인스턴스에서 새 Analysis Services 데이터베이스가 만들어집니다.  
  
    오류가 발생하는 경우 데이터베이스 사용 권한을 설정하는 이전 단계를 검토합니다. 또한 서버 이름을 변경해야 할 수도 있습니다. 기본 서버 이름은 localhost입니다. 서버가 원격 프로그램에 또는 명명된 인스턴스로 설치된 경우 설치에 유효한 서버 이름을 사용하도록 기본값을 재정의해야 합니다. 또한 서버가 원격 컴퓨터에 있는 경우 서버에 대한 액세스를 허용하도록 Windows 방화벽을 구성해야 할 수 있습니다.  
  
    데이터베이스 엔진에 연결하기 위한 서버 이름이 다차원 솔루션(Adventure Works 자습서)의 데이터 원본 개체에 지정되며 솔루션 탐색기에 표시됩니다.  
  
    Analysis Services에 연결하기 위한 서버 이름이 프로젝트 속성 페이지의 배포 탭에 지정되며 솔루션 탐색기에 표시됩니다.  
  
8.  SQL Server Management Studio에서 Analysis Services에 연결합니다. 서버에서 **Analysis Services 자습서** 라는 데이터베이스가 실행되고 있는지 확인합니다.  
  
## <a name="next-step"></a>다음 단계  
이제 자습서를 사용할 준비가 되었습니다. 시작하는 방법에 대한 자세한 내용은 [다차원 모델링&#40;Adventure Works 자습서&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[설치 마법사에서 SQL Server 2016 설치&#40;설치 프로그램&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
[Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configure the Windows Firewall to Allow SQL Server Access](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
  
