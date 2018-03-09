---
title: "큐브 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Cube Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Cube
helpviewer_keywords: Cube element
ms.assetid: 2d801066-6cca-4a99-bbd8-56a38d762108
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7e045552036a2c477ee4792d4f8e23bcead2c6b5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="cube-element-assl"></a>Cube 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]일반, 가상 또는 연결 된 큐브를 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cubes>  
   <Cube>  
            <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
            <Description>...</Description>  
            <Language>...</Language>  
            <Collation>...</Collation>  
            <Translations>...</Translations>  
      <Dimensions>...</Dimensions>  
            <CubePermissions>...</CubePermissions>  
      <MdxScripts>...</MdxScripts>  
      <Perspectives>...</Perspectives>  
      <State>...</State>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Visible>...</Visible>  
      <MeasureGroups>...</MeasureGroups>  
      <DataSourceView >...</Source>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
      <ProactiveCaching>...</ProactiveCaching>  
            <Kpis>...</Kpis>  
            <ErrorConfiguration>...</ErrorConfiguration>  
            <Actions>...</Actions>  
      <StorageLocation>...</StorageLocation>  
      <EstimatedRows>...</EstimatedRows>  
      <LastProcessed>...</LastProcessed>  
      <Annotations>...</Annotations>  
   </Cube>  
</Cubes>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../../../analysis-services/scripting/collections/cubes-element-assl.md)|  
|자식 요소|[작업](../../../analysis-services/scripting/collections/actions-element-assl.md), [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md), [주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [데이터 정렬](../../../analysis-services/scripting/properties/collation-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [ CubePermissions](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md), [DefaultMeasure](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md), [설명](../../../analysis-services/scripting/properties/description-element-assl.md), [차원](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md) [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Kpi](../../../analysis-services/scripting/collections/kpis-element-assl.md), [언어](../../../analysis-services/scripting/properties/language-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [ LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md), [MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [큐브 뷰](../../../analysis-services/scripting/collections/perspectives-element-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md), [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md), [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md), [ScriptCacheProcessingMode](../../../analysis-services/scripting/properties/scriptcacheprocessingmode-element-assl.md), [상태 ](../../../analysis-services/scripting/properties/state-element-assl.md), [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md), [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md), [번역](../../../analysis-services/scripting/collections/translations-element-assl.md), [표시](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Cube>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
