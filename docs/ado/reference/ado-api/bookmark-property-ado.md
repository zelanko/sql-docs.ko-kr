---
title: "책갈피 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c6076acd2bde7e82bf142bad76093d582106877
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="bookmark-property-ado"></a>책갈피 속성 (ADO)
현재 레코드를 고유 하 게 식별 하는 책갈피를 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 현재 레코드를 설정 하거나는 **레코드 집합** 유효한 책갈피로 식별 되는 레코드에는 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **Variant** 유효한 책갈피로 계산 되는 식입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **책갈피** 속성을 현재 레코드의 위치를 저장 하 고 언제 든 지 해당 레코드를 반환 합니다. 책갈피에만 사용할 수 있는 **레코드 집합** 책갈피 기능을 지 원하는 개체입니다.  
  
 열 때는 **레코드 집합** 개체 이면 각 레코드의 고유 책갈피입니다. 현재 레코드에 대 한 책갈피를 저장 하려면 형식의 값을 할당할는 **책갈피** 변수에 속성입니다. 언제 든 지 다른 레코드로 이동한 후에 해당 레코드를 신속 하 게 반환 하려면 설정는 **레코드 집합** 개체의 **책갈피** 속성을 해당 변수의 값입니다.  
  
 사용자는 책갈피의 값을 보려면 못할 수 있습니다. 또한 사용자가 직접 비교할 기대 하지??? 동일한 레코드를 참조 하는 두 책갈피 값이 다 수 있습니다.  
  
 사용 하는 경우는 [복제](../../../ado/reference/ado-api/clone-method-ado.md) 의 복사본을 만드는 메서드는 **레코드 집합** 개체는 **책갈피** 원본 데이터베이스와 복제에 대 한 속성 설정을 **레코드 집합**  개체는 동일 하며 같은 의미로 사용할 수 있습니다. 그러나 다른 책갈피를 사용할 수 없습니다 **레코드 집합** 동일한 원본이 나 명령에서 생성 된 경우에 서로 교체 하 여 개체입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **레코드 집합** 개체는 **책갈피** 속성은 항상 사용할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [BOF, EOF, 및 책갈피 속성 예제 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF, 및 책갈피 속성 예제 (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 메서드](../../../ado/reference/ado-api/supports-method.md)
