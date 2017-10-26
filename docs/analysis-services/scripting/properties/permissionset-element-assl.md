---
title: "PermissionSet 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- PermissionSet Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PermissionSet
helpviewer_keywords:
- PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1448c3db59f149697fa429e6d122d9d20fd403f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="permissionset-element-assl"></a>PermissionSet 요소(ASSL)
  와 연결 된 권한 집합을 식별 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 어셈블리입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ClrAssembly>  
   ...  
   <PermissionSet>...</PermissionSet>  
  
</ClrAssembly>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*안전*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*안전*|내부 계산 및 로컬 데이터 액세스만 허용됩니다. *안전* 는 가장 제한적인 권한 집합입니다. 코드를 실행 하 여 어셈블리에서 *안전* 권한을 파일, 네트워크, 환경 변수 또는 레지스트리 같은 외부 시스템 리소스에 액세스할 수 없습니다.|  
|*ExternalAccess*|*안전*, 파일, 네트워크, 환경 변수를 레지스트리 같은 외부 시스템 리소스에 액세스 하는 추가 기능입니다.|  
|*제한 없음*|무제한 어셈블리 내부 및 외부 리소스에 무제한 액세스를 허용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 내에서 실행 되는 코드는 *Unrestricted* 어셈블리 비관리 코드를 호출할 수 있습니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **PermissionSet** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.PermissionSet>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ComAssembly 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Assemblies 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Database 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Server 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

