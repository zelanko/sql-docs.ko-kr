---
title: "DatabasePermission 요소 (ASSL) | Microsoft Docs"
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
apiname: DatabasePermission Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DatabasePermission
helpviewer_keywords: DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c17db1238e4ceba510024ea64acdbc856ffdcb9b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="databasepermission-element-assl"></a>DatabasePermission 요소(ASSL)
  기본 사용 권한을 정의 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소는 특정 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DatabasePermissions>  
      <DatabasePermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <Administer>...</Administer>  
...</DatabasePermission>  
</DatabasePermissions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[사용 권한](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|기본값|False|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DatabasePermissions](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|  
|자식 요소|[관리](../../../analysis-services/scripting/properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 **DatabasePermission** 개체는 데이터베이스가 소유한 역할에 대해서만 존재할 수 있습니다. 모든 역할에 대해 **DatabasePermission** 개체는 하나만 존재할 수 있습니다.  
  
 이 요소는 DeploymentMode 값 2(테이블 형식 모델)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *Administer* 특성 기본값은 **False**로 설정됩니다. 단, 사용자에게 관리 권한이 있는 경우는 예외입니다. 관리 권한을 가진 사용자의 경우 특성 값이 **True**로 설정됩니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DatabasePermission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Role 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
