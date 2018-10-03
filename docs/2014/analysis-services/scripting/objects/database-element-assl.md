---
title: Database 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Database Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DATABASE
helpviewer_keywords:
- Database element
ms.assetid: c3bc7eaf-ed0d-4395-a3b7-8d9cfacfe911
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46166d77185836c65fe1d026255620dfb87c1f66
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191033"
---
# <a name="database-element-assl"></a>Database 요소(ASSL)
  정의 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Databases>  
   <Database>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastUpdate>...</LastUpdate>  
      <Description>...</Description>  
      <State>   </State>  
      <AggregationPrefix>...</AggregationPrefix>  
      <EstimatedSize>...</EstimatedSize>  
      <LastProcessed>...</LastProcessed>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <Visible>...</Visible>  
      <MasterDatasourceID>...</MasterDataSourceID>  
      <Accounts>...</Accounts>  
      <DataSources>...</DataSources>  
      <DataSourceViews>...</DataSourceViews>  
      <Dimensions>...</Dimensions>  
      <Cubes>...</Cubes>  
      <MiningStructures>...</MiningStructures>  
            <Roles>...</Roles>  
      <Assemblies>...</Assemblies>  
      <DatabasePermissions>...</DatabasePermissions>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[데이터베이스](../collections/databases-element-assl.md)|  
|자식 요소|[계정](../collections/accounts-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md)를 [주석](../collections/annotations-element-assl.md)를 [어셈블리](../collections/assemblies-element-assl.md)를 [데이터 정렬을](../properties/collation-element-assl.md), [ CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [큐브](../collections/cubes-element-assl.md)를 [DatabasePermissions](../collections/databasepermissions-element-assl.md)를 [DataSources](../collections/datasources-element-assl.md)를 [DataSourceViews](../collections/datasourceviews-element-assl.md), [설명을](../properties/description-element-assl.md), [차원](../collections/dimensions-element-assl.md)를 [EstimatedSize](../properties/estimatedsize-element-assl.md)를 [ID](../properties/id-element-assl.md)를 [언어](../properties/language-element-assl.md), [ LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)를 [LastUpdate](../properties/lastupdate-element-assl.md)하십시오 [MasterDatasourceID](../properties/datasourceid-element-assl.md), [MiningStructures](../collections/miningstructures-element-assl.md), [이름을](../properties/name-element-assl.md)합니다 [역할](../collections/roles-element-assl.md), [상태](../properties/state-element-assl.md), [번역](../collections/translations-element-assl.md), [표시](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Database>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Server 요소 &#40;ASSL&#41;](server-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
