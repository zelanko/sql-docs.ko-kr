---
title: 패키지 저장 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.savecopyas.f1
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ccfb64b68dcd1cf7069cc352eeeef034d5697428
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408585"
---
# <a name="save-packages"></a>패키지 저장
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 사용하여 만든 패키지를 파일 시스템에 XML 파일(.dtsx 파일)로 저장합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 msdb 데이터베이스나 패키지 저장소에 패키지 XML 파일의 복사본을 저장할 수도 있습니다. 패키지 저장소는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에서 관리하는 파일 시스템 위치에 있는 폴더를 나타냅니다.  
  
 패키지를 파일 시스템에 저장하면 나중에 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 또는 패키지 저장소로 가져올 수 있습니다. 자세한 내용은 [Integration Services 서비스&#40;SSIS 서비스&#41;](../integration-services/service/integration-services-service-ssis-service.md)를 참조하세요.  
  
 또한 **dtutil**명령 프롬프트 유틸리티를 사용하여 파일 시스템과 msdb 간에 패키지를 복사할 수 있습니다. 자세한 내용은 [dtutil Utility](../integration-services/dtutil-utility.md)를 참조하세요.  
## <a name="save-a-package-to-the-file-system"></a>파일 시스템에 패키지 저장  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 파일로 저장하려는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 저장할 패키지를 클릭합니다.  
  
3.  **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
    > [!NOTE]  
    >  속성 창에서 패키지가 저장된 경로와 파일 이름을 확인할 수 있습니다.  

## <a name="save-a-copy-of-a-package"></a>패키지의 복사본 저장
  이 섹션에서는 패키지 복사본을 파일 시스템, 패키지 저장소 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 **msdb** 데이터베이스에 저장하는 방법에 대해 설명합니다. 패키지 복사본의 저장 위치를 지정할 때 패키지 이름을 업데이트할 수도 있습니다.  
  
 패키지 저장소에는 **msdb** 데이터베이스와 파일 시스템의 폴더가 모두 포함될 수도 있고, **msdb**또는 파일 시스템의 폴더 중 하나만 포함될 수도 있습니다. **msdb**에서 패키지는 **sysssispackages** 테이블에 저장됩니다. 이 테이블에는 패키지가 속한 논리적 폴더를 식별하는 **folderid** 열이 있습니다. 논리적 폴더를 사용하면 파일 시스템의 폴더를 통해 파일 시스템에 저장된 패키지를 그룹화할 수 있는 것과 동일한 방식으로 **msdb** 에 저장된 패키지를 그룹화할 수 있습니다. **msdb** 의 **sysssispackagefolders** 테이블에 있는 행은 폴더를 정의합니다.  
  
 **msdb** 가 패키지 저장소의 일부로 정의되어 있지 않은 경우 **패키지 경로** 옵션에서 SQL Server를 선택할 때 패키지를 기존 논리적 폴더와 계속 연결할 수 있습니다.  
  
> [!NOTE]  
>  패키지 복사본을 저장하려면 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 패키지를 열어야 합니다.  
  
### <a name="to-save-a-copy-of-a-package"></a>패키지 복사본을 저장하려면  
  
1.  솔루션 탐색기에서 복사본을 저장하려는 패키지를 두 번 클릭합니다.  
  
2.  **파일** 메뉴에서 **다른 이름으로 \<패키지 파일>의 복사본 저장**을 클릭합니다.  
  
3.  **패키지 복사본 저장** 대화 상자의 **패키지 위치** 목록에서 패키지 위치를 선택합니다. 사용할 수 있는 옵션은 다음과 같습니다.  
    -   SQL Server
    -   파일 시스템 
    -   SSIS 패키지 저장소 
  
4.  위치가 **SQL Server** 또는 **SSIS 패키지 저장소**인 경우 서버 이름을 제공합니다.  
  
5.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 저장하는 경우에는 인증 유형을 지정하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우에는 사용자 이름과 암호를 제공합니다.  
  
6.  패키지 경로를 지정하려면 해당 경로를 직접 입력하거나, 찾아보기 단추 **(…)** 를 클릭하고 패키지 위치를 지정합니다. 패키지의 기본 이름은 Package입니다. 필요에 맞게 패키지 이름을 업데이트할 수도 있습니다.  
  
     **패키지 경로** 옵션으로 **SQL Server** 를 선택하면 패키지 경로는 **msdb** 의 논리적 폴더와 패키지 이름으로 구성됩니다. 예를 들어 DownloadMonthlyData 패키지가 MSDB 폴더( **msdb**에 있는 논리적 루트 폴더의 기본 이름) 내의 Finance 폴더와 연결되어 있으면 DownloadMonthlyData 패키지의 패키지 경로는 MSDB/Finance/DownloadMonthlyData가 됩니다.  
  
     **패키지 경로** 옵션으로 **SSIS 패키지 저장소** 를 선택하면 패키지 경로는 Integration Services 서비스에서 관리하는 폴더로 구성됩니다. 예를 들어 UpdateDeductions 패키지가 Integration Services 서비스에서 관리하는 파일 시스템 폴더 내의 HumanResources 폴더에 있으면 해당 패키지 경로는 /File System/HumanResources/UpdateDeductions가 됩니다. 마찬가지로 PostResumes 패키지가 MSDB 폴더 내의 HumanResources 폴더와 연결되어 있으면 해당 패키지 경로는 MSDB/HumanResources/PostResumes가 됩니다.  
  
     **패키지 경로** 옵션으로 **파일 시스템** 을 선택하면 패키지 경로는 파일 시스템에서의 위치와 파일 이름으로 구성됩니다. 예를 들어 패키지 이름이 UpdateDemographics이면 패키지 경로는 C:\HumanResources\Quarterly\UpdateDemographics.dtsx와 같이 됩니다.  
  
7.  패키지 보호 수준을 검토합니다.  
  
8.  선택적으로 **보호 수준** 상자 옆에 있는 찾아보기 단추 **(…)** 를 클릭하여 보호 수준을 바꿉니다.  
  
    -   **패키지 보호 수준** 대화 상자에서 다른 보호 수준을 선택합니다.  
  
    -   **확인**을 클릭합니다.  
  
9. **확인**을 클릭합니다.  

## <a name="save-a-package-as-a-package-template"></a>패키지 템플릿으로 패키지 저장
 이 섹션에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 새 Integration Services 패키지를 만들 때 사용자 지정 패키지를 템플릿으로 지정하고 사용하는 방법에 대해 설명합니다. 기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 새 패키지를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 추가할 때 빈 패키지를 만드는 패키지 템플릿을 사용합니다. 이러한 기본 템플릿은 바꿀 수 없지만 새 템플릿을 추가할 수는 있습니다.  
  
 여러 개의 패키지를 템플릿으로 지정하여 사용할 수 있습니다. 사용자 지정 패키지를 템플릿으로 구현하려면 먼저 패키지를 만들어야 합니다.  
  
 사용자 지정 패키지를 템플릿으로 사용하여 패키지를 만들면 새 패키지에 템플릿과 동일한 이름 및 GUID가 지정됩니다. 패키지를 구분하려면 **Name** 속성 값을 업데이트하고 **ID** 속성에 대한 새 GUID를 생성해야 합니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 만들기](../integration-services/create-packages-in-sql-server-data-tools.md) 및 [패키지 속성 설정](../integration-services/set-package-properties.md)을 참조하세요.  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>사용자 지정 패키지를 패키지 템플릿으로 지정하려면  
  
1.  파일 시스템에서 템플릿으로 사용할 패키지를 찾습니다.  
  
2.  해당 패키지를 DataTransformationItems 폴더로 복사합니다. 기본적으로 이 폴더는 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject에 있습니다.  
  
3.  템플릿으로 사용할 각 패키지에 대해 1단계와 2단계를 반복합니다.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>사용자 지정 패키지를 패키지 템플릿으로 사용하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 패키지를 만들려는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.  
  
3.  **새 항목 추가 -\<프로젝트 이름>** 대화 상자에서 템플릿으로 사용할 패키지를 클릭합니다.  
  
     템플릿 목록에 새 SSIS 패키지라는 기본 패키지 템플릿이 포함됩니다. 패키지 아이콘을 통해 패키지 템플릿으로 사용할 수 있는 템플릿을 식별할 수 있습니다.  
  
4.  **추가**를 클릭합니다.  
