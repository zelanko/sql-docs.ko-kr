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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68135017"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 및 DAX의 VBA 함수


  이 문서는 MDX에서 지원 되는 [Visual Basic for Applications 함수](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) 에서 사용할 수 있는 모든 VBA 함수에 대 한 상호 참조를 포함 합니다. 또한 DAX 언어와 기능적으로 동일 하 게 작동 하는 경우 목록에는 메모를 포함 합니다.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 함수 참조  
  
|함수 이름|지원됨|메모|  
|-------------------|---------------|-----------|  
|Abs|DAX, MDX||  
|배열|지원되지 않음||  
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
|명령|지원되지 않음||  
|Cos|MDX만||  
|CreateObject|지원되지 않음||  
|CSng|MDX만||  
|CStr|MDX만||  
|CurDir|지원되지 않음||  
|CVar|MDX만||  
|CVErr|지원되지 않음||  
|Date|MDX만|**경고** DAX는 이름이 같은 다른 함수를 구현 합니다. 지정 된 인수에서 날짜 유형 값을 생성 하는 데 사용 되는 DATE (Year, Month, Day) 함수|  
|DateAdd|MDX만|**경고** DAX는 이름이 같은 다른 함수를 구현 합니다. 지정 된 날짜\<를 지정 된 간격 만큼 이동 하\<는 데 사용 되는 DATEADD (dates>, <number_of_intervals>, interval>) 함수입니다.|  
|DateDiff|MDX만||  
|DatePart|MDX만||  
|DateSerial|MDX만||  
|DateValue|DAX, MDX||  
|일|DAX, MDX||  
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
|Assert|지원되지 않음|**경고** MDX는 이름이 같은 다른 함수를 구현 합니다. FILTER (Set_Expression, Logical_Expression) 함수는 지정 된 인수의 검색 조건에 따라 지정 된 집합을 필터링 한 결과 집합을 반환 합니다.<br /><br /> **경고** DAX는 이름이 같은 다른 함수를 구현 합니다. FILTER (\<table>,\<filter>) 함수는 지정 된 인수에서 다른 테이블이 나 식의 하위 집합을 나타내는 테이블을 반환 합니다.|  
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
|Iif|MDX만|**경고** DAX는 name: IF (logical_test, value_if_true, value_if_false) 함수를 사용 하 여 유사한 함수를 구현 합니다.|  
|IMEStatus|지원되지 않음||  
|입력|지원되지 않음||  
|InputBox|지원되지 않음||  
|InStr|MDX만||  
|InStrRev|지원되지 않음||  
|Int|DAX, MDX||  
|IPmt|MDX만||  
|IRR|MDX만||  
|IsArray|MDX만||  
|IsDateMDX 전용||  
|IsEmpty|MDX만||  
|IsError|DAX, MDX||  
|IsMissing|MDX만||  
|IsNull|MDX만||  
|IsNumeric|MDX만||  
|IsObject|지원되지 않음||  
|Join|지원되지 않음||  
|LBound|지원되지 않음||  
|LCase|MDX만||  
|Left|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|지원되지 않음||  
|LOF|지원되지 않음||  
|로그|MDX만|**중요** DAX는 이름이 같은 다른 함수를 구현 합니다. 로그 (number, base) 함수입니다. 지정된 인수를 통해 지정된 밑에 대한 로그를 반환합니다.|  
|LTrim|MDX만||  
|MacID|지원되지 않음||  
|MacScript|지원되지 않음||  
|Mid|DAX, MDX||  
|Minute|DAX, MDX||  
|MIRR|MDX만||  
|월|DAX, MDX||  
|MonthName|지원되지 않음||  
|MsgBox|지원되지 않음||  
|지금|DAX, MDX||  
|NPer|MDX만||  
|NPV|MDX만||  
|Oct|MDX만||  
|파티션|MDX만||  
|Pmt|MDX만||  
|PPmt|MDX만||  
|PV|MDX만||  
|QBColor|MDX만||  
|비용|MDX만||  
|Replace|지원되지 않음||  
|RGB|MDX만||  
|Right|DAX, MDX||  
|Rnd|MDX만||  
|Round|DAX, MDX||  
|RTrim|MDX만||  
|초|DAX, MDX||  
|Seek|지원되지 않음||  
|Sgn|DAX, MDX||  
|셸|지원되지 않음||  
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
|시간|지원되지 않음||  
|Timer|MDX만||  
|TimeSerial|MDX만||  
|TimeValue|DAX, MDX||  
|Trim|DAX, MDX||  
|TypeName|MDX만||  
|UBound|지원되지 않음||  
|UCase|MDX만||  
|Val|MDX만||  
|VarType|지원되지 않음||  
|요일|DAX, MDX||  
|WeekdayName|지원되지 않음||  
|Year|DAX, MDX||  
  
  
