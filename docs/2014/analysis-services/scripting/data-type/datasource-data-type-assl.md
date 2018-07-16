---
title: DataSource 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DataSource Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSource data type
ms.assetid: 05e8de8d-452d-4128-98a6-4437df227fec
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b498ddc2dcfb4ef2a93d1da98401b4e0c57bdfa7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273369"
---
# <a name="datasource-data-type-assl"></a>DataSource 데이터 형식(ASSL)
  데이터 원본을 나타내는 추상 기본 데이터 형식을 정의 [데이터베이스](../objects/database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataSource>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ManagedProvider>...</ManagedProvider>  
   <ConnectionString>...</ConnectionString>  
   <ConnectionStringSecurity>...</ConnectionStringSecurity>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Isolation>...</Isolation>  
   <MaxActiveConnections>...</MaxActiveConnections>  
   <Description>...</Description>  
   <Timeout>...</Timeout>  
   <Annotations>...</Annotations>  
   <DataSourcePermission>...</DataSourcePermission>  
</DataSource>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|[RelationalDataSource](datasource-data-type-assl.md)하십시오 [OlapDataSource](olapdatasource-data-type-assl.md), [PushedDataSource](pusheddatasource-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [ConnectionString](../properties/connectionstring-element-assl.md)합니다 [ConnectionStringSecurity](../properties/connectionstringsecurity-element-assl.md)를 [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [DataSourcePermission](../collections/datasourcepermissions-element-assl.md), [설명을](../properties/description-element-assl.md)합니다 [ID](../properties/id-element-assl.md), [ImpersonationInfo](../properties/impersonationinfo-element-assl.md), [격리](../properties/isolation-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [ManagedProvider](../properties/managedprovider-element-assl.md)합니다 [MaxActiveConnections](../properties/maxactiveconnections-element-assl.md)를 [이름](../properties/name-element-assl.md), [제한 시간](../properties/timeout-element-assl.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 아웃오브 라인 바인딩을 정의하는 경우 `Name` 요소는 선택적 요소입니다. `Name` 요소를 지정할 필요가 없으므로 큐브, 파티션 등에 대해 바인딩 내에서 데이터 원본을 정의할 수 있습니다. `Database` 요소에 포함된 데이터 원본의 경우에는 `Name`이 필수적 요소입니다.  
  
 데이터 원본에 대한 자세한 내용은 [Data Sources in Multidimensional Models](../../multidimensional-models/data-sources-in-multidimensional-models.md)를 참조하세요.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DataSource>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
