---
title: ComAssembly 데이터 형식 (ASSL) | Microsoft Docs
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
- ComAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ComAssembly
helpviewer_keywords:
- ComAssembly data type
ms.assetid: 23c0f4b3-b6ac-4ec8-9254-74d2f84f5244
caps.latest.revision: 49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 824fb508bb392f6ef84ede39645a5bac0da645e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171554"
---
# <a name="comassembly-data-type-assl"></a>ComAssembly 데이터 형식(ASSL)
  연결 된 COM 라이브러리를 나타내는 파생된 데이터 형식을 정의 [Server](../objects/server-element-assl.md) 하거나 [데이터베이스](../objects/database-element-assl.md) 요소입니다.  
  
> [!IMPORTANT]  
>  COM 어셈블리는 보안 위험을 내포할 수 있습니다. 이러한 위험 및 기타 고려 사항으로 인해 COM 어셈블리는 [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]에서 더 이상 사용되지 않습니다. COM 어셈블리는 후속 릴리스에서 지원되지 않을 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ComAssembly>  
      <!-- The following elements extend Assembly -->  
   <Source>...</Source>  
</ComAssembly>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[어셈블리](../objects/assembly-element-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[원본](../properties/source-element-comassembly-assl.md)|  
|파생 요소|참조 [어셈블리](../objects/assembly-element-assl.md) ([어셈블리](../collections/assemblies-element-assl.md) 모음인 [Database](../objects/database-element-assl.md) 또는 [Server](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 `ComAssembly` 요소는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssAS](../../../includes/ssas-md.md)] 인스턴스의 특정 데이터베이스와 연결된 COM 라이브러리에 대한 참조(정규화된 파일 이름 또는 프로그래밍 방식 식별자)를 포함합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ComAssembly>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ClrAssembly 데이터 형식 &#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
