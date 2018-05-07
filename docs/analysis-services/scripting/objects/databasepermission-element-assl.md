---
title: DatabasePermission 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 64c5ad057df22565b01667ddc30859ee1a4e3b26
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="databasepermission-element-assl"></a>DatabasePermission 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Role 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [개체 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
