---
title: DimensionPermission 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DimensionPermission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DimensionPermission data type
ms.assetid: 066405ff-903f-467a-b0d5-e58653952c52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c783f0627ad82ae0d1f33388ad086f7eb60df82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096630"
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
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[사용 권한](permission-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[AttributePermissions](../collections/attributepermissions-element-assl.md), [AllowedRowsExpression](../collections/attributepermissions-element-assl.md)|  
|파생 요소|[DimensionPermission](../objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 이 요소는 DeploymentMode 값 2(테이블 형식 서버 모드)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *AttributePermission* 특성은 비어 있어야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 이 요소는 DeploymentMode 값 0(OLAP)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *AllowedRowsExpression* 특성은 비어 있어야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DimensionPermission>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
