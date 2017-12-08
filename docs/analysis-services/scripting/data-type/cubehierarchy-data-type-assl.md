---
title: "CubeHierarchy 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CubeHierarchy Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubeHierarchy
helpviewer_keywords: CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7b69a18093cd54d21e2cb0e6ad557ff89f28cf35
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="cubehierarchy-data-type-assl"></a>CubeHierarchy 데이터 형식(ASSL)
  에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [계층](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) 요소에는 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [활성화](../../../analysis-services/scripting/properties/enabled-element-assl.md), [HierarchyID](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [OptimizedState](../../../analysis-services/scripting/properties/optimizedstate-element-assl.md), [표시](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
|파생 요소|[계층 구조](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) ([계층](../../../analysis-services/scripting/collections/hierarchies-element-assl.md) 컬렉션 [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>주의  
 이 데이터 형식에는 제한이 없으므로 다음과 같은 모든 배포 모드에서 사용할 수 있습니다. 0-다차원 및 데이터 마이닝, 1-SharePoint 및 2-테이블 형식.  
  
 이상 버전에서 SQL Server 2016 Analysis Services는 *Enabled* 속성 설정할 수 없습니다 **False** 에 대 한 *CubeHierarchy*합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CubeHierarchy>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [방법 &#40; 검색 XMLA &#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
