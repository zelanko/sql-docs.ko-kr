---
title: "Analysis Services 프로젝트 만들기 (SSDT) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Analysis Services]
- templates [Analysis Services], projects
- projects [Analysis Services], creating
- projects [Analysis Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, defining projects [Analysis Services]
- items [Analysis Services]
ms.assetid: d00913b0-cd6d-4de0-a1e7-4ce86fcc078d
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 25b3c2bf3c86f69e9333b5e62541bbcfbbc877ea
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-an-analysis-services-project-ssdt"></a>Analysis Services 프로젝트 만들기(SSDT)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 템플릿을 사용하거나 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 데이터베이스 가져오기 마법사를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 내용을 읽어서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 정의할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에 현재 로드된 솔루션이 없는 경우 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 만들면 자동으로 새 솔루션이 생성됩니다. 로드된 솔루션이 있으면 새로운 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트가 기존 솔루션에 추가됩니다. 솔루션을 개발하는 가장 좋은 방법은 응용 프로그램 데이터 유형별로 다른 개별 프로젝트를 만들어 프로젝트와 관련 있는 단일 솔루션을 사용하는 것입니다. 예를 들어 동일한 비즈니스 응용 프로그램에 사용되는 Integration Services 패키지, Analysis Services 데이터베이스 및 Reporting Services 보고서에 대해 별도의 프로젝트를 포함하는 단일 솔루션을 사용할 수 있습니다.  
  
 Analysis Services 프로젝트는 단일 Analysis Services 데이터베이스에 사용되는 개체를 포함합니다. 프로젝트의 배포 속성은 프로젝트 메타데이터가 인스턴스화된 개체로 배포될 서버 및 데이터베이스 이름을 지정합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [Analysis Services 프로젝트 템플릿을 사용하여 새 프로젝트 만들기](#bkmk_NewUsingTemplate)  
  
 [기존 Analysis Services 데이터베이스를 사용하여 새 프로젝트 만들기](#bkmk_NewUsingWizard)  
  
 [기존 솔루션에 Analysis Services 프로젝트 추가](#bkmk_AddtoExistingSolution)  
  
 [솔루션 작성 및 배포](#bkmk_buildDeploy)  
  
 [Analysis Services 프로젝트 폴더](#bkmk_ProjectFolders)  
  
 [Analysis Services 파일 형식](#bkmk_FileTypes)  
  
 [Analysis Services 항목 템플릿](#bkmk_ItemTemplates)  
  
##  <a name="bkmk_NewUsingTemplate"></a> Analysis Services 프로젝트 템플릿을 사용하여 새 프로젝트 만들기  
 다음 지침에 따라 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스로 배포할 수 있는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 정의하는 빈 프로젝트를 만듭니다.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **파일**을 클릭하고 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다. **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **비즈니스 인텔리전스 프로젝트**를 선택합니다.  
  
2.  **새 프로젝트** 대화 상자의 **Visual Studio에 설치되어 있는 템플릿** 범주에서 **Analysis Services 프로젝트**를 선택합니다.  
  
3.  **이름** 입력란에 프로젝트 이름을 입력합니다. 입력한 이름이 기본 데이터베이스 이름으로 사용됩니다.  
  
4.  **위치** 드롭다운 목록에서 프로젝트 파일을 저장할 폴더를 입력 또는 선택하거나 **찾아보기** 를 클릭하여 폴더를 선택합니다.  
  
5.  기존 솔루션에 새 프로젝트를 추가하려면 **솔루션** 드롭다운 목록에서 **솔루션에 추가**를 선택합니다.  
  
     —또는—  
  
     새 솔루션을 만들려면 **솔루션** 드롭다운 목록에서 **새 솔루션 만들기**를 선택합니다. 새 솔루션용 폴더를 새로 만들려면 **솔루션용 디렉터리 만들기**를 선택합니다. **솔루션 이름**에 새 솔루션의 이름을 입력합니다.  
  
6.  **확인**을 클릭합니다.  
  
##  <a name="bkmk_NewUsingWizard"></a> 기존 Analysis Services 데이터베이스를 사용하여 새 프로젝트 만들기  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 가져오기 마법사를 사용하여 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 개체를 기반으로 프로젝트를 만듭니다. 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 기반으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 정의하면 해당 데이터베이스에 대한 메타데이터가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트에서 열립니다. 원래 개체에 영향을 주지 않고 프로젝트 내에서 이러한 개체를 수정한 다음 동일한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스(배포 속성에 해당 데이터베이스가 지정된 경우)에 배포하거나 비교 테스트를 위해 새로 만든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 배포할 수 있습니다. 변경 내용을 배포해야만 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 변경 내용이 적용됩니다.  
  
 또한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 가져오기 템플릿을 사용하면 원래 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트가 배포되어 직접 변경된 프로덕션 데이터베이스에서 프로젝트를 만들 수 있습니다.  
  
 프로젝트를 처리하거나 배포하기 전에 데이터 원본에 지정된 데이터 공급자를 변경해야 할 수 있습니다. 사용 중인 SQL Server 소프트웨어가 데이터베이스를 만드는 데 사용된 소프트웨어보다 최신 버전인 경우 프로젝트에 지정된 데이터 공급자가 컴퓨터에 설치되지 않을 수 있습니다. 처리 과정에서 서비스 계정은 Analysis Services 데이터베이스에서 데이터를 검색하는 데 사용됩니다. 데이터베이스가 원격 서버에 있을 경우 로컬 서비스에 해당 서버에 대한 처리 및 읽기 권한이 있는지 확인하십시오.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **파일**을 클릭하고 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다. **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **비즈니스 인텔리전스 프로젝트**를 선택합니다.  
  
2.  **새 프로젝트** 대화 상자의 **Visual Studio에 설치되어 있는 템플릿** 범주에서 **Analysis Services 데이터베이스 가져오기**를 선택합니다.  
  
3.  파일의 이름과 위치를 포함하여 프로젝트 및 솔루션에 대한 속성 정보를 입력합니다. **확인**을 클릭합니다.  
  
4.  **Analysis Services 데이터베이스 가져오기 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
5.  **원본 데이터베이스** 페이지에서 마법사가 내용을 추출하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 만들 서버와 데이터베이스를 지정한 후 **다음**을 클릭합니다.  
  
     지원되는 데이터베이스에는 Analysis Services의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]버전에 생성된 데이터베이스가 포함됩니다.  
  
     데이터베이스 이름을 입력하거나 서버를 쿼리하여 서버의 기존 데이터베이스를 볼 수 있습니다. 데이터베이스가 원격 서버 또는 프로덕션 서버에 있는 경우 데이터베이스 읽기 권한을 요청해야 할 수 있습니다. 방화벽 구성 설정은 데이터베이스에 대한 액세스를 더욱 제한할 수 있습니다. 데이터베이스에 연결하는 중에 오류가 발생하는 경우 먼저 사용 권한과 방화벽 설정을 확인하십시오.  
  
6.  마법사가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 내용 추출을 완료하면 **마법사 완료** 페이지에서 **마침** 을 클릭합니다.  
  
7.  솔루션 탐색기 창을 열어 프로젝트 내용을 봅니다.  
  
##  <a name="bkmk_AddtoExistingSolution"></a> 기존 솔루션에 Analysis Services 프로젝트 추가  
 비즈니스 응용 프로그램의 모든 원본 파일을 포함하는 솔루션이 이미 있는 경우 해당 솔루션에 새 Analysis Services 프로젝트를 추가할 수 있습니다.  
  
 솔루션에 기존 프로젝트를 추가하면 프로젝트가 솔루션에 연결되지만 복사되지는 않습니다. Analysis Services 프로젝트를 다른 솔루션에서 만들었을 경우 프로젝트 파일이 프로젝트를 만든 원본 솔루션과 함께 유지됩니다. 따라서 어느 솔루션을 통해 프로젝트를 변경하더라도 변경 사항이 동일한 원본 파일 집합에 적용됩니다. 이 동작을 원하지 않는 경우 프로젝트 파일을 새 솔루션 폴더로 복사 또는 이동한 다음 솔루션에 프로젝트를 추가해야 합니다.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 솔루션을 엽니다. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **기존 프로젝트** 를 클릭하여 추가할 프로젝트를 선택합니다.  
  
2.  솔루션에 추가할 .dwproj 파일을 선택합니다.  
  
##  <a name="bkmk_buildDeploy"></a> 솔루션 작성 및 배포  
 기본적으로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 로컬 컴퓨터에 있는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 기본 인스턴스에 프로젝트를 배포합니다. **프로젝트에 대한** 속성 페이지 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 대화 상자를 사용하여 **서버** 구성 속성을 변경하면 이 배포 대상을 변경할 수 있습니다.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서는 솔루션을 배포할 때 배포 스크립트에서 변경한 개체 및 종속 개체만 처리합니다. **프로젝트에 대한** 속성 페이지 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 대화 상자를 사용하여 처리 옵션 구성 속성을 변경하면 이 기능을 변경할 수 있습니다.  
  
 솔루션을 빌드한 다음 테스트용 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 배포합니다. 솔루션을 빌드하면 프로젝트의 개체 정의 및 종속성의 유효성을 검사하고 배포 스크립트를 생성합니다. 솔루션을 배포할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 엔진을 사용하여 배포 스크립트를 지정된 인스턴스로 보냅니다.  
  
 프로젝트를 배포한 후 배포된 데이터베이스를 검토하여 테스트합니다. 그런 다음 프로젝트가 완료될 때까지 개체 정의를 수정하고 작성하여 다시 배포할 수 있습니다.  
  
 프로젝트가 완료되면 배포 마법사를 사용하여 솔루션 빌드 시 생성된 배포 스크립트를 최종 테스트, 준비 및 배포용 대상 인스턴스에 배포할 수 있습니다.  
  
##  <a name="bkmk_ProjectFolders"></a> Analysis Services 프로젝트 폴더  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에는 다음 폴더가 있으며 이러한 폴더는 프로젝트에 포함된 항목을 구성하는 데 사용됩니다.  
  
|Folder|Description|  
|------------|-----------------|  
|데이터 원본|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 데이터 원본을 포함합니다. 데이터 원본 마법사를 사용하여 이러한 개체를 만들고 데이터 원본 디자이너에서 편집합니다.|  
|데이터 원본 뷰|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 데이터 원본 뷰를 포함합니다. 데이터 원본 뷰 마법사를 사용하여 이러한 개체를 만들고 데이터 원본 뷰 디자이너에서 편집합니다.|  
|큐브|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 큐브를 포함합니다. 큐브 마법사를 사용하여 이러한 개체를 만들고 큐브 디자이너에서 편집합니다.|  
|차원|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 차원을 포함합니다. 차원 마법사 또는 큐브 마법사를 사용하여 이러한 개체를 만들고 차원 디자이너에서 편집합니다.|  
|마이닝 구조|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 마이닝 구조를 포함합니다. 마이닝 모델 마법사를 사용하여 이러한 개체를 만들고 마이닝 모델 디자이너에서 편집합니다.|  
|역할|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 데이터베이스 역할을 포함합니다. 역할 디자이너에서 역할을 만들고 관리합니다.|  
|어셈블리|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 프로젝트의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .NET Framework 어셈블리 및 COM 라이브러리에 대한 참조를 포함합니다. **참조 추가** 대화 상자를 사용하여 참조를 만듭니다.|  
|기타|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 파일 유형을 제외한 모든 파일 유형을 포함합니다. 이 폴더를 사용하여 프로젝트에 대한 메모를 포함하는 텍스트 파일과 같은 기타 파일을 추가할 수 있습니다.|  
  
##  <a name="bkmk_FileTypes"></a> Analysis Services 파일 형식  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 솔루션은 솔루션에 포함시킨 프로젝트에 따라 그리고 해당 솔루션의 각 프로젝트에 포함시킨 항목에 따라 여러 파일 형식을 포함할 수 있습니다. 일반적으로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 솔루션의 각 프로젝트에 대한 파일은 솔루션 폴더에 저장되며 각 프로젝트에 대해 별도의 폴더에 저장됩니다.  
  
> [!NOTE]  
>  개체에 대한 파일을 프로젝트 폴더에 복사하면 이 개체는 해당 프로젝트에 추가되지 않습니다. 기존 개체 정의를 프로젝트에 추가하려면 **에서 프로젝트의 상황에 맞는 메뉴에서** 추가 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 명령을 사용해야 합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 프로젝트 폴더는 다음 표에 나열된 파일 유형을 포함할 수 있습니다.  
  
|파일 유형|Description|  
|---------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 정의 파일(.dwproj)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 정의 및 포함된 항목, 구성 및 어셈블리 참조에 대한 메타데이터를 포함합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 사용자 설정(.dwproj.user)|특정 사용자의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 구성 정보를 포함합니다.|  
|데이터 원본 파일(.ds)|데이터 원본에 대한 메타데이터를 정의하는 ASSL( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 요소를 포함합니다.|  
|데이터 원본 뷰 파일(.dsv)|데이터 원본 뷰에 대한 메타데이터를 정의하는 ASSL 요소를 포함합니다.|  
|큐브 파일(.cube)|측정값 그룹, 측정값 및 큐브 차원을 비롯하여 큐브에 대한 메타데이터를 정의하는 ASSL 요소를 포함합니다.|  
|파티션 파일(.partitions)|지정한 큐브의 파티션에 대한 메타데이터를 정의하는 ASSL 요소를 포함합니다.|  
|차원 파일(.dim)|데이터베이스 차원에 대한 메타데이터를 정의하는 ASSL 요소를 포함합니다.|  
|마이닝 구조 파일(.dmm)|마이닝 구조 및 관련 마이닝 모델에 대한 메타데이터를 정의하는 ASSL 요소를 포함합니다.|  
|데이터베이스 파일(.database)|계정 유형, 번역 및 데이터베이스 권한을 비롯하여 데이터베이스에 대한 메타데이터를 정의하는 ASSL 요소를 포함합니다.|  
|데이터베이스 역할 파일(.role)|역할 멤버를 비롯하여 데이터베이스 역할에 대한 메타데이터를 정의하는 ASSL 요소를 포함합니다.|  
  
##  <a name="bkmk_ItemTemplates"></a> Analysis Services 항목 템플릿  
 **새 항목 추가** 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 새 항목을 추가하는 경우 지정한 동작을 수행하는 방법을 보여 주는 미리 정의된 스크립트 또는 문인 항목 템플릿을 사용할 수 있습니다.  
  
 다음 표에 나열된 항목 템플릿은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 새 항목 추가 **대화 상자의** 프로젝트 항목 범주에서 사용할 수 있습니다.  
  
|범주|항목 템플릿|Description|  
|--------------|-------------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 항목|Cube|큐브 마법사를 시작하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 새 큐브를 추가합니다.|  
||데이터 원본|데이터 원본 마법사를 시작하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 새 데이터 원본을 추가합니다.|  
||데이터 원본 뷰|데이터 원본 뷰 마법사를 시작하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 새 데이터 원본 뷰를 추가합니다.|  
||데이터베이스 역할|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 새 데이터베이스 역할을 추가한 다음 새 데이터베이스 역할의 역할 디자이너를 표시합니다.|  
||차원|차원 마법사를 시작하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 새 데이터베이스 차원을 추가합니다.|  
||마이닝 구조|데이터 마이닝 마법사를 시작하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 새 마이닝 구조 및 관련 마이닝 모델을 추가합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 프로젝트 속성 구성&#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [Analysis Services 프로젝트 빌드&#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  

