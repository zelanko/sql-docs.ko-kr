---
title: 요소 (ClrAssemblyFile) (ASSL)를 입력 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (ClrAssemblyFile)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ab9e1e2c-ab06-4cd1-b007-16d738dc5604
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c253b2975c5e4f4cbf27c5b2d655a09617d644de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079126"
---
# <a name="type-element-clrassemblyfile-assl"></a>Type 요소(ClrAssemblyFile)(ASSL)
  에 속하는 파일 중 하나의 파일 유형을 지정는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 어셈블리입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ClrAssemblyFile>  
      ...  
      <Type>...</Type>  
   ...  
</ClrAssemblyFile>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*주*|지정된 파일이 어셈블리의 주 파일입니다.|  
|*종속*|지정된 파일이 어셈블리의 종속 파일입니다.|  
|*디버그*|지정된 파일에 디버깅 정보가 있습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Type`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ClrAssemblyFileType>입니다.  
  
 부모에 해당 하는 요소 `Type` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ClrAssemblyFile>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [파일 요소 &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [파일 요소 &#40;ASSL&#41;](../collections/files-element-assl.md)   
 [ClrAssembly 데이터 형식 &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Assembly 요소 &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Assemblies 요소 &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  