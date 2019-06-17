---
title: GetRows 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6babeebec1eac78949f0a80eb0701b5b5ba1dcc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694833"
---
# <a name="getrows-method-ado"></a>GetRows 메서드(ADO)
여러 레코드를 검색 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 배열로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **Variant** 값인 2 차원 배열입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *행*  
 (선택 사항) A [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) 검색할 레코드의 수를 나타내는 값입니다. 기본값은 **adGetRowsRest**합니다.  
  
 *시작*  
 (선택 사항) **문자열** 값 또는 **Variant** 올 레코드에 대 한 책갈피로 계산 되는 **GetRows** 작업 시작 해야 합니다. 사용할 수도 있습니다는 [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) 값입니다.  
  
 *Fields*  
 (선택 사항) A **Variant** 필드 이름 또는 서 수 위치 번호 배열을 단일 필드 이름이 나 서 수 위치를 나타내는입니다. ADO 이러한 필드에만 데이터를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **GetRows** 에서 레코드를 복사 하는 메서드를 **레코드 집합** 2 차원 배열로 합니다. 첫 번째 첨자 필드를 식별 하 고 두 번째 레코드 번호를 식별 합니다. 합니다 *배열* 변수는 자동으로 올바른 차원이 구분 시 크기를 **GetRows** 메서드 데이터를 반환 합니다.  
  
 에 대 한 값을 지정 하지 않으면 합니다 *행* 인수를 **GetRows** 의 모든 레코드를 자동으로 검색 하는 메서드를 **레코드 집합** 개체. 를 사용할 수 있는 것 보다 더 많은 레코드를 요청 하는 경우 **GetRows** 만 사용할 수 있는 레코드 수를 반환 합니다.  
  
 경우는 **레코드 집합** 개체에 책갈피를 지 원하는에서 지정할 수 있는 레코드를 **GetRows** 메서드는 레코드의 값을 전달 하 여 데이터를 검색 하기 시작할 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md)의 속성을 *시작* 인수입니다.  
  
 필드를 제한 하려는 경우는 합니다 **GetRows** 호출이 반환 단일 필드 이름/번호 또는 필드 이름/번호 배열을 전달할 수 있습니다 합니다 *필드* 인수입니다.  
  
 호출한 후 **GetRows**, 읽지 않은 다음 레코드가 현재 레코드가, 또는 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성이로 설정 되어 **True** 레코드가 더 이상 없으면입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [GetRows 메서드 예제 (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows 메서드 예제(VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
