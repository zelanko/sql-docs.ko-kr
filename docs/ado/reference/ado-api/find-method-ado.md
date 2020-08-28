---
description: Find 메서드(ADO)
title: Find 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 18b4dc88dfedbb5a9a06968ebb5b02300439ed1b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972954"
---
# <a name="find-method-ado"></a>Find 메서드(ADO)
[레코드 집합](./recordset-object-ado.md) 에서 지정 된 조건을 만족 하는 행을 검색 합니다. 필요에 따라 검색의 방향, 시작 행 및 시작 행의 오프셋을 지정할 수 있습니다. 조건을 충족 하는 경우에는 현재 행 위치가 찾은 레코드에 대해 설정 됩니다. 그렇지 않으면 위치가 **레코드 집합**의 끝 (또는 시작)으로 설정 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *조건*  
 검색에 사용할 열 이름, 비교 연산자 및 값을 지정 하는 문을 포함 하는 **문자열** 값입니다.  
  
 *SkipRows*  
 선택 사항입니다. 기본값은 0 이며,이 값은 현재 행의 행 오프셋 또는 *시작* 책갈피를 지정 하 여 검색을 시작 하는 **Long** 값입니다. 기본적으로 검색은 현재 행에서 시작 됩니다.  
  
 *SearchDirection*  
 선택 사항입니다. 검색을 현재 행에서 시작할지 아니면 검색 방향으로 사용할 수 있는 다음 행으로 시작할지를 지정 하는 [SearchDirectionEnum](./searchdirectionenum.md) 값입니다. 값이 **Adsearchforward**인 경우 **레코드 집합** 의 끝에서 실패 한 검색을 중지 합니다. 값이 **Adsearchbackward**인 경우 **레코드 집합** 의 시작 부분에서 실패 한 검색을 중지 합니다.  
  
 *시작*  
 선택 사항입니다. 검색의 시작 위치로 작동 하는 **변형** 책갈피입니다.  
  
## <a name="remarks"></a>설명  
 *조건*에는 단일 열 이름만 지정할 수 있습니다. 이 메서드는 다중 열 검색을 지원 하지 않습니다.  
  
 *조건의* 비교 연산자는 " **>** " (보다 큼), "* * \<**" (less than), "=" (equal), "> =" (크거나 같음), "<=" (작거나 같음), "<>" (같지 않음) 또는 "like" (패턴 일치) 일 수 있습니다.  
  
 *조건* 에 있는 값은 문자열, 부동 소수점 숫자 또는 날짜 일 수 있습니다. 문자열 값은 작은따옴표 또는 "#" (숫자 기호) 표시 (예: "state = ' WA '" 또는 "state = #WA #")로 구분 됩니다. 날짜 값은 "#" (숫자 기호) 표시 (예: "start_date > #7/22/97 #")로 구분 됩니다. 이러한 값에는 시간 스탬프를 나타내는 시간, 분, 초 등이 포함 될 수 있지만 밀리초를 포함 하거나 오류가 발생 합니다.  
  
 비교 연산자가 "like" 이면 문자열 값에 별표 (*)를 포함 하 여 하나 이상의 문자 또는 하위 문자열을 찾을 수 있습니다. 예를 들어 "m '과 같은 상태는 \* Maine 및 Massachusetts와 일치 합니다. 선행 및 후행 별표를 사용 하 여 값 내에 포함 된 하위 문자열을 찾을 수도 있습니다. 예를 들어 "as '와 같은 ' state '는 \* \* 알래스카, 아칸 사스 및 Massachusetts와 일치 합니다.  
  
 별표는 위와 같이 조건 문자열의 끝 이나 조건 문자열의 시작 부분 및 끝 부분 에서만 사용할 수 있습니다. 별표는 선행 와일드 카드 (' * str ') 또는 포함 된 와일드 카드 (' r ')로 사용할 수 없습니다 \* . 그러면 오류가 발생 합니다.  
  
> [!NOTE]
>  **Find**를 호출 하기 전에 현재 행 위치를 설정 하지 않은 경우 오류가 발생 합니다. [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)와 같이 행 위치를 설정 하는 메서드는 **Find**를 호출 하기 전에 호출 해야 합니다.  
  
> [!NOTE]
>  레코드 집합에서 **find** 메서드를 호출 하 고 레코드 집합의 현재 위치가 마지막 레코드나 파일의 끝 (EOF)에 있는 경우 아무것도 찾지 못합니다. **MoveFirst** 메서드를 호출 하 여 현재 위치/커서를 레코드 집합의 시작 부분으로 설정 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Find 메서드 예제 (VB)](./find-method-example-vb.md)   
 [인덱스 속성](./index-property.md)   
 [Optimize 속성-동적 (ADO)](./optimize-property-dynamic-ado.md)   
 [Seek 메서드](./seek-method.md)