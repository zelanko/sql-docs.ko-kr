---
title: Integration Services 사용자 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- tools [Integration Services], SSIS Designer
- SSIS Designer
- SSIS, SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: d2c48cff-46f4-4c70-b1f3-c88f9b8757f3
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5eb117c2f5f81c7a9d26fc3c0b62a101e1d9fb7e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36173160"
---
# <a name="integration-services-user-interface"></a>Integration Services 사용자 인터페이스
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너 탭의 디자인 화면 외에도 사용자 인터페이스를 사용하면 패키지에 기능을 추가하고 패키지 개체의 속성을 구성하기 위한 다음 창과 대화 상자에 액세스할 수 있습니다.  
  
-   대화 상자와 창에서는 로깅 및 구성과 같은 기능을 패키지에 추가할 수 있습니다.  
  
-   사용자 지정 편집기에서는 패키지 개체의 속성을 구성할 수 있습니다. 거의 모든 유형의 컨테이너, 태스크 및 데이터 흐름에는 해당 고유 사용자 지정 편집기가 있습니다.  
  
-   일반 편집기인 **고급 편집기** 대화 상자에는 여러 데이터 흐름 구성 요소에 대한 보다 세부적인 구성 옵션이 제공됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서는 또한 환경 구성 및 패키지 사용을 위한 창과 대화 상자가 제공됩니다.  
  
## <a name="dialog-boxes-and-windows"></a>대화 상자 및 창  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 패키지를 열거나 새 패키지를 만든 다음에는 다음과 같은 대화 상자 및 창을 사용할 수 있습니다.  
  
 다음 표에서는 **SSIS** 메뉴 및 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 디자인 화면에서 사용할 수 있는 대화 상자를 보여 줍니다.  
  
|대화 상자|용도|액세스 권한|  
|----------------|-------------|------------|  
|**시작**|샘플, 자습서 및 비디오에 액세스합니다.|**제어 흐름** 탭 또는 **데이터 흐름** 탭의 디자인 화면에서 마우스 오른쪽 단추를 클릭한 다음 **시작**을 클릭합니다.<br /><br /> 새 **프로젝트를 만들 때** 시작 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 창을 자동으로 표시하려면 창의 아래쪽에서 **새 프로젝트에서 항상 표시** 를 선택합니다.|  
|**SSIS 로그 구성**|로그를 추가하고 로깅 세부 정보를 설정하여 패키지 및 해당 태스크에 대한 로깅을 구성합니다.|**SSIS** 메뉴에서 **로깅**을 클릭합니다.<br /><br /> -또는-<br /><br /> **제어 흐름** 탭의 디자인 화면에서 마우스 오른쪽 단추로 아무 곳이나 클릭한 후 **로깅**을 클릭합니다.|  
|**패키지 구성 도우미**|패키지 구성을 추가하고 편집합니다. 이 대화 상자에서 패키지 구성 마법사를 실행합니다.|**SSIS** 메뉴에서 **패키지 구성**을 클릭합니다.<br /><br /> -또는-<br /><br /> **제어 흐름** 탭의 디자인 화면에서 마우스 오른쪽 단추로 아무 곳이나 클릭한 후 **패키지 구성**을 클릭합니다.|  
|**디지털 서명**|패키지에 서명하거나 패키지에서 서명을 제거합니다.|**SSIS** 메뉴에서 **디지털 서명**을 클릭합니다.<br /><br /> -또는-<br /><br /> **제어 흐름** 탭의 디자인 화면에서 마우스 오른쪽 단추로 아무 곳이나 클릭한 후 **디지털 서명**을 클릭합니다.|  
|**중단점 설정**|태스크에 중단점을 설정하고 중단점 속성을 설정합니다.|**제어 흐름** 탭의 디자인 화면에서 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 후 **중단점 편집**을 클릭합니다. 패키지에 중단점을 설정하려면 **제어 흐름** 탭의 디자인 화면에서 마우스 오른쪽 단추로 아무 곳이나 클릭한 후 **중단점 편집**을 클릭합니다.|  
  
 **시작** 창에서는 샘플, 자습서 및 비디오에 대한 링크를 제공합니다. 추가 콘텐츠에 대한 링크를 추가하려면 현재 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에 포함된 SamplesSites.xml 파일을 수정합니다. RSS 피드 URL을 지정하는 \<GettingStartedSamples> 요소 값은 수정하지 않는 것이 좋습니다. 파일은 *\<드라이브>*:\Program Files\Microsoft SQL Server\110\DTS\Binn 폴더에 있습니다. 64비트 컴퓨터의 경우 파일은 *\<드라이브>*:\Program Files(x86)\Microsoft SQL Server\110\DTS\Binn 폴더에 있습니다.  
  
 SamplesSites.xml 파일이 손상된 경우 파일에서 xml을 다음과 같은 기본 xml로 바꿉니다.  
  
 `<?xml version="1.0" ?>`  
  
 `- <SamplesSites>`  
  
 `<GettingStartedSamples>http://go.microsoft.com/fwlink/?LinkID=203147</GettingStartedSamples>`  
  
 `- <ToolboxSamples>`  
  
 `<Site>http://go.microsoft.com/fwlink/?LinkID=203286&query=SSIS%20{0}</Site>`  
  
 `</ToolboxSamples>`  
  
 `</SamplesSites>`  
  
 다음 표에서는 **SSIS** 및 **보기** 메뉴와 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 디자인 화면에서 사용할 수 있는 창을 보여 줍니다.  
  
|창|용도|액세스 권한|  
|------------|-------------|------------|  
|**변수**|사용자 지정 변수를 추가하고 관리합니다.|**SSIS** 메뉴에서 **변수**를 클릭합니다.<br /><br /> -또는-<br /><br /> **제어 흐름** 및 **데이터 흐름** 탭의 디자인 화면에서 마우스 오른쪽 단추로 아무 곳이나 클릭한 후 **변수**를 클릭합니다.<br /><br /> -또는-<br /><br /> **보기** 메뉴에서 **다른 창**을 가리킨 후 **변수**를 클릭합니다.|  
|**이벤트 로그**|런타임에 로그 항목을 봅니다.|**SSIS** 메뉴에서 **이벤트 로그**를 클릭합니다.<br /><br /> -또는-<br /><br /> **제어 흐름** 및 **데이터 흐름** 탭의 디자인 화면에서 마우스 오른쪽 단추로 아무 곳이나 클릭한 후 **이벤트 로그**를 클릭합니다.<br /><br /> -또는-<br /><br /> **보기** 메뉴에서 **다른 창**을 가리킨 후 **이벤트 로그**를 클릭합니다.|  
  
## <a name="custom-editors"></a>사용자 지정 편집기  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 대부분의 컨테이너, 태스크, 원본, 변환 및 대상에 대한 사용자 지정 대화 상자를 제공합니다.  
  
 다음 표에서는 사용자 지정 대화 상자에 액세스하는 방법에 대해 설명합니다.  
  
|편집기 유형|액세스 권한|  
|-----------------|------------|  
|컨테이너. 자세한 내용은 [Integration Services 컨테이너](control-flow/integration-services-containers.md)를 참조하세요.|**제어 흐름** 탭의 디자인 화면에서 컨테이너를 두 번 클릭합니다.|  
|태스크. 자세한 내용은 [Integration Services Tasks](control-flow/integration-services-tasks.md)을(를) 참조하세요.|**제어 흐름** 탭의 디자인 화면에서 태스크를 두 번 클릭합니다.|  
|원본.|**데이터 흐름** 탭의 디자인 화면에서 원본을 두 번 클릭합니다.|  
|변환. 자세한 내용은 [Integration Services Transformations](data-flow/transformations/integration-services-transformations.md)을 참조하세요.|**데이터 흐름** 탭의 디자인 화면에서 변환을 두 번 클릭합니다.|  
|대상.|**데이터 흐름** 탭의 디자인 화면에서 대상을 두 번 클릭합니다.|  
  
## <a name="advanced-editor"></a>고급 편집기  
 **고급 편집기** 대화 상자는 데이터 흐름 구성 요소를 구성하기 위한 사용자 인터페이스입니다. 여기에는 구성 요소 속성이 일반적인 레이아웃으로 표시됩니다. 여러 입력이 포함된 **변환에서는** 고급 편집기 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 대화 상자를 사용할 수 없습니다.  
  
 이 편집기를 열려면 **속성** 창에서 **고급 편집기 표시** 를 클릭하거나 데이터 흐름 구성 요소를 마우스 오른쪽 단추로 클릭한 후 **고급 편집기 표시**를 클릭합니다.  
  
 사용자 지정 원본, 변환 또는 대상을 만들 때 사용자 지정 사용자 인터페이스를 작성하지 않으려면 **고급 편집기** 를 대신 사용하면 됩니다.  
  
## <a name="sql-server-data-tools-features"></a>SQL Server Data Tools 기능  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에 사용할 수 있는 창, 대화 상자 및 메뉴 옵션이 제공됩니다.  
  
 다음은 사용 가능한 창과 메뉴에 대한 요약 설명입니다.  
  
-   **솔루션 탐색기** 창에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에서 개발 중인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 비롯한 프로젝트와 프로젝트 파일이 나열됩니다.  
  
     프로젝트에 포함된 패키지를 이름을 기준으로 정렬하려면 **SSIS 패키지** 노드를 마우스 오른쪽 단추로 클릭한 다음 **이름순 정렬**을 클릭합니다.  
  
-   **도구 상자** 창에는 제어 흐름 및 데이터 흐름을 작성하기 위한 제어 흐름 및 데이터 흐름 항목이 나열됩니다.  
  
-   **속성** 창에는 개체 속성이 나열됩니다.  
  
-   **서식** 메뉴에는 패키지의 컨트롤 크기 조정 및 정렬을 위한 옵션이 제공됩니다.  
  
-   **편집** 메뉴에는 디자인 화면에서 개체를 복사하기 위한 복사 및 붙여넣기 기능이 제공됩니다.  
  
-   **보기** 메뉴에는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에 그래픽적으로 표시된 개체를 수정하기 위한 옵션이 제공됩니다.  
  
 추가 창 및 메뉴에 대한 자세한 내용은 Visual Studio 설명서를 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 패키지를 만드는 방법은 [SQL Server Data Tools에서 패키지 만들기](create-packages-in-sql-server-data-tools.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [SSIS 디자이너](ssis-designer.md)  
  
  