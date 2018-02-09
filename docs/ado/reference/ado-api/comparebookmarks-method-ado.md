---
title: "불일치 메서드 (ADO) | Microsoft Docs"
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
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 431ffdb1a2be03404b4d0c3636f547b6c8cf8514
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="comparebookmarks-method-ado"></a>불일치 메서드 (ADO)
두 개의 책갈피를 비교 하 고 상대 값의 표시를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 [CompareEnum](../../../ado/reference/ado-api/compareenum.md) 책갈피를 나타내는 두 레코드의 상대적인 행 위치를 나타내는 값입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *Bookmark1*  
 첫 번째 행의 책갈피입니다.  
  
 *Bookmark2*  
 두 번째 행의 책갈피입니다.  
  
## <a name="remarks"></a>주의  
 책갈피는 동일 하 게 적용 해야 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 **레코드 집합** 개체 및 해당 [복제](../../../ado/reference/ado-api/clone-method-ado.md)합니다. 서로 다른 책갈피를 안정적으로 비교할 수 없으므로 **레코드 집합** 동일한 원본이 나 명령에서 생성 된 경우에 개체입니다. 도 책갈피를 비교할 수는 **레코드 집합** 개체의 기본 공급자는 비교를 지원 하지 않습니다.  
  
 책갈피 행을 고유 하 게 식별 하는 **레코드 집합** 개체입니다. 사용 하 여는 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md) 해당 책갈피를 현재 행의 속성입니다.  
  
 책갈피의 데이터 형식이 각 공급자에 따라, ADO로 노출 된 **Variant**합니다. SQL Server 책갈피 DBTYPE_R8 형식의 하는 예를 들어 (**Double**). ADO는이 형식으로 노출 된 **Variant** 의 하위 형식으로 **Double**합니다.  
  
 책갈피를 비교할 때 ADO에 모든 형식의 강제 변환 시도 하지 않습니다. 값은 단순히 공급자에 전달 됩니다 비교 발생 하는 위치. 책갈피에 전달 하는 경우는 **불일치** 메서드는 서로 다른 형식의 변수에 저장 된, 다음 형식 불일치 오류를 생성할 수 있습니다: "인수는 잘못 된 형식의 적절 한 범위를 벗어난 또는 충돌 서로. "  
  
 잘못 되었거나 형식이 잘못 하는 책갈피 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [불일치 예제 (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [예제에서는 불일치 (VC + +)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark 속성(ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
