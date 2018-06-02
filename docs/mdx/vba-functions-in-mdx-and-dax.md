---
title: MDX 및 DAX의 VBA 함수 | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a9764d4e302a663800bd71a5c7083d985ea230bc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582525"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 및 DAX의 VBA 함수
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  이 문서에서 사용할 수 있는 모든 VBA 함수의 상호 참조가 포함 [응용 프로그램 기능에 대 한 Visual Basic](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) 는 기능이 있을 DAX 언어에 해당 하는 경우 목록에서 메모를 포함 하는 또한; MDX에서 지원 되는 .  
  
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
|CreateObject|지원되지 않음||  
|CSng|MDX만||  
|CStr|MDX만||  
|CurDir|지원되지 않음||  
|CVar|MDX만||  
|CVErr|지원되지 않음||  
|date|MDX만|**경고** 같은 다른 함수를 구현 하는 DAX 이름; 지정된 된 인수에서 날짜 형식 값을 생성 하는 데 사용 하는 DATE (Year, Month, Day) 함수|  
|DateAdd|MDX만|**경고** 같은 다른 함수를 구현 하는 DAX 이름;는 DATEADD (\<날짜 >, < number_of_intervals >\<간격 >)의 수로 지정 된 날짜를 이동할 사용 되는 함수, 간격 지정|  
|DateDiff]|MDX만||  
|DatePart|MDX만||  
|DateSerial|MDX만||  
|DateValue]|DAX, MDX||  
|Day|DAX, MDX||  
|DDB|MDX만||  
|Dir|지원되지 않음||  
|DoEvents|지원되지 않음||  
|Environ|지원되지 않음||  
|EOF|지원되지 않음||  
|Error|지원되지 않음||  
|Exp|DAX, MDX||  
|FileAttr|지원되지 않음||  
|FileDateTime|지원되지 않음||  
|FileLen|지원되지 않음||  
|Assert|지원되지 않음|**경고** 이름이 같은 다른 함수를 구현 하는 MDX; 지정된 된 인수에서 검색 조건에 따라 지정 된 집합을 필터링 결과 집합을 반환 하는 FILTER (Set_Expression, Logical_Expression) 함수<br /><br /> **경고** 같은 다른 함수를 구현 하는 DAX 이름; FILTER (\<테이블 >,\<필터 >) 함수를 다른 테이블이 나 지정된 된 인수에서 식의 하위 집합을 표시 하는 테이블 반환|  
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
|Iif|MDX만|**경고** 이름의 유사한 기능을 구현 하는 DAX: IF (logical_test, value_if_true, value_if_false) 함수입니다.|  
|IMEStatus|지원되지 않음||  
|Input|지원되지 않음||  
|InputBox|지원되지 않음||  
|InStr|MDX만||  
|InStrRev|지원되지 않음||  
|정수|DAX, MDX||  
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
|NPer]|MDX만||  
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
|둘째|DAX, MDX||  
|Seek|지원되지 않음||  
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
|문자열]|MDX만||  
|StrReverse|지원되지 않음||  
|스위치|MDX만||  
|SYD|MDX만||  
|탭|지원되지 않음||  
|Tan|MDX만||  
|Time|지원되지 않음||  
|Timer|MDX만||  
|TimeSerial|MDX만||  
|TimeValue|DAX, MDX||  
|Trim]|DAX, MDX||  
|TypeName|MDX만||  
|UBound|지원되지 않음||  
|UCase|MDX만||  
|Val|MDX만||  
|VarType|지원되지 않음||  
|Weekday|DAX, MDX||  
|WeekdayName|지원되지 않음||  
|Year|DAX, MDX||  
  
  
