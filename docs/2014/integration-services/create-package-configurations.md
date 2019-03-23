---
title: 패키지 구성 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, configurations
- Package Configurations Organizer dialog box
- SSIS packages, configurations
- Integration Services packages, configurations
- configurations [Integration Services]
- packages [Integration Services], configurations
- deploying packages [Integration Services], configurations
ms.assetid: 91ac0347-f908-44f5-bd3d-115790223af4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c4bf8041fbac675653bb620d3aca7b1abba21a0a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388051"
---
# <a name="create-package-configurations"></a>패키지 구성 만들기
  **패키지 구성 도우미** 대화 상자 및 패키지 구성 마법사를 사용하여 패키지 구성을 만들 수 있습니다. 이 도구에 액세스하려면 **의** SSIS **메뉴에서** 패키지 구성 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]을 클릭합니다.  
  
> [!NOTE]  
>  **구성**속성 옆에 있는 줄임표 단추를 클릭하여 **패키지 구성 도우미** 에 액세스할 수도 있습니다. 구성 속성은 패키지의 속성 창에 나타납니다.  
  
> [!NOTE]  
>  구성은 패키지 배포 모델에 사용할 수 있습니다. 매개 변수는 프로젝트 배포 모델에 대한 구성 대신 사용됩니다. 프로젝트 배포 모델을 사용하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하십시오.  
  
 **패키지 구성 도우미** 대화 상자에서는 구성을 사용하도록 패키지를 활성화하고 구성을 추가 및 삭제하며 구성이 로드되는 기본 순서를 설정할 수 있습니다.  
  
> [!NOTE]  
>  패키지 구성이 기본 순서로 로드되는 경우 **패키지 구성 도우미** 대화 상자에 표시된 목록의 맨 위에서 맨 아래까지의 구성이 로드됩니다. 그러나 런타임 시 패키지 구성이 기본 순서로 로드되지 않을 수 있습니다. 특히 부모 패키지 구성은 다른 유형의 구성보다 뒤에 로드됩니다.  
  
> [!NOTE]  
>  여러 구성이 동일한 개체 속성을 설정하는 경우 마지막으로 로드된 값이 런타임에 사용됩니다.  
  
 **패키지 구성 도우미** 대화 상자에서는 구성을 만드는 단계를 안내하는 패키지 구성 마법사를 실행할 수 있습니다. 패키지 구성 마법사를 실행하려면 **패키지 구성 도우미** 대화 상자에서 새 구성을 추가하거나 기존 구성을 편집합니다. 마법사 페이지에서 구성 유형을 선택하고 사용자가 구성에 직접 액세스할 것인지 또는 환경 변수를 사용할지 선택한 다음 구성에 저장할 속성을 선택하십시오.  
  
 다음 예에서는 패키지 구성 마법사의 마법사 완료 페이지에 표시되는 변수와 패키지의 대상 속성을 보여 줍니다.  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 이 예에서는 구성이 다음과 같은 속성을 업데이트합니다.  
  
-   사용자 정의 변수의 RaiseChangedEvent 속성, `TodaysDate`입니다.  
  
-   패키지의 MaximumErrorCount, LoggingMode 및 LocaleID 속성입니다.  
  
-   내 SQL 태스크 범위에 있는 사용자 정의 변수 `varTableName`의 Value 속성  
  
 "\Package"는 루트를 나타내며 구성에서 업데이트하는 속성에 대한 경로를 정의하는 개체를 구분하는 데 마침표(.)가 사용됩니다. 변수 및 속성의 이름은 대괄호로 묶여 있습니다. 구성에서는 패키지 이름과 상관없이 패키지라는 용어가 사용되지만 경로 내의 다른 모든 개체는 자체 사용자 정의 이름을 사용합니다.  
  
 마법사를 완료하면 **패키지 구성 도우미** 대화 상자의 구성 목록에 새 구성이 추가됩니다.  
  
> [!NOTE]  
>  패키지 구성 마법사의 마지막 페이지인 마법사 완료 페이지에는 구성의 대상 속성이 나열됩니다. **dtexec** 명령 프롬프트 유틸리티를 사용하여 패키지를 실행할 때 속성을 업데이트하려면 패키지 구성 마법사를 실행하여 속성 경로를 나타내는 문자열을 생성한 다음 복사하여 **dtexec**의 설정 옵션으로 사용할 수 있게 명령 프롬프트 창에 붙여넣습니다.  
  
 다음 표에서는 **패키지 구성 도우미** 대화 상자 구성 목록의 열에 대해 설명합니다.  
  
|Column|Description|  
|------------|-----------------|  
|**구성 이름**|구성의 이름입니다.|  
|**구성 유형**|구성의 유형입니다.|  
|**구성 문자열**|구성의 위치입니다. 위치는 경로, 환경 변수, 레지스트리 키, 부모 패키지 변수 이름 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 테이블일 수 있습니다.|  
|**대상 개체**|구성이 있는 속성을 가진 개체의 이름입니다. 구성이 XML 구성 파일이면 여러 개체를 업데이트할 수 있으므로 열이 비어 있습니다.|  
|**대상 속성**|속성의 이름입니다. 구성에서 XML 구성 파일 또는 SQL Server 테이블에 쓰면 여러 개체를 업데이트할 수 있으므로 열이 비어 있습니다.|  
  
### <a name="to-create-a-package-configuration"></a>패키지 구성을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **제어 흐름**, **데이터 흐름**, **이벤트 처리기**또는 **패키지 탐색기** 탭을 차례로 클릭합니다.  
  
4.  **SSIS** 메뉴에서 **패키지 구성**을 클릭합니다.  
  
5.  **패키지 구성 도우미** 대화 상자에서 **패키지 구성 설정**을 선택하고 **추가**를 클릭합니다.  
  
6.  패키지 구성 마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
7.  구성 유형 선택 페이지에서 구성 유형을 지정하고 구성 유형과 관련된 속성을 설정합니다. 자세한 내용은 [Package Configuration Wizard UI Reference](../../2014/integration-services/package-configuration-wizard-ui-reference.md)을 참조하세요.  
  
8.  내보낼 속성 선택 페이지에서 구성에 포함할 패키지 개체의 속성을 선택합니다. 구성 유형이 하나의 속성만 지원할 경우 이 마법사 페이지의 제목은 대상 속성 선택입니다. 자세한 내용은 [Package Configuration Wizard UI Reference](../../2014/integration-services/package-configuration-wizard-ui-reference.md)을 참조하세요.  
  
    > [!NOTE]  
    >  한 개의 구성에 여러 속성을 포함하는 기능은 **XML 구성 파일** 및 **SQL Server** 구성 유형만 지원합니다.  
  
9. 마법사 완료 페이지에 구성 이름을 입력하고 **마침**을 클릭합니다.  
  
10. **패키지 구성 도우미** 대화 상자에서 구성을 확인합니다.  
  
11. **닫기**를 클릭합니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
-   msdn.microsoft.com의 기술 문서 - [Integration Services 패키지 구성 이해](https://go.microsoft.com/fwlink/?LinkId=165643)   
  
-   블로그 항목 [패키지 구성을 코드에서 패키지를 만드는](https://go.microsoft.com/fwlink/?LinkId=217663), www.sqlis.com에 있습니다.  
  
-   블로그 항목 [API 샘플-패키지 구성 파일을 프로그래밍 방식으로 추가](https://go.microsoft.com/fwlink/?LinkId=217664)을 보려면 blogs.msdn.com에서.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 구성](../../2014/integration-services/package-configurations.md)   
 [배포 패키지 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [프로그래밍 방식으로 변수 작업](building-packages-programmatically/working-with-variables-programmatically.md)  
  
  
