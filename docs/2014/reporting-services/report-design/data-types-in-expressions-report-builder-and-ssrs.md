---
title: 식의 데이터 형식(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 94fdf921-270c-4c12-87b3-46b1cc98fae5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5db09273a26bd8dd596a6ae576b2f8f0cc414190
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106073"
---
# <a name="data-types-in-expressions-report-builder-and-ssrs"></a>식의 데이터 형식(보고서 작성기 및 SSRS)
  데이터 형식은 여러 종류의 데이터를 나타낼 때 이를 효율적으로 저장하고 처리할 수 있도록 합니다. 일반적인 데이터 형식으로는 텍스트(문자열이라고도 함), 소수 자릿수가 있거나 없는 숫자, 날짜 및 시간, 이미지 등이 있습니다. 보고서의 값은 RDL(Report Definition Language) 데이터 형식이어야 합니다. 보고서에서 값을 표시할 때 원하는 대로 값의 형식을 지정할 수 있습니다. 예를 들어 통화를 나타내는 필드는 보고서 정의에 부동 소수점 숫자로 저장되지만 이를 표시할 때는 사용자가 선택한 형식 속성에 따라 다양한 형식을 사용할 수 있습니다.  
  
 표시 형식에 대한 자세한 내용은 [보고서 항목 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-language-rdl-data-types-and-common-language-runtime-clr-data-types"></a>RDL(Report Definition Language) 데이터 형식 및 CLR(공용 언어 런타임) 데이터 형식  
 RDL 파일에 지정된 값은 RDL 데이터 형식이어야 합니다. 보고서를 컴파일 및 처리할 때 RDL 데이터 형식은 CLR 데이터 형식으로 변환됩니다. 다음 표에는 기본값으로 표시되는 변환이 나와 있습니다.  
  
|RDL 형식|CLR 형식|  
|--------------|---------------|  
|문자열|기본값: 문자열<br /><br /> Chart, GUID, Timespan|  
|Boolean|기본값: Boolean|  
|정수|기본값: Int64<br /><br /> Int16, Int32, Uint16, Uint64, Byte, Sbyte|  
|DateTime|기본값: DateTime<br /><br /> DateTimeOffset|  
|부동|기본값: Double<br /><br /> Single, Decimal|  
|이진|기본값: Byte[]|  
|Variant|Byte[]를 제외한 위의 모든 항목|  
|VariantArray|Variant의 배열|  
|직렬화 가능|Serializable로 표시되어 있거나 ISerializable을 구현하는 형식 또는 Variant|  
  
## <a name="understanding-data-types-and-writing-expressions"></a>데이터 형식 이해 및 식 작성  
 예를 들어 그룹 또는 필터 식을 정의하거나 집계를 계산할 때와 같이 식을 작성하여 값을 비교하거나 조합하는 경우에는 데이터 형식을 이해하는 것이 중요합니다. 비교 및 계산은 데이터 형식이 동일한 항목 간에만 유효합니다. 데이터 형식이 일치하지 않는 경우에는 식을 사용하여 보고서 항목의 데이터 형식을 명시적으로 변환해야 합니다.  
  
 다음 목록에서는 데이터를 다른 데이터 형식으로 변환해야 하는 경우를 설명합니다.  
  
-   한 데이터 형식의 보고서 매개 변수 값을 다른 데이터 형식의 데이터 세트 필드와 비교할 경우.  
  
-   서로 다른 데이터 형식의 값을 비교하는 필터 식을 작성할 경우  
  
-   서로 다른 데이터 형식의 필드를 조합하는 정렬 식을 작성할 경우  
  
-   서로 다른 데이터 형식의 필드를 조합하는 그룹 식을 작성할 경우  
  
-   데이터 원본에서 검색된 값을 한 데이터 형식에서 다른 데이터 형식으로 변환할 경우  
  
## <a name="determining-the-data-type-of-report-data"></a>보고서 데이터의 데이터 형식 확인  
 보고서 항목의 데이터 형식을 확인하려면 해당 항목의 데이터 형식을 반환하는 식을 작성합니다. 예를 들어 `MyField`필드의 데이터 형식을 표시하려면 테이블 셀에 `=Fields!MyField.Value.GetType().ToString()`식을 추가합니다. 그러면 `MyField`를 나타내는 데 사용되는 `System.String` 또는 `System.DateTime` 등의 CLR 데이터 형식이 표시됩니다.  
  
## <a name="converting-dataset-fields-to-a-different-data-type"></a>데이터 세트 필드를 다른 데이터 형식으로 변환  
 데이터 세트 필드를 보고서에 사용하기 전에 변환할 수도 있습니다. 다음 목록에서는 기존 데이터 세트 필드를 변환하는 방법을 설명합니다.  
  
-   데이터 세트 쿼리를 수정하여 변환된 데이터가 있는 새 쿼리 필드를 추가합니다. 관계형 또는 다차원 데이터 원본의 경우 데이터 원본 리소스를 사용하여 변환이 수행됩니다.  
  
-   하나의 결과 집합 열에 있는 모든 데이터를 다른 데이터 형식의 새 열로 변환하는 식을 작성하여 기존 보고서 데이터 세트 필드를 기반으로 하는 계산 필드를 만듭니다. 예를 들어 `=CStr(Fields!Year.Value)`식은 Year 필드를 정수 값에서 문자열 값으로 변환합니다. 자세한 내용은 [보고서 데이터 창에서 필드 추가, 편집, 새로 고침&#40;보고서 작성기 및 SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)을 참조하세요.  
  
-   사용 중인 데이터 처리 확장 프로그램에 미리 형식이 지정된 데이터를 검색하기 위한 메타데이터가 포함되어 있는지 확인합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 쿼리에는 큐브를 처리할 때 이미 형식이 지정된 큐브 값에 대한 FORMATTED_VALUE 확장 속성이 포함되어 있습니다. 자세한 내용은 [Analysis Services 데이터베이스에 대한 확장 필드 속성 &#40;SSRS&#41;](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)을 참조하세요.  
  
## <a name="understanding-parameter-data-types"></a>매개 변수 데이터 형식 이해  
 보고서 매개 변수 데이터 형식 중 하나 여야 합니다. 부울, DateTime, Integer, Float 또는 텍스트 (문자열이 라고도 함). 데이터 세트 쿼리에 쿼리 매개 변수가 포함되는 경우 보고서 매개 변수가 자동으로 만들어져 쿼리 매개 변수에 연결됩니다. 보고서 매개 변수의 기본 데이터 형식은 String입니다. 보고서 매개 변수의 기본 데이터 형식을 변경하려면 **보고서 매개 변수 속성** 대화 상자의 **일반** 페이지에 있는 **데이터 형식** 드롭다운 목록에서 올바른 값을 선택합니다.  
  
> [!NOTE]  
>  DateTime 데이터 형식인 보고서 매개 변수는 밀리초를 지원하지 않습니다. 밀리초가 포함된 값을 기반으로 하는 매개 변수를 만들 수 있지만 사용 가능한 값 드롭다운 목록에서 밀리초가 포함된 날짜 또는 시간 값이 들어 있는 값을 선택할 수는 없습니다.  
  
## <a name="writing-expressions-that-convert-data-types-or-extract-parts-of-data"></a>데이터 형식을 변환하거나 데이터의 일부를 추출하는 식 작성  
 연결 연산자(&)를 사용하여 텍스트와 데이터 집합 필드를 조합하는 경우 CLR(공용 언어 런타임)에서는 일반적으로 기본 형식을 제공합니다. 데이터 세트 필드 또는 매개 변수를 특정 데이터 형식으로 명시적으로 변환해야 하는 경우에는 CLR 메서드 또는 Visual Basic 런타임 라이브러리 함수를 사용하여 데이터를 변환해야 합니다.  
  
 다음 표에서는 데이터 형식의 변환 예를 보여 줍니다.  
  
|변환 유형|예제|  
|------------------------|-------------|  
|DateTime을 String으로 변환|`=CStr(Fields!Date.Value)`|  
|String을 DateTime으로 변환|`=DateTime.Parse(Fields!DateTimeinStringFormat.Value)`|  
|String을 DateTimeOffset으로 변환|`=DateTimeOffset.Parse(Fields!DateTimeOffsetinStringFormat.Value)`|  
|연도 추출|`=Year(Fields!TimeinStringFormat.Value)`<br /><br /> `-- or --`<br /><br /> `=Year(Fields!TimeinDateTimeFormat.Value)`|  
|Boolean을 Integer로 변환|`=CInt(Parameters!BooleanField.Value)`<br /><br /> -1은 True이고 0은 False입니다.|  
|Boolean을 Integer로 변환|`=System.Convert.ToInt32(Fields!BooleanFormat.Value)`<br /><br /> 1은 True이고 0은 False입니다.|  
|DateTimeOffset 값의 DateTime 부분만 변환|`=Fields!MyDatetimeOffset.Value.DateTime`|  
|DateTimeOffset 값의 Offset 부분만 변환|`=Fields!MyDatetimeOffset.Value.Offset`|  
  
 Format 함수를 사용하여 값의 표시 형식을 제어할 수도 있습니다. 자세한 내용은 [함수(Visual Basic)](https://go.microsoft.com/fwlink/?linkid=111483)를 참조하세요.  
  
## <a name="advanced-examples"></a>고급 예제  
 데이터 원본의 모든 데이터 형식에 대한 변환을 지원하지 않는 데이터 공급자를 사용하여 데이터 원본에 연결하는 경우 지원되지 않는 데이터 원본 형식의 기본 데이터 형식은 String이 됩니다. 다음 예제에서는 문자열로 반환되는 특정 데이터 형식에 대한 솔루션을 제공합니다.  
  
### <a name="concatenating-a-string-and-a-clr-datetimeoffset-data-type"></a>String 및 CLR DateTimeOffset 데이터 형식 연결  
 대부분의 데이터 형식에 대해 CLR에서는 사용자가 & 연산자를 사용하여 데이터 형식이 각기 다른 값을 하나의 문자열로 연결할 수 있도록 기본 변환을 제공합니다. 예를 들어 `="The date and time are: " & Fields!StartDate.Value` 식은 "The date and time are: "라는 텍스트와 <xref:System.DateTime> 값인 데이터 세트 필드 StartDate를 연결합니다.  
  
 일부 데이터 형식의 경우에는 ToString 함수를 포함해야 할 수 있습니다. 예를 들어 <xref:System.DateTimeOffset>System.DateTimeOffset `="The time is: " & Fields!StartDate.Value.ToString()`을 참조하세요.  
  
### <a name="converting-a-string-data-type-to-a-clr-datetime-data-type"></a>String 데이터 형식을 CLR DateTime 데이터 형식으로 변환  
 데이터 처리 확장 프로그램에서 데이터 원본에 정의된 일부 데이터 형식을 지원하지 않는 경우 데이터는 텍스트로 검색될 수 있습니다. 예를 들어 `datetimeoffset(7)` 데이터 형식 값은 String 데이터 형식으로 검색될 수 있습니다. 오스트레일리아의 퍼스에서 2008년 7월 1일 오전 6:05:07.9999999의 문자열 값은 다음과 같습니다.  
  
 `2008-07-01 06:05:07.9999999 +08:00`  
  
 이 예제에서는 날짜(2008년 7월 1일), 소수 자릿수가 7개인 시간(오전 6:05:07.9999999), 시간 및 분 단위의 UTC 표준 시간대 오프셋(더하기 8시간 0분)을 차례로 보여 줍니다. 다음 예제에서 이 값은 `MyDateTime.Value`라는 `String` 필드에 배치됩니다.  
  
 다음 방법 중 하나를 사용하여 이 데이터를 하나 이상의 CLR 값으로 변환할 수 있습니다.  
  
-   입력란에서 식을 사용하여 문자열의 일부를 추출합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    -   다음 식은 UTC 표준 시간대 오프셋의 시간 부분만 추출하여 분으로 변환합니다. `=CInt(Fields!MyDateTime.Value.Substring(Fields!MyDateTime.Value.Length-5,2)) * 60`  
  
         결과는 `480`입니다.  
  
    -   다음 식은 문자열을 날짜 및 시간 값으로 변환합니다. `=DateTime.Parse(Fields!MyDateTime.Value)`  
  
         `MyDateTime.Value` 문자열에 UTC 오프셋이 있는 경우 `DateTime.Parse` 함수는 먼저 UTC 오프셋(오전 7시: UTC 시간인 전날 밤 오후 11시 + [`+08:00`])에 맞게 조정합니다. 그런 다음 `DateTime.Parse` 함수는 로컬 보고서 서버의 UTC 오프셋을 적용하고, 필요한 경우 일광 절약 시간제에 맞게 시간을 다시 조정합니다. 예를 들어 워싱턴의 레드몬드에서 일광 절약 시간제에 맞게 조정된 현지 시간 오프셋은 `[-07:00]`이거나 오후 11시로부터 7시간 전입니다. 결과 다음 `DateTime` 값: `2007-07-06 04:07:07 PM` (2007 7 월 6 일 오후 4시 07분)입니다.  
  
 문자열을 변환 하는 방법에 대 한 자세한 내용은 `DateTime` 데이터 형식 참조 [구문 분석 하는 날짜 및 시간 문자열](https://go.microsoft.com/fwlink/?LinkId=89703)를 [특정 문화권에 대 한 시간과 날짜 서식 지정](https://go.microsoft.com/fwlink/?LinkId=89704), 및 [선택 DateTime, DateTimeOffset 및 TimeZoneInfo 간의](https://go.microsoft.com/fwlink/?linkid=110652) MSDN에 있습니다.  
  
-   식을 사용하여 문자열의 일부를 추출하는 새 계산 필드를 보고서 데이터 세트에 추가합니다. 자세한 내용은 [보고서 데이터 창에서 필드 추가, 편집, 새로 고침&#40;보고서 작성기 및 SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)을 참조하세요.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수로 날짜 및 시간 값을 독립적으로 추출하여 별도의 열을 만들도록 보고서 데이터 집합 쿼리를 변경합니다. 다음 예제에서는 `DatePart` 함수를 사용하여 연도에 대한 열과 분으로 변환된 UTC 표준 시간대에 대한 열을 추가하는 방법을 보여 줍니다.  
  
     `SELECT`  
  
     `MyDateTime,`  
  
     `DATEPART(year, MyDateTime) AS Year,`  
  
     `DATEPART(tz, MyDateTime) AS OffsetinMinutes`  
  
     `FROM MyDates`  
  
     결과 집합에는 세 개의 열이 있습니다. 첫 번째 열은 날짜 및 시간 열이고, 두 번째 열은 연도 열이며, 세 번째 열은 UTC 오프셋(분) 열입니다. 다음 행에서는 예제 데이터를 보여 줍니다.  
  
     `2008-07-01 06:05:07             2008                   480`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 데이터 형식에 대한 자세한 내용은 [SQL Server 온라인 설명서](https://go.microsoft.com/fwlink/?linkid=120955)의 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) 및 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 형식에 대한 자세한 내용은 [SQL Server 온라인 설명서](../../analysis-services/multidimensional-models/olap-physical/data-types-in-analysis-services.md) 의 [SQL Server Books Onl의e](https://go.microsoft.com/fwlink/?linkid=120955)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 항목 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)  
  
  
