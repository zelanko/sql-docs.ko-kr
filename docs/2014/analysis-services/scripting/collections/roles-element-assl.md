---
title: Roles 요소 (ASSL) | Microsoft Docs
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
- Roles Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Roles
helpviewer_keywords:
- Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6227c72cc4fdd20b8c739bcb6019a83fbaaaa58
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295583"
---
# <a name="roles-element-assl"></a>Roles 요소(ASSL)
  부모 요소 아래에 정의된 [Role](../objects/role-element-assl.md) 요소의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Database> <!-- or Server -->  
   ...  
   <Roles>  
      <Role>...</Role>  
   </Roles>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Database](../objects/database-element-assl.md), [Server](../objects/server-element-assl.md)|  
|자식 요소|[역할](../objects/role-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `Roles` 요소와 연결된 `Server` 요소는 관리자라는 하나의 역할만 포함하며, 이는 서버 관리자 역할을 나타냅니다. 서버 관리자 역할은 변경 또는 삭제할 수 없으며 컬렉션에 다른 역할을 추가할 수도 없습니다.  
  
 `Roles` 요소와 연결된 `Database` 요소는 해당 데이터베이스에 대해 정의된 역할을 포함합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.RoleCollection>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
