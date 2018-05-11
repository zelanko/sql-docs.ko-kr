---
title: Administer 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 59b73f6cc648eaa35d53add20205aa483bc5bb76
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="administer-element-assl"></a>Administer 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  연결 된 사용 권한 관리 권한이 포함 되는지 여부를 나타냅니다는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DatabasePermission>  
      ...  
      <Administer>...</Administer>  
   ...  
</DatabasePermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Administer** 요소는 사용자가 지정된 데이터베이스에서만 관리 기능을 수행할 수 있는지 여부를 나타냅니다. 서버 관리자 역할은 인스턴스에 포함된 모든 데이터베이스에서 관리 기능을 수행할 수 있습니다.  
  
 부모에 해당 하는 요소 **관리** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DatabasePermission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Permission 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [Role 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
