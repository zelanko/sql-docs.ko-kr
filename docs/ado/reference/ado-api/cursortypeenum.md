---
title: CursorTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6875e6b2b967cf73511c73bf4ca7cdafed21557b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="cursortypeenum"></a>CursorTypeEnum
사용 되는 커서의 유형을 지정는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|동적 커서를 사용 합니다. 추가, 변경 및 다른 사용자가 삭제 표시 되는 모든 종류의를 통해 이동 하 고는 **레코드 집합** 허용 책갈피를 제외 하 고 공급자 템플릿을 지원 하지 않는 경우.|  
|**adOpenForwardOnly**|0|기본. 정방향 전용 커서를 사용 합니다. 스크롤할 수 있습니다만 앞으로 레코드가 한다는 점을 제외 하면 정적 커서와 같습니다. 하나만 통과 해야 할 때 성능이 향상 된 **레코드 집합**합니다.|  
|**adOpenKeyset**|1.|키 집합 커서를 사용합니다. 다른 사용자를 삭제 하는에서 다른 사용자가 추가 하는 레코드를 볼 수 없다는 점을 제외 하면 동적 커서와 유사 프로그램 **레코드 집합**합니다. 다른 사용자가 데이터 변경 내용을 계속 표시 됩니다.|  
|**adOpenStatic**|3|데이터를 찾거나 보고서를 생성 하는 데 사용할 수 있는 레코드 집합의 정적 복사본이 며 정적 커서를 사용 합니다. 추가, 변경 또는 다른 사용자가 삭제 표시 되지 않습니다.|  
|**adOpenUnspecified**|-1|커서의 형식을 지정 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>적용 대상  
 [CursorType 속성(ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
