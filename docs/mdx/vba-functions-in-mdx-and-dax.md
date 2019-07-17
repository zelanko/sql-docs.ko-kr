---
title: MDX 및 DAX의 VBA 함수 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 39a0db181f3b1d1a40af1a5fa27ba78366a9d2b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135017"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 및 DAX의 VBA 함수


  이 문서에서 사용 가능한 모든 VBA 함수에 대 한 교차 참조를 포함 [Visual Basic for Applications 기능](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) MDX에서 지원 되는 DAX 언어와 기능적 동등성 있으면 목록에서 메모를 포함 하는 또한; .  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 함수 참조  
  
|함수 이름|지원됨|참고|  
|-------------------|---------------|-----------|  
|Abs|DAX, MDX||  
|Array|지원되지 않음||  
|Asc|MDX만||  
|AscW|MDX만||  
|Atn|MDX만||  
|CallByName|지원되지 않음||  
|CBool|MDX만||  
|CByte|MDX만||  
|CCur|MDX만||  
|CDate|MDX만||  
|CDbl|MDX만||  
|CDec|MDX만||  
|Choose|MDX만||  
|Chr|MDX만||  
|CInt|MDX만||  
|CLng|MDX만||  
|CLngLng|지원되지 않음||  
|CLngPtr|지원되지 않음||  
|Command|지원되지 않음||  
|Cos|MDX만||  
|CreateObject 메서드|지원되지 않음||  
|CSng|MDX만||  
|CStr|MDX만||  
|CurDir|지원되지 않음||  
|CVar|MDX만||  
|CVErr|지원되지 않음||  
|Date|MDX만|**경고** 같은 다른 함수를 구현 하는 DAX 이름; DATE (Year, Month, Day) 함수를 지정된 된 인수에서 날짜 형식 값을 생성 하는 데 사용|  
|DateAdd|MDX만|**경고** 같은 다른 함수를 구현 하는 DAX dateadd 이름 (\<날짜 >, < number_of_intervals >\<간격 >)의 번호로 지정 된 날짜를 이동 하는 데 사용 하는 함수를 간격 지정|  
|DateDiff|MDX만||  
|DatePart|MDX만||  
|DateSerial|MDX만||  
|DateValue|DAX, MDX||  
|Day|DAX, MDX||  
|DDB|MDX만||  
|Dir|지원되지 않음||  
|DoEvents|지원되지 않음||  
|Environ|지원되지 않음||  
|EOF|지원되지 않음||  
|오류|지원되지 않음||  
|Exp|DAX, MDX||  
|FileAttr|지원되지 않음||  
|FileDateTime|지원되지 않음||  
|FileLen|지원되지 않음||  
|Filter|지원되지 않음|**경고** 동일한 이름의 다른 함수를 구현 하는 MDX; FILTER (Set_Expression, Logical_Expression) 함수는 지정 된 인수의 검색 조건에 따라 지정 된 집합을 필터링 한 결과 집합을 반환 합니다<br /><br /> **경고** 같은 다른 함수를 구현 하는 DAX 이름, 필터 (\<테이블 >,\<필터 >) 함수는 다른 테이블 또는 지정된 된 인수에서 식의 하위 집합을 나타내는 테이블 반환|  
|Fix|MDX만||  
|Format(Visual Basic for Applications)|DAX, MDX||  
|FormatCurrency|지원되지 않음||  
|FormatDateTime|지원되지 않음||  
|FormatNumber|지원되지 않음||  
|FormatPercent|지원되지 않음||  
|FreeFile|지원되지 않음||  
|FV|MDX만||  
|GetAllSettings|지원되지 않음||  
|GetAttr|지원되지 않음||  
|GetObject|지원되지 않음||  
|GetSetting|지원되지 않음||  
|Hex|MDX만||  
|Hour|DAX, MDX||  
|Iif|MDX만|**경고** DAX는 이름이 비슷한 함수를 구현 합니다. IF (logical_test, value_if_true, value_if_false) 함수입니다.|  
|IMEStatus|지원되지 않음||  
|입력|지원되지 않음||  
|InputBox|지원되지 않음||  
|InStr|MDX만||  
|InStrRev|지원되지 않음||  
|Int|DAX, MDX||  
|IPmt|MDX만||  
|IRR|MDX만||  
|IsArray|MDX만||  
|IsDateMDX만||  
|IsEmpty|MDX만||  
|IsError|DAX, MDX||  
|IsMissing|MDX만||  
|IsNull|MDX만||  
|IsNumeric|MDX만||  
|IsObject|지원되지 않음||  
|Join|지원되지 않음||  
|LBound|지원되지 않음||  
|LCase|MDX만||  
|왼쪽|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|지원되지 않음||  
|LOF|지원되지 않음||  
|Log|MDX만|**중요 한** 같은 다른 함수를 구현 하는 DAX 이름, LOG (number, base) 함수입니다. 지정된 인수를 통해 지정된 밑에 대한 로그를 반환합니다.|  
|LTrim|MDX만||  
|MacID|지원되지 않음||  
|MacScript|지원되지 않음||  
|Mid|DAX, MDX||  
|Minute|DAX, MDX||  
|MIRR|MDX만||  
|Month|DAX, MDX||  
|MonthName|지원되지 않음||  
|MsgBox|지원되지 않음||  
|지금|DAX, MDX||  
|NPer|MDX만||  
|NPV|MDX만||  
|Oct|MDX만||  
|Partition|MDX만||  
|Pmt|MDX만||  
|PPmt|MDX만||  
|PV|MDX만||  
|QBColor|MDX만||  
|Rate|MDX만||  
|바꾸기|지원되지 않음||  
|RGB|MDX만||  
|오른쪽|DAX, MDX||  
|Rnd|MDX만||  
|반올림|DAX, MDX||  
|RTrim|MDX만||  
|Second|DAX, MDX||  
|검색|지원되지 않음||  
|Sgn|DAX, MDX||  
|Shell|지원되지 않음||  
|Sin|MDX만||  
|SLN|MDX만||  
|Space|MDX만||  
|Spc|지원되지 않음||  
|분할|지원되지 않음||  
|Sqr|MDX만||  
|Str|MDX만||  
|StrComp|MDX만||  
|StrConv|MDX만||  
|String|MDX만||  
|StrReverse|지원되지 않음||  
|스위치|MDX만||  
|SYD|MDX만||  
|탭|지원되지 않음||  
|Tan|MDX만||  
|Time|지원되지 않음||  
|Timer|MDX만||  
|TimeSerial|MDX만||  
|TimeValue|DAX, MDX||  
|Trim|DAX, MDX||  
|TypeName|MDX만||  
|UBound|지원되지 않음||  
|UCase|MDX만||  
|Val|MDX만||  
|VarType|지원되지 않음||  
|Weekday|DAX, MDX||  
|WeekdayName|지원되지 않음||  
|Year|DAX, MDX||  
  
  
