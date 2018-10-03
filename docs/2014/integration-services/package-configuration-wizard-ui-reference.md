---
title: 패키지 구성 마법사 UI 참조 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.configwizard.selectobjects.f1
- sql12.dts.configwizard.selecconfigtype.f1
- sql12.dts.configwizard.finishdtsconfiguration.f1
- sql12.dts.configwizard.welcome.f1
ms.assetid: adca6938-6d5a-40ec-950e-dceb79d044fe
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f984034b21680842bdb4813f4f8d9489edb0913b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160383"
---
# <a name="package-configuration-wizard-ui-reference"></a>패키지 구성 마법사 UI 참조
  **패키지 구성 마법사** 를 사용하여 런타임에 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지 및 패키지 개체의 속성을 업데이트하는 구성을 만들 수 있습니다. 이 마법사는 **패키지 구성 도우미** 대화 상자에서 기존 구성을 수정하거나 새 구성을 추가하는 경우 실행됩니다. **패키지 구성 도우미** 대화 상자를 열려면 **의** SSIS **메뉴에서** 패키지 구성 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]을 선택합니다. 자세한 내용은 [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)를 참조하세요.  
  
> [!NOTE]  
>  구성은 패키지 배포 모델에 사용할 수 있습니다. 매개 변수는 프로젝트 배포 모델에 대한 구성 대신 사용됩니다. 프로젝트 배포 모델을 사용하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하십시오.  
  
 다음 섹션에서는 마법사의 페이지에 대해 설명합니다.  
  
## <a name="welcome-to-the-package-configuration-wizard-page"></a>패키지 구성 마법사 시작 페이지  
 **SSIS 구성 마법사** 를 사용하여 런타임에 패키지 및 패키지 개체의 속성을 업데이트하는 구성을 만들 수 있습니다.  
  
### <a name="options"></a>변수  
 **이 페이지를 다시 표시 안 함**  
 다음에 마법사를 열 때 시작 페이지를 표시하지 않습니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
## <a name="select-configuration-type-page"></a>구성 유형 선택 페이지  
 **구성 유형 선택** 페이지를 사용하여 만들 구성 유형을 지정할 수 있습니다.  
  
 사용할 구성 유형을 결정하는 데 추가 정보가 필요한 경우 [Package Configurations](../../2014/integration-services/package-configurations.md)을 참조하십시오.  
  
### <a name="static-options"></a>정적 옵션  
 **구성 유형**  
 다음 옵션을 사용하여 구성을 저장할 원본 유형을 선택합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**XML 구성 파일**|구성을 XML 파일로 저장합니다. 이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**환경 변수**|환경 변수 중 하나에 구성을 저장합니다. 이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**레지스트리 항목**|레지스트리에 구성을 저장합니다. 이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**부모 패키지 변수**|태스크를 포함하는 패키지의 변수로 구성을 저장합니다.  이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**SQL Server**|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 테이블에 구성을 저장합니다. 이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
  
 **다음**  
 마법사 시퀀스에서 다음 페이지를 표시합니다.  
  
### <a name="dynamic-options"></a>동적 옵션  
  
#### <a name="configuration-type-option--xml-configuration-file"></a>구성 유형 옵션 = XML 구성 파일  
 **구성 설정을 직접 지정**  
 설정을 직접 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**구성 파일 이름**|마법사에서 생성하는 구성 파일의 경로를 입력합니다.|  
|**찾아보기**|**구성 파일 위치 선택** 대화 상자를 사용하여 마법사에서 생성하는 구성 파일의 경로를 지정할 수 있습니다. 파일이 없으면 마법사에서 새 파일을 생성합니다.|  
  
 **구성 위치가 환경 변수에 저장됨**  
 구성이 저장되는 환경 변수를 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**환경 변수**|목록에서 환경 변수를 선택합니다.|  
  
#### <a name="configuration-type-option--environment-variable"></a>구성 유형 옵션 = 환경 변수  
 **환경 변수**  
 구성 정보를 포함하는 환경 변수를 선택합니다.  
  
#### <a name="configuration-type-option--registry-entry"></a>구성 유형 옵션 = 레지스트리 항목  
 **구성 설정을 직접 지정**  
 설정을 직접 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**레지스트리 항목**|구성 정보를 포함하는 레지스트리 키를 입력합니다. 형식은 \<레지스트리 키>입니다.<br /><br /> 레지스트리 키가 HKEY_CURRENT_USER에 이미 있어야 하고 Value라고 지정된 값을 가져야 합니다. 값은 DWORD 또는 문자열이 될 수 있습니다.<br /><br /> HKEY_CURRENT_USER의 루트에 없는 레지스트리 키를 사용하려면 \<레지스트리 키\레지스트리 키\\...> 형식을 사용하여 키를 식별합니다.|  
  
 **구성 위치가 환경 변수에 저장됨**  
 구성이 저장되는 환경 변수를 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**환경 변수**|목록에서 환경 변수를 선택합니다.|  
  
#### <a name="configuration-type-option--parent-package-variable"></a>구성 유형 옵션 = 부모 패키지 변수  
 **구성 설정을 직접 지정**  
 설정을 직접 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**부모 변수**|구성 정보를 포함하는 부모 패키지의 변수를 지정합니다.|  
  
 **구성 위치가 환경 변수에 저장됨**  
 구성이 저장되는 환경 변수를 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**환경 변수**|목록에서 환경 변수를 선택합니다.|  
  
#### <a name="configuration-type-options--sql-server"></a>구성 유형 옵션 = SQL Server  
 **구성 설정을 직접 지정**  
 설정을 직접 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**대량 삽입 태스크 편집기**|목록에서 연결을 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다.|  
|**구성 테이블**|기존 테이블을 선택하거나 **새로 만들기** 를 클릭하여 새 테이블을 만드는 SQL 문을 작성합니다.|  
|**구성 필터**|기존 구성 이름을 선택하거나 새 이름을 입력합니다.<br /><br /> 같은 테이블에 여러 SQL Server 구성을 저장할 수 있으며 각 구성은 여러 구성 항목을 포함할 수 있습니다.<br /><br /> 이 사용자 정의 값은 특정 구성에 속하는 구성 항목을 식별하기 위해 테이블에 저장됩니다.|  
  
 **구성 위치가 환경 변수에 저장됨**  
 구성이 저장되는 환경 변수를 지정하는 데 사용합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**환경 변수**|목록에서 환경 변수를 선택합니다.|  
  
## <a name="select-objects-to-export-page"></a>내보낼 개체 선택 페이지  
 **대상 속성 선택 또는 내보낼 속성 선택** 페이지를 사용하여 구성에 포함할 개체 속성을 지정할 수 있습니다. 여러 속성을 선택하는 기능은 XML 구성 유형을 선택하는 경우에만 사용할 수 있습니다.  
  
### <a name="options"></a>변수  
 **개체**  
 패키지 계층을 확장하고 내보낼 속성을 선택합니다.  
  
 **속성 특성**  
 속성의 특성을 봅니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
## <a name="completing-the-wizard-page"></a>마법사 완료 페이지  
 **마법사 완료** 페이지를 사용하여 구성의 이름을 지정하고 마법사에서 구성을 만드는 데 사용하는 설정을 볼 수 있습니다. 마법사를 완료하면 패키지의 모든 구성을 나열하는 **패키지 구성 도우미** 가 표시됩니다.  
  
### <a name="options"></a>변수  
 **구성 이름**  
 구성의 이름을 입력합니다.  
  
 **미리 보기**  
 마법사에서 구성을 만드는 데 사용하는 설정을 봅니다.  
  
 **마침**  
 구성을 만든 다음 **패키지 구성 마법사**를 종료합니다.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)  
  
  
