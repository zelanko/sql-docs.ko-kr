---
title: Assembly 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Assembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Assembly data type
ms.assetid: 0a381322-9509-4579-a754-c6cdd0a70cc9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb02963baa8a7fca296abe89801d89c1f7ea19fa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209650"
---
# <a name="assembly-data-type-assl"></a>Assembly 데이터 형식(ASSL)
  나타내는 추상 기본 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리나와 연결 된 COM 동적 연결 라이브러리 (DLL)는 [Server](../objects/server-element-assl.md) 또는 [데이터베이스](../objects/database-element-assl.md) 요소입니다.  
  
> [!IMPORTANT]  
>  COM 어셈블리는 보안 위험을 내포할 수 있습니다. 이러한 위험 및 기타 고려 사항으로 인해 COM 어셈블리는 [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]에서 더 이상 사용되지 않습니다. COM 어셈블리는 후속 릴리스에서 지원되지 않을 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Assembly>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Annotations>...</Annotations>  
</Assembly>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|[ClrAssembly](assembly-data-type-assl.md), [ComAssembly](comassembly-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)를 [설명](../properties/description-element-assl.md)를 [ID](../properties/id-element-assl.md)를 [ImpersonationInfo](../properties/impersonationinfo-element-assl.md), [ LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [이름](../properties/name-element-assl.md)|  
|파생 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Assembly` 데이터 형식은 인스턴스 또는 데이터베이스와 연결된 COM 라이브러리를 나타내는 `ComAssembly` 요소와 인스턴스 또는 데이터베이스와 연결된 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리를 나타내는 `ClrAssembly` 요소에 대한 기본 데이터 형식으로 사용됩니다. 어셈블리에 대 한 자세한 내용은 참조 하세요. [다차원 모델 어셈블리 관리](../../multidimensional-models/multidimensional-model-assemblies-management.md)합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Assembly>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Server 요소 &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Database 요소 &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
