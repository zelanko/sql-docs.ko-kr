---
title: PermissionSet 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- PermissionSet Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PermissionSet
helpviewer_keywords:
- PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 471ef43aea9fadcca7ab8a4a36870a3bdddee22f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263469"
---
# <a name="permissionset-element-assl"></a>PermissionSet 요소(ASSL)
  연결 된 권한 집합을 식별 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 어셈블리입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ClrAssembly>  
   ...  
   <PermissionSet>...</PermissionSet>  
  
</ClrAssembly>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*안전 하 게 보호*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*안전 하 게 보호*|내부 계산 및 로컬 데이터 액세스만 허용됩니다. *안전한* 는 가장 제한적인 권한 집합입니다. 코드를 사용 하 여 어셈블리에서 실행 *안전한* 권한을 파일, 네트워크, 환경 변수 또는 레지스트리 같은 외부 시스템 리소스에 액세스할 수 없습니다.|  
|*ExternalAccess*|*안전한*, 파일, 네트워크, 환경 변수 및 레지스트리와 같은 외부 시스템 리소스를 액세스 하는 추가 기능을 사용 하 여 합니다.|  
|*무제한*|무제한 어셈블리 내부 및 외부 리소스에 무제한 액세스를 허용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 내에서 실행 되는 코드를 *Unrestricted* 어셈블리는 비관리 코드를 호출할 수 있습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `PermissionSet`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.PermissionSet>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ComAssembly 데이터 형식 &#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [Assemblies 요소 &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Database 요소 &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Server 요소 &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
