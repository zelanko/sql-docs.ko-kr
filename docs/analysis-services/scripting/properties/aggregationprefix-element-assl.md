---
title: "AggregationPrefix 요소 (ASSL) | Microsoft Docs"
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
- AggregationPrefix Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationPrefix
helpviewer_keywords:
- AggregationPrefix element
ms.assetid: 1581e0df-ae8e-41ce-9c92-f0f7cac487f2
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ef1688e23bddf1136775474c93ae62a05bb97ab
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationprefix-element-assl"></a>AggregationPrefix 요소(ASSL)
  관련 부모 요소 전체에서 집계 이름에 사용할 공통 접두사를 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Database, MeasureGroup, Partition -->  
   ...  
   <AggregationPrefix>...</AggregationPrefix>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 집계 접두사에서 집계 이름을 생성 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 및 관계형 ROLAP (OLAP) 파티션에 저장 된 집계에 대 한 관계형 데이터베이스의 테이블 이름도 생성 합니다.  
  
 완전히 확장된 집계 이름은 다음 부분으로 구성됩니다.  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 집계 이름의 처음 네 부분은 집계 접두사를 구성합니다. 사용자가 다음과 같이 처음 네 부분을 제공합니다.  
  
-   *DatabasePrefix* 는 **AggregationPrefix** 요소와 연관된 **Database** 요소의 값을 나타냅니다.  
  
-   *CubePrefix* 는 **AggregationPrefix** 요소와 연관된 **Cube** 요소의 값을 나타냅니다.  
  
-   *MeasureGroupPrefix* 는 **AggregationPrefix** 요소와 연관된 **MeasureGroup** 요소의 값을 나타냅니다.  
  
-   *PartitionPrefix* 는 **AggregationPrefix** 요소와 연관된 **Partition** 요소의 값을 나타냅니다.  
  
 이름의 다섯 번째 부분인 *AggregationID*는 시스템 정의 ID로, 사용자는 이름의 이 부분을 제어할 수 없습니다.  
  
 부모에 해당 하는 요소 **AggregationPrefix** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.MeasureGroup>, 및 <xref:Microsoft.AnalysisServices.Partition>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

