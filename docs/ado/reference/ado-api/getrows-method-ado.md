---
description: GetRows 메서드(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a197cf085c4c1d741c19a55524313edbd4c5906
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443565"
---
# <a name="getrows-method-ado"></a>GetRows 메서드(ADO)
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 여러 레코드를 배열로 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>Return Value  
 해당 값이 2 차원 배열인 **Variant** 를 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *행*  
 (선택 사항) 검색할 레코드 수를 나타내는 [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) 값입니다. 기본값은 **adGetRowsRest**입니다.  
  
 *시작*  
 (선택 사항) **GetRows** 작업을 시작 해야 하는 레코드의 책갈피로 계산 되는 **문자열** 값 또는 **변형** 입니다. [책갈피 열거형](../../../ado/reference/ado-api/bookmarkenum.md) 값을 사용할 수도 있습니다.  
  
 *필드*  
 (선택 사항) 단일 필드 이름 또는 서 수 위치를 나타내는 **Variant** 이거나, 필드 이름 또는 서 수 위치 번호의 배열입니다. ADO는 이러한 필드의 데이터만 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **GetRows** 메서드를 사용 하 여 레코드 **집합** 의 레코드를 2 차원 배열로 복사할 수 있습니다. 첫 번째 첨자는 필드를 식별 하 고 두 번째 첨자는 레코드 번호를 식별 합니다. **GetRows** 메서드가 데이터를 반환할 때 *배열* 변수는 올바른 크기로 자동 조정 됩니다.  
  
 *Rows* 인수 값을 지정 하지 않으면 **GetRows** 메서드가 **레코드 집합** 개체의 모든 레코드를 자동으로 검색 합니다. 사용할 수 있는 것 보다 많은 레코드를 요청 하는 경우 **GetRows** 는 사용 가능한 레코드 수만 반환 합니다.  
  
 **레코드 집합** 개체가 책갈피를 지 원하는 경우에는 **GetRows** 메서드가 *시작* 인수에 해당 레코드의 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md) 속성 값을 전달 하 여 데이터 검색을 시작 해야 하는 레코드를 지정할 수 있습니다.  
  
 **GetRows** 호출에서 반환 되는 필드를 제한 하려는 경우 *필드* 인수에서 단일 필드 이름/번호 또는 필드 이름/숫자의 배열을 전달할 수 있습니다.  
  
 **GetRows**를 호출한 후에는 읽지 않은 다음 레코드가 현재 레코드가 되 고, 레코드가 더 이상 없으면 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성이 **True** 로 설정 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [GetRows 메서드 예제 (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows 메서드 예제(VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
