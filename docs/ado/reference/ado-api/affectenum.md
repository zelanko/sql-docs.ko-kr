---
description: AffectEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d67a4916328d5d6d435da1b8080be42e52b35f67
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776652"
---
# <a name="affectenum"></a>AffectEnum
작업의 영향을 받는 레코드를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|**레코드 집합**에 적용 된 [필터가](./filter-property.md) 없는 경우는 모든 레코드에 영향을 줍니다.<br /><br /> **필터** 속성이 문자열 조건 (예: "Author = ' Smith '")으로 설정 된 경우이 작업은 현재 챕터의 표시 되는 레코드에 영향을 줍니다.<br /><br /> **Filter** 속성이 [filtergroupenum](./filtergroupenum.md) 또는 책갈피 배열의 멤버로 설정 되 면 작업은 **레코드 집합**의 모든 행에 영향을 줍니다. **참고: adAffectAll** 는 Visual Basic 개체 브라우저에서 숨겨집니다.|  
|**adAffectAllChapters**|4|현재 적용 되는 **필터** 를 통해 표시 되지 않는 레코드 집합을 포함 하 여 **레코드 집합**의 모든 형제 챕터에 있는 모든 레코드에 영향을 줍니다.|  
|**adAffectCurrent**|1|현재 레코드에만 영향을 줍니다.|  
|**adAffectGroup**|2|현재 [필터](./filter-property.md) 속성 설정을 만족 하는 레코드에만 영향을 줍니다. 이 옵션을 사용 하려면 **필터** 속성을 **filtergroupenum** 값 또는 **책갈피** 배열로 설정 해야 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums.|  
|AdoEnums.|  
|AdoEnums. GROUP|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [CancelBatch 메서드(ADO)](./cancelbatch-method-ado.md)  
        [Delete 메서드(ADO 레코드 집합)](./delete-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [Resync 메서드](./resync-method.md)  
        [UpdateBatch 메서드](./updatebatch-method.md)  
    :::column-end:::
:::row-end:::