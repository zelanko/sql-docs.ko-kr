---
title: Find 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e71776a43aa338246b4acb3b4d9f620c19234f0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748223"
---
# <a name="find-method-ado"></a>Find 메서드(ADO)
검색을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 지정된 된 조건을 만족 시키는 행에 대 한 합니다. 필요에 따라 검색, 시작 행 및 오프셋을 시작할 행의 방향을 지정할 수 있습니다. 현재 행 위치가 찾은 레코드;에 설정 된 조건이 충족 되 면 하는 경우 끝 (또는 시작) 위치 설정 되어이 고, 그렇지 합니다 **레코드 집합**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *조건*  
 A **문자열** 검색에 사용할 열 이름, 비교 연산자 및 값을 지정 하는 문을 포함 하는 값입니다.  
  
 *SkipRows*  
 선택적*합니다.* **긴** 값을 해당 기본값은 현재 행의 행 오프셋을 지정 하는 0 또는 *시작* 검색을 시작할 책갈피입니다. 기본적으로 현재 행에서 검색이 시작 됩니다.  
  
 *SearchDirection*  
 선택적*합니다.* A [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) 검색 방향 검색으로 다음 사용 가능한 행 또는 현재 행에서 시작 되어야 하는지 여부를 지정 하는 값입니다. 끝에 실패 한 검색이 중지 되는 **Recordset** 값이 **adSearchForward**합니다. 시작 부분에 실패 한 검색이 중지 되는 **Recordset** 값이 **adSearchBackward**합니다.  
  
 *시작*  
 (선택 사항) A **Variant** 검색 시작 위치와 작동 하는 책갈피입니다.  
  
## <a name="remarks"></a>Remarks  
 에 단일 열 이름만 지정할 수 있습니다 *조건을*합니다. 이 메서드는 여러 열 검색을 지원 하지 않습니다.  
  
 비교 연산자 *조건을* 될 수 있습니다 "**>**"(보다 큼),"**\<**" (보다 작음), "=" (같음), "> =" (보다 크거나 같음), "< =" (작거나 같음), "<>" (다음과 같지 않은 경우) 또는 "좋아요" (패턴 일치).  
  
 값 *조건을* 문자열, 부동 소수점 숫자 또는 날짜 일 수 있습니다. 문자열 값은 작은따옴표 또는 "#" (숫자 기호)를 사용 하 여 구분 기호로 분리 된 (예를 들어, "상태 '서울' =" 또는 "상태 = WA # #"). 날짜 값이 "#" (숫자 기호) 기호를 사용 하 여 구분 됩니다 (예를 들어, "start_date > #7 월 22 일/97 #"). 이러한 값 시간, 분 및 초를 나타내는 타임 스탬프를 포함할 수 있지만 시간 (밀리초)을 포함 하지 않아야 하거나 오류가 발생 합니다.  
  
 비교 연산자 "좋아요" 이면 문자열 값을 찾으려면 하나 이상의 원하는 문자나 부분 문자열에 별표 (*)를 포함할 수 있습니다. 예를 들어, "와 같은 상태 저는\*'" Maine, 등이 검색 합니다. 또한 값 내에 포함 된 부분 문자열을 찾으려면 선행 및 후행 별표를 사용할 수 있습니다. 예를 들어, "와 같은 상태 '\*으로\*'" Alaska, 사스, 매사추세츠와 일치 합니다.  
  
 별표 위에 표시 된 대로 시작과 조건 문자열의 끝 또는 조건 문자열의 끝에만 사용할 수 있습니다. 선행 와일드 카드로 별표를 사용할 수 없습니다 ('* str'), 또는 포함된 와일드 카드 문\*r'). 이렇게 하면 오류가 발생 합니다.  
  
> [!NOTE]
>  현재 행 위치를 호출 하기 전에 설정 되어 있지 않으면 오류가 발생 합니다 **찾을**합니다. 같은 행 위치를 설정 하는 모든 메서드가 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)를 호출 하기 전에 호출 해야 **찾을**합니다.  
  
> [!NOTE]
>  호출 하는 경우는 **찾을** 메서드는 레코드 집합 및 레코드 집합의 현재 위치에서 마지막 레코드 또는 파일 끝 (EOF) 이면 아무 것도 검색 되지 것입니다. 호출 해야 합니다 **MoveFirst** 레코드 집합의 시작 부분에 현재 위치/커서를 설정 하는 방법입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Find 메서드 예제 (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [인덱스 속성](../../../ado/reference/ado-api/index-property.md)   
 [Optimize 속성-동적 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek 메서드](../../../ado/reference/ado-api/seek-method.md)
