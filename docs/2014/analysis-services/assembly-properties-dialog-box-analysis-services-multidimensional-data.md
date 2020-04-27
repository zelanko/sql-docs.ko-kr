---
title: 어셈블리 속성 대화 상자 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.assemblyproperties.f1
ms.assetid: da1174d6-d82b-4337-ac19-7368dbd95a84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b21230ddff5a3db043b533a4f921a30b02da739b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062303"
---
# <a name="assembly-properties-dialog-box-analysis-services---multidimensional-data"></a>어셈블리 속성 대화 상자(Analysis Services - 다차원 데이터)
  **의** 어셈블리 속성 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 어셈블리 참조 속성을 설정할 수 있습니다. **개체 탐색기** 에서 어셈블리를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택하여 **어셈블리 속성**대화 상자를 표시할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
|용어|정의|  
|----------|----------------|  
|**이름**|어셈블리 참조의 이름을 변경하려면 입력합니다.<br /><br /> 참고: 이 값을 변경하면 어셈블리 참조에서 참조하는 어셈블리 이름은 변경되지 않지만 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 또는 데이터베이스에서 해당 어셈블리 참조를 참조할 때 사용하는 이름이 변경됩니다.|  
|**ID**|어셈블리 참조에서 참조하는 어셈블리의 식별자를 표시합니다.|  
|**설명**|어셈블리 참조에 대한 설명을 변경하려면 입력합니다.|  
|**생성된 타임스탬프**|어셈블리 참조가 생성된 날짜와 시간을 표시합니다.|  
|**최종 스키마 업데이트**|어셈블리 참조의 메타데이터가 마지막으로 업데이트된 날짜와 시간을 표시합니다.|  
|**Type**|어셈블리 참조의 유형을 표시합니다. 다음과 같은 값이 표시됩니다.<br /><br /> **.Net 어셈블리**: 어셈블리 참조는 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 어셈블리를 참조 합니다.<br /><br /> **COM DLL**: 어셈블리 참조는 com 라이브러리를 참조 합니다.|  
|**원본**|어셈블리 참조의 원본을 표시합니다. 이 속성에는 일반적으로 어셈블리 참조에서 참조하는 어셈블리의 전체 경로와 파일 이름이 포함되어 있습니다.|  
|**권한 집합**|어셈블리 참조에 대한 액세스 권한을 결정하는 데 사용되는 권한 집합을 선택합니다. 이 속성에 사용할 수 있는 값에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.ClrAssembly.PermissionSet%2A>을 참조하십시오.|  
|**가장 정보**|어셈블리 참조에 액세스할 때 사용할 가장 정보를 선택합니다. 이 속성에 사용할 수 있는 값에 대한 자세한 내용은 [ImpersonationInfo 요소&#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)를 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [다차원 모델 어셈블리 관리](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
