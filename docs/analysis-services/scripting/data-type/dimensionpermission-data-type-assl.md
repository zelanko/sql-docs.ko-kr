---
title: "DimensionPermission 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DimensionPermission Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DimensionPermission data type
ms.assetid: 066405ff-903f-467a-b0d5-e58653952c52
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 12a84edf950081669776e18775d9191fe523d66c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dimensionpermission-data-type-assl"></a>DimensionPermission 데이터 형식(ASSL)
  데이터베이스 차원에 할당된 사용 권한을 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionPermission>  
   <!-- The following elements extend Permission -->  
   <AttributePermissions>...</AttributePermissions>  
   <AllowedRowsExpression>...</AllowedRowsExpression>  
</DimensionPermission>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[사용 권한](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[AttributePermissions](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md), [AllowedRowsExpression](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|  
|파생 요소|[DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 이 요소는 DeploymentMode 값 2(테이블 형식 서버 모드)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *AttributePermission* 특성은 비어 있어야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 이 요소는 DeploymentMode 값 0(OLAP)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *AllowedRowsExpression* 특성은 비어 있어야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DimensionPermission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

