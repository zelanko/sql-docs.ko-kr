---
title: CursorTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 059d6bb8e621839ccf21bb4eb4251db08f427523
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761401"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
사용 되는 커서의 형식을 지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|동적 커서를 사용 합니다. 추가, 변경 및 다른 사용자가 삭제 표시 되는 모든 유형의 통해 이동 합니다 **레코드 집합** 허용 되는 책갈피를 제외 하 고 해당 공급자를 지원 하지 않는 경우.|  
|**adOpenForwardOnly**|0|기본. 정방향 전용 커서를 사용 합니다. 동일 하 게 정적 커서를 제외 하 고 레코드를 통해 앞으로 스크롤하여만 있습니다. 하나만 통과 해야 하는 경우 성능이 향상 됩니다는 **레코드 집합**합니다.|  
|**adOpenKeyset**|1|키 집합 커서를 사용합니다. 다른 사용자가 삭제 된 레코드에서 액세스할 수 없는 다른 사용자에 게 추가 하는 레코드를 볼 수 없다는 점을 제외 하 고 동적 커서를와 유사 하 **레코드 집합**합니다. 다른 사용자가 데이터 변경 내용을 계속 표시 됩니다.|  
|**adOpenStatic**|3|데이터를 찾거나 보고서를 생성 하는 데 사용할 수 있는 레코드 집합의 정적 복사본이 며 정적 커서를 사용 합니다. 추가, 변경 또는 다른 사용자가 삭제 표시 되지 않습니다.|  
|**adOpenUnspecified**|-1|커서의 유형을 지정 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>적용 대상  
 [CursorType 속성(ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
