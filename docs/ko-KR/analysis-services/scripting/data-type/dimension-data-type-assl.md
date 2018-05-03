---
title: 데이터 형식 (ASSL) 차원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Dimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Dimension data type
ms.assetid: 3fe6adc2-5206-44c3-a689-a731705f43ca
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6f1b35f0f1ce022d4f3f5ae60f4dfc02d5d5fba1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dimension-data-type-assl"></a>Dimension 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  데이터베이스 차원을 나타내는 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <Description>...</Description>  
   <Source>...</Source>  
   <MiningModelID>...</MiningModelID>  
   <Type>...</Type>  
   <UnknownMember>...</UnknownMember>  
   <MdxMissingMemberMode>...</MdxMissingMemberMode>  
   <ErrorConfiguration>...</ErrorConfiguration>  
   <StorageMode>...</StorageMode>  
   <WriteEnabled>...</WriteEnabled>  
   <ProcessingPriority>...</ProcessingPriority>  
   <LastProcessed>...</LastProcessed>  
   <DimensionPermissions>...</DimensionPermissions>  
   <DependsOnDimensionID>...</DependsOnDimensionID>  
   <Language>...</Language>  
   <Collation>...</Collation>  
   <UnknownMemberName>...</UnknownMemberName>  
   <UnknownMemberTranslations>...</UnknownMemberTranslations>  
   <State>...</State>  
   <ProactiveCaching>...</ProactiveCaching>  
   <ProcessingMode>...</ProcessingMode>  
   <CurrentStorageMode>...</CurrentStorageMode>  
   <Translations>...</Translations>  
   <Attributes>...</Attributes>  
   <AttributeAllMemberName>...</AttributeAllMemberName>  
   <AttributeAllMemberTranslations>...</AttributeAllMemberTranslations>  
   <Hierarchies>...</Hierarchies>  
   <Relationships>...</Annotations>  
   <Annotations>...</Annotations>  
</Dimension>  
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
|자식 요소|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AttributeAllMemberName](../../../analysis-services/scripting/properties/attributeallmembername-element-assl.md), [AttributeAllMemberTranslations](../../../analysis-services/scripting/collections/attributeallmembertranslations-element-assl.md), [Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md), [Collation](../../../analysis-services/scripting/properties/collation-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md), [DependsOnDimensionID](../../../analysis-services/scripting/properties/dependsondimensionid-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [DimensionPermissions](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [Hierarchies](../../../analysis-services/scripting/collections/hierarchies-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Language](../../../analysis-services/scripting/properties/language-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MdxMissingMemberMode](../../../analysis-services/scripting/properties/mdxmissingmembermode-element-assl.md), [MiningModelID](../../../analysis-services/scripting/properties/miningmodelid-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md), [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md), [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md), [Relationships](../../../analysis-services/scripting/collections/relationships-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [State](../../../analysis-services/scripting/properties/state-element-assl.md), [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md), [Type](../../../analysis-services/scripting/properties/type-element-dimension-assl.md), [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md), [UnknownMemberName](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md), [UnknownMemberTranslations](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md), [WriteEnabled](../../../analysis-services/scripting/properties/writeenabled-element-assl.md)|  
|파생 요소|[차원](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 이 데이터 형식은 DeploymentMode 값 1(SharePoint) 및 2(테이블 형식)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *WriteEnabled* 자식 요소는 다음으로 설정: **False**  
  
-   *UnknownMember* 자식 요소는 다음으로 설정: **AutomaticNull**  
  
-   모든 고유 특성의 *NullProcessing* 자식 요소는 다음으로 설정: **Error**  
  
 다음 자식 특성은 DeploymentMode 값 1(SharePoint) 및 2(테이블 형식)에서 지원되지 않습니다.  
  
-   *DimensionPermissions*  
  
-   *MiningModelID*  
  
-   *ProactiveCaching*  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.AggregationDimension>, <xref:Microsoft.AnalysisServices.AggregationDesignDimension>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.MeasureGroupDimension>, 및 <xref:Microsoft.AnalysisServices.PerspectiveDimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
