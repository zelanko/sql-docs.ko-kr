---
title: '4단계: 패키지 구성 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: e04a5321-63d5-4ec5-85b9-cb4eaf6c87f6
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3ccfede2f138e5635c01cd9bc22143a0b77cb118
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-4---adding-package-configurations"></a>1-4단원 - 패키지 구성 추가
이 태스크에서는 각 패키지에 구성을 추가합니다. 구성은 런타임 시 패키지 속성 및 패키지 개체의 값을 업데이트합니다.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 다양한 구성 유형이 제공됩니다. 구성을 환경 변수, 레지스트리 항목, 사용자 정의 변수, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블 및 XML 파일에 저장할 수 있습니다. 보다 나은 유연성을 위해 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 간접 구성 사용을 지원합니다. 이는 실제 값을 지정하는 구성의 위치는 환경 변수를 사용하여 지정한다는 것을 의미합니다. Deployment Tutorial 프로젝트의 패키지는 XML 구성 파일과 간접 구성의 조합을 사용합니다. XML 구성 파일은 여러 속성에 대한 구성을 포함할 수 있으며 가능한 경우 여러 패키지에서 참조할 수 있습니다. 이 자습서에서는 각 패키지에 대한 별개의 구성 파일을 사용합니다.  
  
구성 파일은 연결 문자열과 같은 중요한 정보를 포함하는 경우가 많습니다. 따라서 ACL(액세스 제어 목록)을 사용하여 파일을 저장하는 위치나 폴더에 대한 액세스를 제한하고 패키지 실행이 허용되는 사용자나 계정에만 액세스를 제공해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
이전 태스크에서 Deployment Tutorial 프로젝트에 추가했던 패키지(DataTransfer 및 LoadXMLData)는 구성을 구현해야 대상 서버에 배포된 후 성공적으로 실행됩니다. 구성을 구현하려면 XML 구성 파일에 대한 간접 구성을 만든 다음 XML 구성 파일을 만듭니다.  
  
구성 파일인 DataTransferConfig.dtsConfig 및 LoadXMLData.dtsConfig를 만듭니다. 이러한 파일은 패키지에 사용되는 데이터 및 로그 파일의 위치를 지정하는 패키지의 속성을 업데이트하는 이름-값 쌍을 포함합니다. 나중에 배포 프로세스의 한 단계에서 구성 파일의 값을 업데이트하여 대상 컴퓨터에 있는 파일의 새 위치를 반영합니다.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 DataTransferConfig.dtsConfig 및 LoadXMLData.dtsConfig가 DataTransfer 및 LoadXMLData 패키지의 종속 파일임을 인식하고 구성 파일을 자동으로 포함합니다.  
  
### <a name="to-create-indirect-configuration-for-the-datatransfer-package"></a>DataTransfer 패키지에 대한 간접 구성을 만들려면  
  
1.  솔루션 탐색기에서 DataTransfer.dtsx를 두 번 클릭합니다.  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 제어 흐름 디자인 화면의 배경을 아무 곳이나 클릭합니다.  
  
3.  **SSIS** 메뉴에서 **패키지 구성**을 클릭합니다.  
  
4.  **패키지 구성 도우미**대화 상자에서 아직 선택하지 않은 경우 **패키지 구성 설정** 을 선택하고 **추가**를 클릭합니다.  
  
5.  패키지 구성 마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
6.  구성 유형 선택 페이지의 **구성 유형** 목록에서 **XML 구성 파일** 을 선택하고 **구성 위치가 환경 변수에 저장됨** 옵션을 선택한 다음 **DataTransfer** 를 입력하거나 목록에서 **DataTransfer** 환경 변수를 선택합니다.  
  
    > [!NOTE]  
    > 이 환경 변수를 목록에서 사용할 수 있게 하려면 변수를 추가한 후에 컴퓨터를 다시 시작해야 할 수도 있습니다. 컴퓨터를 다시 시작하지 않으려면 환경 변수의 이름을 입력합니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  마법사 완료 페이지에서 **구성 이름** 상자에 **DataTransfer EV Configuration** 을 입력하고 **미리 보기** 창에서 구성 내용을 검토한 다음 **마침**을 클릭합니다.  
  
9. **패키지 구성 도우미**대화 상자를 닫습니다.  
  
### <a name="to-create-the-xml-configuration-for-the-datatransfer-package"></a>DataTransfer 패키지에 대한 XML 구성을 만들려면  
  
1.  솔루션 탐색기에서 DataTransfer.dtsx를 두 번 클릭합니다.  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 제어 흐름 디자인 화면의 배경을 아무 곳이나 클릭합니다.  
  
3.  **SSIS** 메뉴에서 **패키지 구성**을 클릭합니다.  
  
4.  패키지 구성 도우미 대화 상자에서 **패키지 구성 설정** 확인란을 선택하고 **추가**를 클릭합니다.  
  
5.  패키지 구성 마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
6.  구성 유형 선택 페이지의 **구성 유형** 목록에서 **XML 구성 파일** 을 선택한 다음 **찾아보기**를 클릭합니다.  
  
7.  **구성 파일 위치 선택** 대화 상자에서 C:\DeploymentTutorial로 이동한 다음 **파일 이름** 상자에 **DataTransferConfig** 를 입력하고 **저장**을 클릭합니다.  
  
8.  구성 유형 선택 페이지에서 **다음**을 클릭합니다.  
  
9. 내보낼 속성 선택 페이지에서 DataTransfer, 연결 관리자, Deployment Tutorial Log 및 Properties를 확장한 다음 **연결 문자열** 확인란을 선택합니다.  
  
10. 연결 관리자 내에서 NewCustomers를 확장한 다음 **연결 문자열** 확인란을 선택합니다.  
  
11. **다음**을 클릭합니다.  
  
12. 마법사 완료 페이지에서 **구성 이름** 상자에 **DataTransfer Configuration** 을 입력하고 구성 내용을 검토한 다음 **마침**을 클릭합니다.  
  
13. **패키지 구성 도우미** 대화 상자에서 DataTransfer EV Configuration이 먼저 나열된 다음 DataTransfer Configuration이 나열되는지 확인하고 **닫기**를 클릭합니다.  
  
### <a name="to-create-indirect-configuration-for-the-loadxmldata-package"></a>LoadXMLData 패키지에 대한 간접 구성을 만들려면  
  
1.  솔루션 탐색기에서 LoadXMLData.dtsx를 두 번 클릭합니다.  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 제어 흐름 디자인 화면의 배경을 아무 곳이나 클릭합니다.  
  
3.  **SSIS** 메뉴에서 **패키지 구성**을 클릭합니다.  
  
4.  **패키지 구성 도우미**대화 상자에서 **추가**를 클릭합니다.  
  
5.  패키지 구성 마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
6.  구성 유형 선택 페이지의 **구성 유형** 목록에서 **XML 구성 파일** 을 선택하고 **구성 위치가 환경 변수에 저장됨** 옵션을 선택한 다음 **LoadXMLData** 를 입력하거나 목록에서 **LoadXMLData** 환경 변수를 선택합니다.  
  
    > [!NOTE]  
    > 이 환경 변수를 목록에서 사용할 수 있게 하려면 변수를 추가한 후에 컴퓨터를 다시 시작해야 할 수도 있습니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  마법사 완료 페이지에서 **구성 이름** 상자에 **LoadXMLData EV Configuration** 을 입력하고 구성 내용을 검토한 다음 **마침**을 클릭합니다.  
  
### <a name="to-create-the-xml-configuration-for-the-loadxmldata-package"></a>LoadXMLData 패키지에 대한 XML 구성을 만들려면  
  
1.  솔루션 탐색기에서 LoadXMLData.dtsx를 두 번 클릭합니다.  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 제어 흐름 디자인 화면의 배경을 아무 곳이나 클릭합니다.  
  
3.  **SSIS** 메뉴에서 **패키지 구성**을 클릭합니다.  
  
4.  패키지 구성 도우미 대화 상자에서 **패키지 구성 설정** 확인란을 선택하고 **추가**를 클릭합니다.  
  
5.  패키지 구성 마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
6.  구성 유형 선택 페이지의 **구성 유형** 목록에서 **XML 구성 파일** 을 선택한 다음 **찾아보기**를 클릭합니다.  
  
7.  **구성 파일 위치 선택** 대화 상자에서 C:\DeploymentTutorial로 이동한 다음 **파일 이름** 상자에 **LoadXMLDataConfig** 를 입력하고 **저장**을 클릭합니다.  
  
8.  구성 유형 선택 페이지에서 **다음**을 클릭합니다.  
  
9. 내보낼 속성 선택 페이지에서 LoadXMLData, 실행 파일, Load XML Data 및 Properties를 확장한 다음 **[XMLSource].[XMLData]** 및 **[XMLSource].[XMLSchemaDefinition]** 확인란을 선택합니다.  
  
10. **다음**을 클릭합니다.  
  
11. 마법사 완료 페이지에서 **구성 이름** 상자에 **LoadXMLData Configuration** 을 입력하고 구성 내용을 검토한 다음 **마침**을 클릭합니다.  
  
12. **패키지 구성 도우미** 대화 상자에서 LoadXMLData EV Configuration이 먼저 나열된 다음 LoadXMLData Configuration이 나열되는지 확인하고 **닫기**를 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[5단계: 업데이트된 패키지 테스트](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="see-also"></a>참고 항목  
[패키지 구성](../integration-services/packages/package-configurations.md)  
[패키지 구성 만들기](../integration-services/packages/create-package-configurations.md)  
[패키지에서 사용되는 파일 액세스](../integration-services/security/security-overview-integration-services.md#files)  
