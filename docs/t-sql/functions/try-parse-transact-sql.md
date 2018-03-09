---
title: TRY_PARSE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRY_PARSE_TSQL
- TRY_PARSE
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_PARSE function
ms.assetid: 292bac1d-edd8-468c-8ff1-8c7de625bc55
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0b26f46431909dd4fbfaa820db8c3869333f555d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
 **nvarchar (4000)** 지정된 된 데이터 형식으로 구문 분석 한 서식이 지정 된 값을 나타내는 값입니다.  
  
 *string_value* 요청한 데이터 형식 또는 null을 반환 하는 TRY_PARSE의 유효한 표현 이어야 합니다.  
  
 *data_type*  
 결과에 대해 요청된 데이터 형식을 나타내는 리터럴입니다.  
  
 *문화권*  
 문화권을 식별 하는 선택적 문자열 *string_value* 서식이 지정 됩니다.  
  
 경우는 *문화권* 인수 제공 하지 않으면, 현재 세션의 언어가 사용 됩니다. 이 언어는 SET LANGUAGE 문을 사용하여 명시적으로 또는 암시적으로 설정됩니다. *문화권* ;.NET Framework에서 지 원하는 모든 culture를 허용 하 여 명시적으로 지 원하는 언어로 제한 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 경우는 *문화권* 인수가 유효 하지 않을, 구문 분석 오류가 발생 합니다.  
  
## <a name="return-types"></a>반환 형식  
 요청한 데이터 형식으로 변환된 식 결과를 반환하거나 캐스팅에 실패한 경우 Null을 반환합니다.  
  
## <a name="remarks"></a>주의  
 TRY_PARSE는 문자열에서 날짜/시간 및 숫자 형식으로 변환하는 경우에만 사용하세요. 일반 형식 변환의 경우 이전처럼 CAST나 CONVERT를 사용합니다. 문자열 값을 구문 분석할 경우 성능에 영향을 주게 됩니다.  
  
 TRY_PARSE는 .NET Framework CLR(공용 언어 런타임)이 설치되어 있어야 사용할 수 있습니다.  
  
 이 함수는 CLR이 있어야 실행되므로 원격에서 실행할 수 없습니다. CLR이 설치되어 있어야만 실행되는 함수를 원격에서 호출할 경우 원격 서버에서 오류가 발생합니다.  
  
 **Data_type 매개 변수에 대 한 자세한 내용**  
  
 에 대 한 값은 *data_type* 매개 변수 스타일 함께 다음 표에 표시 된 형식으로 제한 됩니다. 허용되는 패턴을 쉽게 알 수 있도록 스타일 정보가 나와 있습니다. 스타일에 대 한 자세한 내용은.NET Framework 설명서를 참조는 **System.Globalization.NumberStyles** 및 **DateTimeStyles** 열거형입니다.  
  
|범주|형식|.NET 형식|사용되는 스타일|  
|--------------|----------|---------------|-----------------|  
|숫자|bigint|Int64|NumberStyles.Number|  
|숫자|int|Int32|NumberStyles.Number|  
|숫자|smallint|Int16|NumberStyles.Number|  
|숫자|tinyint|Byte|NumberStyles.Number|  
|숫자|decimal|Decimal|NumberStyles.Number|  
|숫자|numeric|Decimal|NumberStyles.Number|  
|숫자|float|Double|NumberStyles.Float|  
|숫자|real|단일|NumberStyles.Float|  
|숫자|smallmoney|Decimal|NumberStyles.Currency|  
|숫자|money|Decimal|NumberStyles.Currency|  
|날짜 및 시간|date|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|time|TimeSpan|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|datetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|smalldatetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|datetime2|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|날짜 및 시간|datetimeoffset|DateTimeOffset|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
  
 **문화권 매개 변수에 대 한 자세한 내용**  
  
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
|Português (브라질)|브라질어|1046|pt-BR|  
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
  
## <a name="see-also"></a>관련 항목:  
 [Parse&#40; Transact SQL &#41;](../../t-sql/functions/parse-transact-sql.md)   
 [변환 함수 &#40; Transact SQL &#41;](../../t-sql/functions/conversion-functions-transact-sql.md)   
 [TRY_CONVERT &#40; Transact SQL &#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
