---
title: CompareBookmarks 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85ca76678c0d3e75a106164626c4e3c3a81bd7e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315981"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks 메서드(ADO)
두 개의 책갈피를 비교 하 여 상대 값 표시를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 [CompareEnum](../../../ado/reference/ado-api/compareenum.md) 해당 책갈피를 나타내는 두 레코드의 상대적인 행 위치를 나타내는 값입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *Bookmark1*  
 첫 번째 행의 책갈피입니다.  
  
 *Bookmark2*  
 두 번째 행의 책갈피입니다.  
  
## <a name="remarks"></a>Remarks  
 책갈피는 동일 하 게 적용 해야 합니다 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 **레코드 집합** 개체 및 해당 [복제](../../../ado/reference/ado-api/clone-method-ado.md)합니다. 서로 다른 책갈피를 안정적으로 비교할 수 없습니다 **레코드 집합** 동일한 원본 또는 명령에서 만들어진 경우에 개체입니다. 책갈피를 비교할 수 나는 **레코드 집합** 개체의 기본 공급자 비교를 지원 하지 않습니다.  
  
 책갈피 행을 고유 하 게 식별 하는 **레코드 집합** 개체입니다. 사용 된 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md) 해당 책갈피를 가져오려면 현재 행의 속성입니다.  
  
 ADO로 노출 하는 각 공급자에 게 특정 책갈피의 데이터 형식 이므로 **Variant**합니다. SQL Server 책갈피 DBTYPE_R8 형식의 예는 (**이중**). ADO이이 형식으로 노출 된 **Variant** 의 하위 형식을 사용 하 여 **Double**합니다.  
  
 책갈피를 비교 하는 경우 ADO는 모든 형식의 강제 변환 하지 않습니다. 값은 공급자에 전달 하기만 하면 됩니다 비교가 발생 합니다. 책갈피에 전달 하는 경우는 **CompareBookmarks** 메서드는 서로 다른 형식의 변수에 저장 된, 다음 유형 불일치 오류를 생성할 수 있습니다. "인수는 잘못 된 형식의 적절 한 범위를 벗어난 또는 서로 충돌 합니다."  
  
 잘못 되었거나 형식이 잘못 된 책갈피를 사용 하면 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [CompareBookmarks 메서드 예제 (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks 메서드 예제 (VC + +)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark 속성(ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
