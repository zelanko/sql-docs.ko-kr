---
title: 샘플 데이터 및 프로젝트 설치 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0ec266a98e3a27dd277ccd9f790ae73d1793ec38
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="install-sample-data-and-multidimensional-projects"></a>샘플 데이터 및 다차원 프로젝트 설치 
[!INCLUDE[ssas-appliesto-sqlas-all](../includes/ssas-appliesto-sqlas-all.md)]

지침과이 문서에서 제공 하는 링크를 사용 하 여 Analysis Services 자습서에 사용 되는 데이터 및 프로젝트 파일을 설치 합니다. 
  
## <a name="step-1-install-prerequisites"></a>1 단계: 필수 구성 요소 설치 
이 자습서의 단원에서는 다음 소프트웨어가 설치되어 있다고 가정합니다. 단일 컴퓨터에서 모든 기능을 설치할 수 있습니다. 이러한 기능을 설치하려면 SQL Server 설치 프로그램을 실행하고 기능 선택 페이지에서 해당 기능을 선택합니다.  
  
-   SQL Server 데이터베이스 엔진  
  
-   SQL Server Analysis Services (SSAS) 
  
    Analysis Services는 Evaluation, Enterprise, Business Intelligence, Standard 버전에서만 사용할 수 있습니다. 다차원 모델은 Azure Analysis Services에서 지원 되지 않습니다.
  
    기본적으로 Analysis Services 2016 이상 설치 마법사의 구성 페이지는 서버에서 다차원 서버 모드를 선택 하 여 재정의할 수는 테이블 형식 인스턴스로 설치 됩니다.
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>2 단계: 다운로드 하 여 개발자 및 관리 도구 설치
SQL Server 데이터 도구 (SSDT) Visual Studio에 대 한 다운로드 되 고 다른 SQL Server 기능에서 별도로 설치 됩니다. 또는 Visual Studio 2015에 대 한 디자이너 및 보고서와 BI 모델을 만드는 사용 되는 프로젝트 템플릿이 SSDT에 포함 된 [Nuget 패키지](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) Visual Studio 2017에 대 한 합니다.  
  
[SQL Server Data Tools 다운로드](http://go.microsoft.com/fwlink/?LinkID=827542).   

SQL Server Management Studio (SSMS) 다운로드 하 고 다른 SQL Server 기능에서 별도로 설치 됩니다.  

[SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)  

필요에 따라 자습서를 진행할 때 Excel을 설치하여 다차원 데이터를 검색하는 것이 좋습니다. Excel을 설치하면 작성하려는 큐브에 연결되어 있는 피벗 테이블 필드를 사용하여 Excel을 시작하는 **Excel에서 분석** 기능이 사용하도록 설정됩니다. 데이터와 상호 작용할 수 있도록 피벗 보고서를 빨리 작성할 수 있으므로 Excel을 사용하여 데이터를 검색하는 것이 좋습니다.  
  
또는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 기본 제공되는 MDX 쿼리 디자이너를 사용하여 데이터를 검색할 수 있습니다. 쿼리 디자이너는 데이터가 플랫 행 집합으로 제공된다는 점을 제외하면 동일한 데이터를 반환합니다.  
  
## <a name="step-3-install-databases"></a>3 단계: 설치 데이터베이스  
Analysis Services 다차원 모델에서는 관계형 데이터베이스 관리 시스템에서 가져오는 트랜잭션 데이터를 사용합니다. 이 자습서에서는 데이터 원본으로 관계형 데이터베이스를 사용 합니다.  
  
-   **AdventureWorksDW2012 이상** – 데이터베이스 엔진 인스턴스에서 실행 되는 관계형 데이터 웨어하우스입니다. Analysis Services 데이터베이스 및 빌드하고 자습서 전체에서 배포 하는 프로젝트에서 사용 하는 원래 데이터를 제공 합니다. 하지만이 자습서에서는 AdventureWorksDW2012를 사용 하는, 수행 이상 버전에서 작동 가정 합니다.
  
    이 예제 데이터베이스를 사용할 수 있습니다 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 이상. 일반에서 데이터베이스 엔진 버전에 일치 하는 샘플 데이터베이스 버전을 사용 해야 합니다.
  
데이터베이스를 설치 하려면 다음을 수행 합니다.  
  
1.  다운로드는 [AdventureWorkDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) GitHub에서 데이터베이스를 백업 합니다.  
  
2.  백업 파일을 로컬 SQL Server 데이터베이스 엔진 인스턴스의 데이터 디렉터리로 복사 합니다.
  
3.  Microsoft SQL Server Management Studio를 시작하고 데이터베이스 엔진 인스턴스에 연결합니다.  
  
4.  데이터베이스를 복원합니다.  
  
## <a name="step-4-grant-database-permissions"></a>4 단계: Grant 데이터베이스 사용 권한  
예제 프로젝트에서는 데이터를 가져오거나 처리하는 데 사용되는 보안 컨텍스트를 지정하는 데이터 원본 가장을 사용합니다. 기본적으로 가장 설정은 데이터 액세스에 사용할 Analysis Services 서비스 계정을 지정합니다. Analysis Services를 실행 하는 서비스 계정 데이터 판독기 사용에 있는지 확인 해야이 기본 설정을 사용 하 여 **AdventureWorksDW** 데이터베이스입니다.  
  
> [!NOTE]  
> 학습 목적으로 기본 서비스 계정 가장 옵션을 사용하고 SQL Server의 서비스 계정에 데이터 판독기 사용 권한을 부여하는 것이 좋습니다. 다른 가장 옵션을 사용할 수 있는 경우에도 모든 옵션이 작업 처리에 적합하지는 않습니다. 특히 현재 사용자의 자격 증명 사용을 위한 옵션은 처리에 지원되지 않습니다.  
  
1.  서비스 계정을 확인합니다. SQL Server 구성 관리자 또는 서비스 콘솔 응용 프로그램을 사용하여 계정 정보를 볼 수 있습니다. 기본 계정을 사용하여 Analysis Services를 기본 인스턴스로 설치한 경우 서비스가 **NT Service\MSSQLServerOLAPService**로 실행됩니다.  
  
2.  Management Studio에서 데이터베이스 엔진 인스턴스에 연결합니다.  
  
3.  보안 폴더를 확장하고 로그인을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.  
  
4.  일반 페이지의 로그인 이름에 **NT Service\MSSQLServerOLAPService** 또는 서비스를 실행할 계정을 입력합니다.  
  
5.  **사용자 매핑**을 클릭합니다.  
  
6.  옆의 확인란을 선택 된 **AdventureWorksDW** 데이터베이스입니다. 역할 멤버 자격에 **db_datareader** 및 **public**이 자동으로 포함됩니다. **확인** 을 클릭하여 기본값을 적용합니다.  
  
## <a name="step-5-install-projects"></a>5 단계: 설치 프로젝트  

이 자습서에는 작업 결과를 완료된 프로젝트와 비교하거나 시퀀스에서 더 많이 진행된 단원을 시작할 수 있도록 예제 프로젝트가 포함되어 있습니다.  
  
1.  다운로드는 [adventure-works-다차원-자습서-projects.zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) GitHub에서 Analysis Services 예제 페이지에 대 한 Adventure Works에서 합니다.  
  
    자습서 프로젝트에 대해 작동 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 이상.  
  
2.  .zip 파일을 루트 드라이브 바로 아래 폴더(예: C:\Tutorial)로 이동합니다. 이 단계를 수행하면 Downloads 폴더에 파일 압축을 풀 경우 가끔 발생하는 "경로가 너무 길다"는 의미의 오류가 줄어듭니다.  
  
3.  이 파일을 마우스 오른쪽 단추로 클릭하고 **압축 풀기**를 선택하여 샘플 프로젝트의 압축을 풉니다. 파일을 추출한 다음 나면 폴더 Lesson 1, 2, 3, 5, 6, 7, 8, 9, 10 완료 및 Lesson 4 Start 합니다. 
  
4.  이러한 파일에서 읽기 전용 권한을 제거합니다. 부모 폴더를 마우스 오른쪽 단추로 클릭, 선택 **속성**에 대 한 확인란의 선택을 취소 하 고 **읽기 전용**합니다. **확인**을 클릭합니다. 이 폴더, 하위 폴더 및 파일에 변경 내용을 적용합니다.  

5.  사용 중인 단원에 해당 하는 솔루션 (.sln) 파일을 엽니다. 예를 들어 "Lesson 1 Complete" 폴더에서 Analysis Services Tutorial.sln 파일을 엽니다.  
  
6.  데이터베이스 사용 권한 및 서버 위치 정보를 설정 올바르게 확인 하려면 솔루션을 배포 합니다.  
  
    Analysis Services와 데이터베이스 엔진이 기본 인스턴스(MSSQLServer)로 설치되어 있고 모든 소프트웨어가 같은 컴퓨터에서 실행되고 있는 경우 빌드 메뉴에서 **솔루션 배포** 를 클릭하여 샘플 프로젝트를 빌드하고 해당 프로젝트를 로컬 Analysis Services 인스턴스에 배포할 수 있습니다. 배포 하는 동안 데이터는 처리 (또는 가져온)에서 고 **AdventureWorksDW** 로컬 데이터베이스 엔진 인스턴스에서 데이터베이스입니다. 데이터베이스 엔진에서 검색 한 데이터를 포함 하는 Analysis Services 인스턴스에서 새 Analysis Services 데이터베이스가 만들어집니다.  
  
    오류가 발생하는 경우 데이터베이스 사용 권한을 설정하는 이전 단계를 검토합니다. 또한 서버 이름을 변경해야 할 수도 있습니다. 기본 서버 이름은 localhost입니다. 서버가 원격 프로그램에 또는 명명된 인스턴스로 설치된 경우 설치에 유효한 서버 이름을 사용하도록 기본값을 재정의해야 합니다. 또한 서버가 원격 컴퓨터에 있는 경우 서버에 대한 액세스를 허용하도록 Windows 방화벽을 구성해야 할 수 있습니다.  
  
    데이터베이스 엔진에 연결하기 위한 서버 이름이 다차원 솔루션(Adventure Works 자습서)의 데이터 원본 개체에 지정되며 솔루션 탐색기에 표시됩니다.  
  
    Analysis Services에 연결하기 위한 서버 이름이 프로젝트 속성 페이지의 배포 탭에 지정되며 솔루션 탐색기에 표시됩니다.  
  
7.  SQL Server Management Studio에서 Analysis Services에 연결합니다. 서버에서 **Analysis Services 자습서** 라는 데이터베이스가 실행되고 있는지 확인합니다.  
  
## <a name="next-step"></a>다음 단계  
이제 자습서를 사용할 준비가 되었습니다. 시작하는 방법에 대한 자세한 내용은 [다차원 모델링&#40;Adventure Works 자습서&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configure the Windows Firewall to Allow SQL Server Access](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  