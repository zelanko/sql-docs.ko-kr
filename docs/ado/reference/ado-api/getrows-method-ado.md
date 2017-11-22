---
title: "GetRows 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords: Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8a80f8619d636c13b8c76b4f867e7cbe6333a742
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="getrows-method-ado"></a>(ADO) 메서드
여러 레코드를 검색 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 배열에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **Variant** 값이 2 차원 배열입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *행*  
 (선택 사항) A [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) 검색할 레코드의 수를 나타내는 값입니다. 기본값은 **adGetRowsRest**합니다.  
  
 *시작*  
 (선택 사항) A **문자열** 값 또는 **Variant** 있는 레코드에 대 한 책갈피로 계산 되는 **GetRows** 작업을 시작 해야 합니다. 사용할 수도 있습니다는 [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) 값입니다.  
  
 *필드*  
 (선택 사항) A **Variant** 나타내는 단일 필드 이름 또는 서 수 위치 또는 배열 필드 이름 또는 서 수 위치 번호입니다. ADO 이러한 필드의 데이터에 대해서만 반환합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **GetRows** 레코드를 복사할 메서드는 **레코드 집합** 2 차원 배열에 있습니다. 첫 번째 첨자 필드를 식별 하 고 두 번째 레코드 번호를 식별 합니다. *배열* 변수에 자동으로 올바른 차원이 지정 된 시 크기는 **GetRows** 메서드 데이터를 반환 합니다.  
  
 에 대 한 값을 지정 하지 않으면는 *행* 인수는 **GetRows** 의 모든 레코드를 자동으로 검색 하는 메서드는 **레코드 집합** 개체입니다. 를 사용할 수 있는 것 보다 더 많은 레코드를 요청 하는 경우 **GetRows** 만 사용할 수 있는 레코드의 수를 반환 합니다.  
  
 경우는 **레코드 집합** 개체가 책갈피를 지 원하는에 지정할 수 있습니다는 레코드는 **GetRows** 해당 레코드의 값을 전달 하 여 데이터를 검색할 메서드를 시작 해야 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md)속성에는 *시작* 인수입니다.  
  
 필드를 제한 하려는 경우는 **GetRows** 호출이 반환 단일 필드 이름/번호 또는 필드 이름/번호의 배열을 전달할 수 있습니다는 *필드* 인수입니다.  
  
 호출한 후 **GetRows**, 읽지 않은 다음 레코드가 현재 레코드가, 또는 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성이 **True** 레코드가 더 이상 없는 경우.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [GetRows 메서드 예제 (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows 메서드 예제(VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
