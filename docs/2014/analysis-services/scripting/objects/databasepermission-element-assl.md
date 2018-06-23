---
title: DatabasePermission 요소 (ASSL) | Microsoft Docs
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
- DatabasePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DatabasePermission
helpviewer_keywords:
- DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e47203616cc76fa09c0fd0658e7dad8a89c90a9b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36094055"
---
# <a name="databasepermission-element-assl"></a>DatabasePermission 요소(ASSL)
  기본 사용 권한을 정의 [데이터베이스](database-element-assl.md) 요소는 특정 [역할](role-element-assl.md) 요소입니다.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[사용 권한](../data-type/permission-data-type-assl.md)|  
|기본값|False|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DatabasePermissions](../collections/databasepermissions-element-assl.md)|  
|자식 요소|[관리](../properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `DatabasePermission` 개체는 데이터베이스가 소유한 역할에 대해서만 존재할 수 있습니다. 모든 역할에 대해 `DatabasePermission` 개체는 하나만 존재할 수 있습니다.  
  
 이 요소는 DeploymentMode 값 2(테이블 형식 모델)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *관리* 특성 기본값 설정은 `False`, 사용자에 게 관리 권한이 경우를 제외 하 고 있습니다. 관리 권한을 가진 사용자의 경우 특성 값이 `True`로 설정됩니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DatabasePermission>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Role 요소 &#40;ASSL&#41;](role-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  