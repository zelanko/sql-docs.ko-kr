---
title: AffectEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c0efaeacb53492eab6485ca9d89629f27e4dfcd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="affectenum"></a>AffectEnum
작업의 영향을 받는 레코드를 지정 합니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|없는 경우는 [필터](../../../ado/reference/ado-api/filter-property.md) 에 적용 된 **레코드 집합**, 모든 레코드에 영향을 줍니다.<br /><br /> 경우는 **필터** 문자열 조건 속성이 설정 되어 (같은 "작성자 'Smith' ="), 다음 작업을 현재 장에 표시 된 레코드에 영향을 줍니다.<br /><br /> 경우는 **필터** 속성의 멤버에는 [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 책갈피, 작업의 배열에는의 모든 행에 영향을 줍니다 또는 **레코드 집합**합니다. **참고:****adAffectAll** Visual Basic 개체 브라우저에서 숨길 수 있습니다.|  
|**adAffectAllChapters**|4|모든 레코드의 모든 형제 장에 있는 영향을 줍니다는 **레코드 집합**, 하나를 통해 표시 되지 않는 포함 하 여 **필터** 현재 적용 되어 있습니다.|  
|**adAffectCurrent**|1.|현재 레코드를만 영향을 줍니다.|  
|**adAffectGroup**|2|현재 만족 하는 레코드에만 영향을 줍니다 [필터](../../../ado/reference/ado-api/filter-property.md) 속성을 설정 합니다. 설정 해야 합니다는 **필터** 속성을 한 **FilterGroupEnum** 값 또는 배열 **책갈피** 이 옵션을 사용 하도록 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.Affect.ALL|  
|AdoEnums.Affect.ALLCHAPTERS|  
|AdoEnums.Affect.CURRENT|  
|AdoEnums.Affect.GROUP|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[CancelBatch 메서드(ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|[Delete 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|  
|[Resync 메서드](../../../ado/reference/ado-api/resync-method.md)|[UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)|
