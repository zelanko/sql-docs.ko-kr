---
title: CreatedTimestamp 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CreatedTimestamp Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CreatedTimestamp
helpviewer_keywords:
- CreatedTimestamp element
ms.assetid: 35f5dd33-ea82-4be3-a117-69136aa9d1a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e13b032b34ee63a7c7a939d7ad17b8ceb1786739
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191023"
---
# <a name="createdtimestamp-element-assl"></a>CreatedTimestamp 요소(ASSL)
  부모 요소의 읽기 전용 생성 타임스탬프를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Assembly> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CreatedTimestamp>...</CreatedTimestamp>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|DateTime|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[어셈블리](../objects/assembly-element-assl.md), [큐브](../objects/cube-element-assl.md)를 [데이터베이스](../objects/database-element-assl.md)를 [DataSource](../objects/datasource-element-assl.md)를 [DataSourceView](../objects/datasourceview-element-assl.md), [차원](../objects/dimension-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md)를 [MeasureGroup](../objects/group-element-assl.md)를 [MiningModel](../objects/miningmodel-element-assl.md)를 [MiningStructure](../objects/miningstructure-element-assl.md), [파티션](../objects/partition-element-assl.md)하십시오 [권한을](../data-type/permission-data-type-assl.md), [관점](../objects/perspective-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `CreatedTimestamp` 요소는 지정된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서 개체가 만들어진 날짜와 시간을 나타내는 읽기 전용 `DateTime` 값을 포함합니다. 이 요소의 값은 비워둘 수 없습니다.  
  
 부모에 해당 하는 요소 `CreatedTimestamp` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.Assembly>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>를 <xref:Microsoft.AnalysisServices.DataSource>를 <xref:Microsoft.AnalysisServices.DataSourceView>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MdxScript>, <xref:Microsoft.AnalysisServices.MeasureGroup>, <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningStructure>, <xref:Microsoft.AnalysisServices.Partition>합니다 <xref:Microsoft.AnalysisServices.Permission>, 및 <xref:Microsoft.AnalysisServices.Perspective>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
