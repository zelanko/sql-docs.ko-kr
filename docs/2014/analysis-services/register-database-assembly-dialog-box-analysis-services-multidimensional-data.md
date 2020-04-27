---
title: 데이터베이스 어셈블리 등록 대화 상자 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidevstudio.assembly.registerassembly.f1
ms.assetid: 0c07cc87-fc94-456f-b878-7b23e39772b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06647219ca5768495620bb1db60cf34910844f25
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070467"
---
# <a name="register-database-assembly-dialog-box-analysis-services---multidimensional-data"></a>데이터베이스 어셈블리 등록 대화 상자(Analysis Services - 다차원 데이터)
  **의** 서버 어셈블리 등록 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 어셈블리 참조 속성을 설정할 수 있습니다. **개체 탐색기** 에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 또는 데이터베이스의 어셈블리 폴더를 마우스 오른쪽 단추로 클릭하고 **새 어셈블리** 를 선택하면 **서버 어셈블리 등록**대화 상자를 표시할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
|용어|정의|  
|----------|----------------|  
|**Type**|어셈블리 참조 유형을 선택합니다. 사용할 수 있는 값은 다음과 같습니다.<br /><br /> **.Net 어셈블리**: <br />                      어셈블리 참조는 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 어셈블리를 참조합니다.<br /><br /> **COM DLL**: <br />                      어셈블리 참조는 COM 라이브러리를 참조합니다.<br /><br /> <br /><br /> ** \* \* 보안 \* 정보** COM 어셈블리는 보안 위험을 초래할 수 있습니다. 이러한 위험 및 기타 고려 사항으로 인해 COM 어셈블리는 [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)]에서 더 이상 사용되지 않습니다. COM 어셈블리는 후속 릴리스에서 지원되지 않을 수 있습니다.|  
|**파일 이름**|.NET 어셈블리 또는 COM 라이브러리의 전체 경로와 파일 이름을 입력합니다.|  
|**...**|**열기** 대화 상자를 표시하고 .NET 어셈블리 또는 COM 라이브러리의 전체 경로와 파일 이름을 선택하려면 클릭합니다.|  
|**어셈블리 이름**|어셈블리 참조 이름을 입력하여 설정합니다.<br /><br /> 참고: 이 값을 변경하면 어셈블리 참조에서 참조하는 어셈블리 이름은 변경되지 않지만 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 또는 데이터베이스에서 해당 어셈블리 참조를 참조할 때 사용하는 이름이 변경됩니다.|  
|**디버그 정보 포함**|.NET 어셈블리 또는 COM 라이브러리의 디버그 정보를 포함하려면 이 옵션을 선택합니다(있는 경우).|  
|**생성된 타임스탬프**|어셈블리 참조가 생성된 날짜와 시간을 표시합니다.|  
|**최종 스키마 업데이트**|어셈블리 참조의 메타데이터가 마지막으로 업데이트된 날짜와 시간을 표시합니다.|  
|**원본**|어셈블리 참조의 원본을 표시합니다. 이 속성에는 일반적으로 어셈블리 참조에서 참조하는 어셈블리의 전체 경로와 파일 이름이 포함되어 있습니다.|  
|**안전**|어셈블리 참조에 이 권한 집합을 사용하려면 이 옵션을 선택합니다. 이 옵션을 선택하면 어셈블리에 내부 계산과 로컬 데이터 액세스만 허용됩니다. 이 옵션을 사용하여 어셈블리에서 실행한 코드는 파일, 네트워크, 환경 변수 또는 레지스트리와 같은 외부 시스템 리소스에 액세스할 수 없습니다.<br /><br /> ** \* \* 보안 \* 정보** 이 옵션은 외부 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 리소스에 액세스 하지 않고 계산 및 데이터 관리 작업을 수행 하는 어셈블리에 대해 권장 되는 권한 설정입니다. 이 옵션은 가장 제한적인 권한 집합을 나타냅니다.|  
|**외부 액세스**|어셈블리 참조에 이 권한 집합을 사용하려면 이 옵션을 선택합니다. 이 옵션을 선택하면 어셈블리에 내부 계산과 로컬 데이터 액세스만 허용됩니다. 이 권한 집합을 사용하여 어셈블리에서 실행한 코드는 파일, 네트워크, 환경 변수 및 레지스트리와 같은 외부 시스템 리소스에 액세스할 수 있습니다.<br /><br /> ** \* \* 보안 \* 정보** 외부 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]리소스에 액세스 하는 어셈블리에는이 옵션을 사용 하는 것이 좋습니다. 이 옵션을 사용한 어셈블리는 기본적으로 서비스 계정의 보안 자격 증명을 사용하여 실행됩니다. 이 어셈블리 내의 코드는 호출자의 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 인증 보안 컨텍스트를 명시적으로 가장할 수 있습니다. 기본값이 서비스 계정으로 실행되는 것이기 때문에 서비스 계정으로 실행하도록 신뢰할 수 있는 역할에만 이 옵션을 사용한 어셈블리 실행 권한을 부여해야 합니다. 이 옵션은 **안전**보다 덜 제한적이고 **제한 없음**보다는 더 제한적인 권한 집합을 나타냅니다.|  
|**무제한**|어셈블리 참조에 이 권한 집합을 사용하려면 이 옵션을 선택합니다. 이 옵션을 선택하면 어셈블리에서 제한 없이 내부 및 외부 리소스에 액세스할 수 있습니다. 이 옵션을 사용한 어셈블리 내에서 실행되는 코드는 비관리 코드를 호출할 수 있습니다.<br /><br /> ** \* \* 보안 \* 정보** 어셈블리에 제한 없는 액세스가 필요한 경우가 아니면이 옵션을 사용 하지 않는 것이 좋습니다. 보안 측면에서 이 옵션은 **외부 액세스**와 같습니다. 그러나 **외부 액세스** 옵션을 사용한 어셈블리는 이 옵션을 사용한 어셈블리에 포함되지 않는 다양한 안정성 및 견고성 보호 기능을 제공합니다. 이 옵션을 지정하면 어셈블리의 코드가 프로세스 공간에 대해 잘못된 작업을 수행할 수 있으므로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 견고성과 확장성이 저하될 수 있습니다. 이 옵션은 가장 덜 제한적인 권한 집합을 나타내며 주의해서 사용해야 합니다.|  
|**특정 사용자 이름 및 암호 사용**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체가 지정된 사용자 계정의 보안 자격 증명을 사용하려면 이 옵션을 선택합니다.|  
|**사용자 이름**|선택한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에서 사용할 사용자 계정의 도메인과 이름을 입력합니다. 사용자 계정의 도메인과 이름은 다음 형식을 사용합니다.<br /><br /> 도메인 이름>* \<* **\\** 사용자 계정 이름>* \<*<br /><br /> 참고: 이 옵션은 **특정 사용자 이름 및 암호 사용** 을 선택한 경우에만 사용할 수 있습니다.|  
|**암호**|선택한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에서 사용할 사용자 계정의 도메인과 이름을 입력합니다.|  
|**서비스 계정 사용**|개체를 관리하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서비스와 연결된 보안 자격 증명을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에 사용하려면 이 옵션을 선택합니다.|  
|**현재 사용자의 자격 증명 사용**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에서 현재 사용자의 보안 자격 증명을 사용하려면 이 옵션을 선택합니다.|  
|**기본**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 기본 사용자 계정을 사용하려면 이 옵션을 선택합니다. 이 옵션을 선택하는 것은 **현재 사용자의 자격 증명 사용** 옵션을 선택하는 것과 같습니다.|  
|**설명**|어셈블리 참조 설명을 입력하여 설정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [다차원 모델 어셈블리 관리](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
