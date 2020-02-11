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
ms.openlocfilehash: 0d737c2f031fa3ba630eabb7e52dff0e056c3390
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919593"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks 메서드(ADO)
두 책갈피를 비교 하 여 상대 값의 표시를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>Return Value  
 책갈피로 표시 되는 두 레코드의 상대 행 위치를 나타내는 [Compareenum](../../../ado/reference/ado-api/compareenum.md) 값을 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *않고 책갈피 2*  
 첫 번째 행의 책갈피입니다.  
  
 *Bookmark2 등*  
 두 번째 행의 책갈피입니다.  
  
## <a name="remarks"></a>설명  
 책갈피는 동일한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 **레코드 집합** 개체와 해당 [복제본](../../../ado/reference/ado-api/clone-method-ado.md)에 적용 되어야 합니다. 동일한 원본이 나 명령에서 생성 된 경우에도 여러 **레코드 집합** 개체의 책갈피를 안정적으로 비교할 수 없습니다. 기본 공급자가 비교를 지원 하지 않는 **레코드 집합** 개체에 대 한 책갈피를 비교할 수도 없습니다.  
  
 책갈피는 **레코드 집합** 개체의 행을 고유 하 게 식별 합니다. 현재 행의 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md) 속성을 사용 하 여 책갈피를 가져옵니다.  
  
 책갈피의 데이터 형식은 각 공급자와 관련이 있으므로 ADO는이를 **변형**으로 제공 합니다. 예를 들어 SQL Server 책갈피의 형식은 DBTYPE_R8 (**Double**)입니다. ADO는 **Double**형식의 **Variant** 로이 형식을 표시 합니다.  
  
 책갈피를 비교할 때 ADO는 어떤 유형의 강제 변환도 시도 하지 않습니다. 값은 비교가 발생 하는 공급자에 게 전달 됩니다. **Comparebookmarks** 메서드에 전달 된 책갈피가 서로 다른 형식의 변수에 저장 되어 있는 경우 "인수가 잘못 된 형식이 고, 허용 되는 범위를 벗어남 또는 서로 충돌 합니다."와 같은 형식 불일치 오류를 생성할 수 있습니다.  
  
 잘못 되었거나 형식이 잘못 된 책갈피를 사용할 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [CompareBookmarks 메서드 예제 (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks 메서드 예제 (VC + +)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark 속성(ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
