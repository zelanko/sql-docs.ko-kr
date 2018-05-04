---
title: CreatedTimestamp 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- CreatedTimestamp Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CreatedTimestamp
helpviewer_keywords:
- CreatedTimestamp element
ms.assetid: 35f5dd33-ea82-4be3-a117-69136aa9d1a4
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 047acd47a712c0daf3be74989922d4533a4bd9a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="createdtimestamp-element-assl"></a>CreatedTimestamp 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|과 같이 지원되는|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[어셈블리](../../../analysis-services/scripting/objects/assembly-element-assl.md), [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md), [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md), [권한](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **CreatedTimestamp** 읽기 전용 요소는 포함 **DateTime** 개체의 지정 된 인스턴스에 생성 된 시간과 날짜를 나타내는 값 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. 이 요소의 값은 비워둘 수 없습니다.  
  
 부모에 해당 하는 요소 **CreatedTimestamp** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Assembly>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.DataSourceView>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MdxScript>, <xref:Microsoft.AnalysisServices.MeasureGroup>, <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningStructure>, <xref:Microsoft.AnalysisServices.Partition>, <xref:Microsoft.AnalysisServices.Permission>, 및 <xref:Microsoft.AnalysisServices.Perspective>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
