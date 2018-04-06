---
title: DataSource 데이터 형식 (ASSL) | Microsoft Docs
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
- DataSource Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataSource data type
ms.assetid: 05e8de8d-452d-4128-98a6-4437df227fec
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 68997a04b74297bdd56991110d5a1fe2d77dd33c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="datasource-data-type-assl"></a>DataSource 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]데이터 원본을 나타내는 추상 기본 데이터 형식을 정의 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.  
  
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
|파생 데이터 형식|[RelationalDataSource](../../../analysis-services/scripting/data-type/relationaldatasource-data-type-assl.md), [OlapDataSource](../../../analysis-services/scripting/data-type/olapdatasource-data-type-assl.md), [PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [ConnectionString](../../../analysis-services/scripting/properties/connectionstring-element-assl.md), [ConnectionStringSecurity](../../../analysis-services/scripting/properties/connectionstringsecurity-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [DataSourcePermission](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md), [설명](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [ImpersonationInfo](../../../analysis-services/scripting/properties/impersonationinfo-element-assl.md), [격리](../../../analysis-services/scripting/properties/isolation-element-assl.md), [LastSchemaUpdate ](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [ManagedProvider](../../../analysis-services/scripting/properties/managedprovider-element-assl.md), [MaxActiveConnections](../../../analysis-services/scripting/properties/maxactiveconnections-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [제한 시간](../../../analysis-services/scripting/properties/timeout-element-assl.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 아웃오브 라인 바인딩을 정의하는 경우 **Name** 요소는 선택적 요소입니다. **Name** 요소를 지정할 필요가 없으므로 큐브, 파티션 등에 대해 바인딩 내에서 데이터 원본을 정의할 수 있습니다. **Database** 요소에 포함된 데이터 원본의 경우에는 **Name** 이 필수적 요소입니다.  
  
 데이터 원본에 대한 자세한 내용은 [Data Sources in Multidimensional Models](../../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)를 참조하세요.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DataSource>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
