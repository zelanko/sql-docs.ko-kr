---
title: Find 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d1e46954ec7a0983927b1d375615fe6e6cbf10ee
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="find-method-ado"></a>Find 메서드 (ADO)
검색 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 지정된 된 조건을 만족 시키는 행에 대 한 합니다. 필요에 따라 검색, 시작 행 및 행 시작에서 오프셋의 방향을 지정할 수 있습니다. 조건이 충족 되 면 검색 된 레코드로; 현재 행의 위치가 설정 됩니다. 그렇지 위치의 끝 (또는 시작)으로 설정 되 고 **레코드 집합**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *조건*  
 A **문자열** 검색에 사용할 열 이름, 비교 연산자 및 값을 지정 하는 문이 포함 된 값입니다.  
  
 *SkipRows*  
 선택적*합니다.* A **긴** 값, 기본값은 현재 행의 행 오프셋을 나타내는 0 또는 *시작* 책갈피는 검색을 시작 합니다. 기본적으로 현재 행에서 검색이 시작 됩니다.  
  
 *SearchDirection*  
 선택적*합니다.* A [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) 검색 현재 행 또는 검색의 방향에 사용 가능한 다음 행에서 시작 되어야 하는지 여부를 지정 하는 값입니다. 실패 한 검색 끝날 때 중지 된 **레코드 집합** 값이 **adSearchForward**합니다. 실패 한 검색의 시작 부분에서 중지 된 **레코드 집합** 값이 **adSearchBackward**합니다.  
  
 *시작*  
 (선택 사항) A **Variant** 검색을 위한 시작 위치로 서 작동 하는 책갈피입니다.  
  
## <a name="remarks"></a>주의  
 에 단일 열 이름만 지정할 수 있습니다 *조건*합니다. 이 메서드는 여러 열 검색을 지원 하지 않습니다.  
  
 비교 연산자 *조건* 될 수 있습니다 "**>**"(보다 큼),"**\<**" (보다 작음), "=" (같음), "> =" (보다 크거나 같음), "< =" (작거나 같음), "(같지 않음)," <> 또는 "좋아요" (패턴 일치).  
  
 값 *조건* 문자열, 부동 소수점 숫자 또는 날짜 수 있습니다. 문자열 값은 작은따옴표 또는 "#" (숫자 기호)로 구분 (예를 들어 "상태 = '서울'" 또는 "상태 = WA # #"). 날짜 값 표시 "#" (숫자 기호)로 구분 됩니다 (예를 들어 "start_date > #7/22/97 #"). 이러한 값 시간, 분 및 초를 나타내는 타임 스탬프 포함 될 수 있지만 밀리초를 포함 해야 하거나 오류가 발생 합니다.  
  
 비교 연산자가 있는 경우 "좋아요", 문자열 값에 별표 (*) 문자 또는 부분 문자열의 하나 이상의 항목을 찾을를 포함할 수 있습니다. 예를 들어 "와 같은 상태 중\*'", Maine 등이 검색 합니다. 선행 및 후행 별표를 사용 하 여 값 내에 포함 된 부분 문자열을 찾을 수 있습니다. 예를 들어 "와 같은 상태 '\*으로\*'" Alaska, 사스, 등이 검색 합니다.  
  
 별표 위에 표시 된 대로 시작과 조건 문자열의 끝에 나 조건 문자열의 끝에만 사용할 수 수 있습니다. 와일드 카드 앞으로 별표를 사용할 수 없습니다 ('* str'), 또는 다른 이름으로 포함된 와일드 카드 문\*r'). 이 인해 오류가 발생 합니다.  
  
> [!NOTE]
>  호출 하기 전에 현재 행 위치가 설정 되지 않은 경우 오류가 발생 합니다 **찾을**합니다. 와 같은 행 위치를 설정 하는 모든 메서드 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)를 호출 하기 전에 호출 해야 **찾을**합니다.  
  
> [!NOTE]
>  호출 하는 경우는 **찾을** 메서드는 레코드 및 레코드 집합의 현재 위치에서 마지막 레코드 또는 of 파일 끝 (EOF) 이면 아무 것도 검색 되지 것입니다. 호출 해야는 **MoveFirst** 메서드는 레코드 집합의 시작 부분으로 현재 위치/커서를 설정 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [(VB) 메서드 예제 찾기](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Index 속성](../../../ado/reference/ado-api/index-property.md)   
 [동적 속성 (ADO)를 최적화 합니다.](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek 메서드](../../../ado/reference/ado-api/seek-method.md)
