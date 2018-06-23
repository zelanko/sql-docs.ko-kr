---
title: DataSourcePermission 요소 (ASSL) | Microsoft Docs
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
- DataSourcePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSourcePermission element
ms.assetid: 6dc6fb13-034e-479a-902e-27f3fb78c33f
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9ca326118ce782962b0100c310ddb308af91f21b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091157"
---
# <a name="datasourcepermission-element-assl"></a>DataSourcePermission 요소(ASSL)
  기본 사용 권한을 정의 [DataSource](../data-type/datasource-data-type-assl.md) 는 특정 데이터 형식을 [역할](role-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataSourcePermissions>  
   <DataSourcePermission xsi:type="Permission">  
      <!-- No child elements other than those from Permission are defined -->  
...</DataSourcePermission>  
</DataSourcePermissions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[사용 권한](../data-type/permission-data-type-assl.md)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 한 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataSourcePermissions](../collections/datasourcepermissions-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DataSourcePermission` 개체는 데이터베이스가 소유한 역할에 대해서만 존재할 수 있습니다. 모든 역할에 대해 `DataSourcePermission` 개체는 하나만 존재할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Role 요소 &#40;ASSL&#41;](role-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  