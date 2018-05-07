---
title: ComAssembly 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 409eb7fd0dd093e7bd44a642868c8dd87d25f04e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="comassembly-data-type-assl"></a>ComAssembly 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [Server](../../../analysis-services/scripting/objects/server-element-assl.md) 또는 [Database](../../../analysis-services/scripting/objects/database-element-assl.md) 요소와 연결된 COM 라이브러리를 나타내는 파생 데이터 형식을 정의합니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[어셈블리](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[원본](../../../analysis-services/scripting/properties/source-element-comassembly-assl.md)|  
|파생 요소|[Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) ([Database](../../../analysis-services/scripting/collections/assemblies-element-assl.md) 또는 [Server](../../../analysis-services/scripting/objects/database-element-assl.md) 의 [Assemblies](../../../analysis-services/scripting/objects/server-element-assl.md)컬렉션) 참조|  
  
## <a name="remarks"></a>주의  
 **ComAssembly** 의 인스턴스와 연결 된 COM 라이브러리를 참조 (정규화 된 파일 이름 또는 프로그래밍 방식 식별자)를 포함 하는 요소 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 또는 특정 인스턴스에서 데이터베이스 [!INCLUDE[ssAS](../../../includes/ssas-md.md)]합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ComAssembly>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ClrAssembly 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
