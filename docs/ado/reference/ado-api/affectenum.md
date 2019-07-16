---
title: AffectEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a936eb39583afff34dd317b85bc4198022b15e7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920752"
---
# <a name="affectenum"></a>AffectEnum
작업에 의해 영향을 받는 레코드를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|없는 경우는 [필터](../../../ado/reference/ado-api/filter-property.md) 에 적용 합니다 **레코드 집합**, 모든 레코드에 영향을 줍니다.<br /><br /> 경우는 **필터** 문자열 조건 속성 (같은 "작성자 'Smith' ="), 다음 작업은 현재 장의 표시 되는 레코드에 영향을 줍니다.<br /><br /> 경우는 **필터** 의 멤버 속성을 [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 책갈피, 작업의 배열에는 모든 행의 영향이 나는 **레코드 집합**. **참고: adAffectAll** Visual Basic 개체 브라우저에서 숨겨집니다.|  
|**adAffectAllChapters**|4|모든 레코드의 모든 형제 장에 있는 영향을 주는 합니다 **레코드 집합**를 비롯 한 모든 통해 표시 되지 않는 **필터** 현재 적용 되는.|  
|**adAffectCurrent**|1|현재 레코드를만 영향을 줍니다.|  
|**adAffectGroup**|2|현재 충족 하는 레코드에만 영향을 주는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성을 설정 합니다. 설정 해야 합니다 **필터** 속성을를 **FilterGroupEnum** 값 또는 배열을 **책갈피** 이 옵션을 사용 하 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
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
