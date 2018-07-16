---
title: StorageEngineUsed 요소 (XMLA) | Microsoft Docs
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
- StorageEngineUsed Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
ms.assetid: 98895c10-f3c2-4d8a-be94-6128c828561d
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c6c8f7cdca7fb8134a27c8d1319385861294893a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37203964"
---
# <a name="storageengineused-element-xmla"></a>StorageEngineUsed 요소(XMLA)
  현재 데이터베이스 유형에 대해 설명하는 읽기 전용 값을 포함합니다.  
  
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
            <StorageEngineUsed >...</StorageEngineUsed>  
   </Database>  
</Databases>  
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
|부모 요소|[database](../objects/database-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*기존의*|데이터베이스 모델은 MOLAP, ROLAP 또는 HOLAP 저장소 모드에 해당합니다.|  
|*InMemory*|데이터베이스 모델은 IMBI 저장소 모드에 해당합니다.|  
|*혼합*|데이터베이스 모델은 IMBI와 MOLAP, ROLAP 또는 HOLAP 저장소 모드를 혼합합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `StorageEngineUsed`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.StorageEngineUsed>입니다.  
  
 AMO(Analysis Management Objects) 개체 모델에서 `StorageEngineUsed`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.Database>입니다.  
  
  
