---
title: DataSourcePermission 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4130cd2a0eb83b32c8bcdf703d10ca6305af619
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087623"
---
# <a name="datasourcepermission-element-assl"></a>DataSourcePermission 요소(ASSL)
  기본 사용 권한을 정의 [데이터 원본](../data-type/datasource-data-type-assl.md) 특정 데이터 형식 [역할](role-element-assl.md) 요소입니다.  
  
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
|기본값|없음|  
|카디널리티|0-n: 한 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataSourcePermissions](../collections/datasourcepermissions-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `DataSourcePermission` 개체는 데이터베이스가 소유한 역할에 대해서만 존재할 수 있습니다. 모든 역할에 대해 `DataSourcePermission` 개체는 하나만 존재할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [역할 요소 &#40;ASSL&#41;](role-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
