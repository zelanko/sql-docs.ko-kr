---
title: Bookmark 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61fa4619bd70b170f13dbc879748364f019f8bdd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716301"
---
# <a name="bookmark-property-ado"></a>Bookmark 속성(ADO)
현재 레코드를 고유 하 게 식별 하는 책갈피를 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에서 현재 레코드를 설정 하거나를 **레코드 집합** 유효한 책갈피에서 식별 되는 레코드 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **Variant** 유효한 책갈피로 계산 되는 식입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **책갈피** 속성을 현재 레코드의 위치를 저장 하 고 언제 든 지 해당 레코드를 반환 합니다. 책갈피에만 사용할 수 있습니다 **레코드 집합** 책갈피 기능을 지 원하는 개체입니다.  
  
 여는 경우를 **레코드 집합** 개체 이면 각 레코드의 고유 책갈피입니다. 현재 레코드에 대 한 책갈피를 저장 하려면 값을 할당 합니다 **책갈피** 변수에 속성입니다. 언제 든 지 다른 레코드로 이동 후에 해당 레코드를 신속 하 게 반환 하려면 설정 합니다 **Recordset** 개체의 **책갈피** 속성을 해당 변수의 값입니다.  
  
 사용자는 책갈피의 값을 볼 수 있습니다. 또한 사용자가 책갈피 동일한 레코드를 참조 하는 두 책갈피 다른 값이 있을 수 있으므로 직접 비교할 수를 기대할 수 없습니다.  
  
 사용 하는 경우는 [복제](../../../ado/reference/ado-api/clone-method-ado.md) 의 복사본을 만드는 메서드를 **레코드 집합** 개체를 **책갈피** 속성 설정을 원래 값과 중복 **레코드 집합**  개체는 동일 하며 서로 교환해 서 사용할 수 있습니다. 그러나 서로 다른 책갈피를 사용할 수 없습니다 **레코드 집합** 동일한 원본 또는 명령에서 만들어진 경우에 서로 교체 하 여 개체입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용 되 면 **레코드 집합** 개체를 **책갈피** 속성은 항상 사용할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [BOF, EOF 및 책갈피 속성 예제 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF 및 책갈피 속성 예제 (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 메서드](../../../ado/reference/ado-api/supports-method.md)
