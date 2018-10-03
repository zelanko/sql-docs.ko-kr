---
title: Administer 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Administer Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Administer
helpviewer_keywords:
- Administer element
ms.assetid: 52924cd6-6176-47c8-ab17-4ee0e0ce42b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 682c65420383bcd3db70d1c477781c7db1193334
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149303"
---
# <a name="administer-element-assl"></a>Administer 요소(ASSL)
  연결 된 사용 권한 관리 권한이 포함 되는지 여부를 나타내는 [데이터베이스](../objects/database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DatabasePermission>  
      ...  
      <Administer>...</Administer>  
   ...  
</DatabasePermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DatabasePermission](../objects/databasepermission-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Administer` 요소는 사용자가 지정된 데이터베이스에서만 관리 기능을 수행할 수 있는지 여부를 나타냅니다. 서버 관리자 역할은 인스턴스에 포함된 모든 데이터베이스에서 관리 기능을 수행할 수 있습니다.  
  
 부모에 해당 하는 요소가 `Administer` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DatabasePermission>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Permission 데이터 형식 &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [역할 요소 &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
