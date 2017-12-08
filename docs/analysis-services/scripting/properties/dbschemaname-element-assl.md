---
title: "DbSchemaName 요소 (ASSL) | Microsoft Docs"
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
apiname: DbSchemaName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DbSchemaName
helpviewer_keywords: DbSchemaName element
ms.assetid: ae0f0edd-7b76-400d-a288-39a36d2a746b
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e45aa795d343b11323bedf7430de85bef321050d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dbschemaname-element-assl"></a>DbSchemaName 요소(ASSL)
  로 식별 된 테이블의 부모 요소에 사용 되는 스키마의 이름이 고 [DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TableBinding> <!-- or TableNotification -->  
   ...  
   <DbSchemaName>...</DbSchemaName>  
   ...  
</TableBinding>  
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
|부모 요소|[TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md), [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **DbSchemaName** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.TableBinding> 및 <xref:Microsoft.AnalysisServices.TableNotification>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
