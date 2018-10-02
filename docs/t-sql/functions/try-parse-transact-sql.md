---
title: TRY_PARSE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_PARSE_TSQL
- TRY_PARSE
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_PARSE function
ms.assetid: 292bac1d-edd8-468c-8ff1-8c7de625bc55
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9968c95f42d2256054d472b53d5c9039c26c1865
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785561"
---
# <a name="tryparse-transact-sql"></a>TRY_PARSE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 요청한 데이터 형식으로 변환된 식 결과를 반환하거나 캐스팅에 실패한 경우 null을 반환합니다. TRY_PARSE는 문자열에서 날짜/시간 및 숫자 형식으로 변환하는 경우에만 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
TRY_PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>인수  
 *string_value*  
 지정된 데이터 형식으로 구문 분석할 형식이 지정된 값을 나타내는 **nvarchar(4000)** 값입니다.  
  
 *string_value*는 요청한 데이터 형식에 대한 유효한 표현이어야 합니다. 그렇지 않으면 TRY_PARSE는 null을 반환합니다.  
  
 *data_type*  
 결과에 대해 요청된 데이터 형식을 나타내는 리터럴입니다.  
  
 *culture*  
 *string_value*의 형식을 지정하는 데 사용되는 culture를 식별하는 선택적 문자열입니다.  
  
 *culture* 인수를 지정하지 않으면 현재 세션의 언어가 사용됩니다. 이 언어는 SET LANGUAGE 문을 사용하여 명시적으로 또는 암시적으로 설정됩니다. *culture*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 명시적으로 지원하는 언어로만 국한되지 않으며 .NET Framework에서 지원하는 모든 culture를 수용합니다. *culture* 인수가 유효하지 않을 경우 PARSE는 오류를 발생시킵니다.  
  
## <a name="return-types"></a>반환 형식  
 요청한 데이터 형식으로 변환된 식 결과를 반환하거나 캐스팅에 실패한 경우 Null을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 TRY_PARSE는 문자열에서 날짜/시간 및 숫자 형식으로 변환하는 경우에만 사용하세요. 일반 형식 변환의 경우 이전처럼 CAST나 CONVERT를 사용합니다. 문자열 값을 구문 분석할 경우 성능에 영향을 주게 됩니다.  
  
 TRY_PARSE는 .NET Framework CLR(공용 언어 런타임)이 설치되어 있어야 사용할 수 있습니다.  
  
 이 함수는 CLR이 있어야 실행되므로 원격에서 실행할 수 없습니다. CLR이 설치되어 있어야만 실행되는 함수를 원격에서 호출할 경우 원격 서버에서 오류가 발생합니다.  
  
 **data_type 매개 변수에 대한 자세한 정보**  
  
 *data_type* 매개 변수의 값은 다음 표에 나온 형식 및 스타일로 제한됩니다. 허용되는 패턴을 쉽게 알 수 있도록 스타일 정보가 나와 있습니다. 스타일에 대한 자세한 내용은 **System.Globalization.NumberStyles** 및 **DateTimeStyles** 열거형에 대한 .NET Framework 설명서를 참조하십시오.  
  
|범주|형식|.NET 형식|사용되는 스타일|  
|--------------|----------|---------------|-----------------|  
|숫자|bigint|Int64|NumberStyles.Number|  
|숫자|ssNoversion|Int32|NumberStyles.Number|  
|숫자|SMALLINT|Int16|NumberStyles.Number|  
|숫자|TINYINT|Byte|NumberStyles.Number|  
|숫자|Decimal|Decimal|NumberStyles.Number|  
|숫자|NUMERIC|Decimal|NumberStyles.Number|  
|숫자|FLOAT|Double|NumberStyles.Float|  
|숫자|REAL|단일|NumberStyles.Float|  
|숫자|SMALLMONEY|Decimal|NumberStyles.Currency|  
|숫자|money|Decimal|NumberStyles.Currency|  
|날짜 및 시간|날짜|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|Time|TimeSpan|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|DATETIME|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|smalldatetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|Datetime2|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|datetimeoffset|DateTimeOffset|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
  
 **culture 매개 변수에 대한 자세한 정보**  
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어와 .NET Framework culture 간 매핑을 보여 줍니다.  
  
|전체 이름|별칭|LCID|해당 culture|  
|---------------|-----------|----------|----------------------|  
|us_english|영어|1033|ko-KR|  
|Deutsch|독일어|1031|de-DE|  
|Français|프랑스어|1036|fr-FR|  
|日本語|일본어|1041|ja-JP|  
|Dansk|덴마크어|1030|da-DK|  
|Español|스페인어|3082|es-ES|  
|Italiano|이탈리아어|1040|it-IT|  
|Nederlands|네덜란드어|1043|nl-NL|  
|Norsk|노르웨이어|2068|nn-NO|  
|Português|포르투갈어|2070|pt-PT|  
|Suomi|핀란드어|1035|fi|  
|Svenska|스웨덴어|1053|sv-SE|  
|čeština|체코어|1029|Cs-CZ|  
|magyar|헝가리어|1038|Hu-HU|  
|polski|폴란드어|1045|Pl-PL|  
|română|루마니아어|1048|Ro-RO|  
|hrvatski|크로아티아어|1050|hr-HR|  
|slovenčina|슬로바키아어|1051|Sk-SK|  
|slovenski|슬로베니아어|1060|Sl-SI|  
|ελληνικά?|그리스어|1032|El-GR|  
|български|불가리아어|1026|bg-BG|  
|русский|러시아어|1049|Ru-RU|  
|Türkçe|터키어|1055|Tr-TR|  
|British|영어(영국)|2057|en-GB|  
|eesti|에스토니아어|1061|Et EE|  
|latviešu|라트비아어|1062|lv-LV|  
|lietuvių|리투아니아어|1063|lt-LT|  
|Português(브라질)|브라질어|1046|pt-BR|  
|繁體中文|중국어(번체)|1028|zh-TW|  
|한국어|한국어|1042|Ko-KR|  
|简体中文|중국어(간체)|2052|zh-CN|  
|아랍어|아랍어|1025|ar-SA|  
|ไทย|태국어|1054|Th-TH|  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example-of-tryparse"></a>1. TRY_PARSE의 간단한 예  
  
```  
SELECT TRY_PARSE('Jabberwokkie' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-detecting-nulls-with-tryparse"></a>2. TRY_PARSE를 사용하여 Null 검색  
  
```  
SELECT  
    CASE WHEN TRY_PARSE('Aragorn' AS decimal USING 'sr-Latn-CS') IS NULL  
        THEN 'True'  
        ELSE 'False'  
END  
AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
True  
  
(1 row(s) affected)  
```  
  
### <a name="c-using-iif-with-tryparse-and-implicit-culture-setting"></a>3. TRY_PARSE 및 암시적 culture 설정과 함께 IIF 사용  
  
```  
SET LANGUAGE English;  
SELECT IIF(TRY_PARSE('01/01/2011' AS datetime2) IS NULL, 'True', 'False') AS Result;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
False  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [PARSE&#40;Transact-SQL&#41;](../../t-sql/functions/parse-transact-sql.md)   
 [변환 함수&#40;Transact-SQL&#41;](../../t-sql/functions/conversion-functions-transact-sql.md)   
 [TRY_CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
