---
title: "구문 분석 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/05/2017
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
- PARSE
- PARSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PARSE function
ms.assetid: 6a2dbf10-f692-471b-9458-24d246963049
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3e172a7d68edc212ce4803103dc1f975e4bf89db
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="parse-transact-sql"></a>PARSE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 요청한 데이터 형식으로 변환된 식 결과를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>인수  
 *string_value*  
 **nvarchar**(4000)의 형식이 지정 된 값을 나타내는 값을 지정된 된 데이터 형식으로 구문 분석 합니다.  
  
 *string_value* 오류가 요청한 데이터 형식 또는 구문 분석 발생 한 유효한 표현 해야 합니다.  
  
 *data_type*  
 결과에 대해 요청된 데이터 형식을 나타내는 리터럴 값입니다.  
  
 *문화권*  
 문화권을 식별 하는 선택적 문자열 *string_value* 서식이 지정 됩니다.  
  
 경우는 *문화권* 인수를 제공 하지 않으면 현재 세션의 언어가 사용 됩니다. 이 언어는 SET LANGUAGE 문을 사용하여 명시적으로 또는 암시적으로 설정됩니다. *문화권* ;.NET Framework에서 지 원하는 모든 culture를 허용 하 여 명시적으로 지 원하는 언어로 제한 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 경우는 *문화권* 인수가 유효 하지 않을, 구문 분석 오류가 발생 합니다.  
  
## <a name="return-types"></a>반환 형식  
 요청한 데이터 형식으로 변환된 식 결과를 반환합니다.  
  
## <a name="remarks"></a>주의  
 PARSE에 인수로 전달된 Null 값은 두 가지 방법으로 처리됩니다.  
  
1.  Null 상수를 전달하는 경우 오류가 발생합니다. Null 값은 culture를 인식하는 방법으로 다른 데이터 형식으로 구문 분석될 수 없습니다.  
  
2.  런타임에 Null 값이 포함된 매개 변수를 전달할 경우 Null이 반환되며 전체 일괄 처리가 취소되지 않습니다.  
  
 PARSE는 문자열에서 날짜/시간 및 숫자 형식으로 변환하는 경우에만 사용하세요. 일반 형식 변환의 경우 이전처럼 CAST나 CONVERT를 사용합니다. 문자열 값을 구문 분석할 경우 성능에 영향을 주게 됩니다.  
  
 구문 분석 있는지 여부의는.NET Framework 런타임 CLR (공용 언어)에 의존합니다.  
  
 이 함수는 CLR이 있어야 실행되므로 원격에서 실행할 수 없습니다. CLR이 설치되어 있어야만 실행되는 함수를 원격에서 호출할 경우 원격 서버에서 오류가 발생합니다.  
  
 **Data_type 매개 변수에 대 한 자세한 내용**  
  
 에 대 한 값은 *data_type* 매개 변수 스타일 함께 다음 표에 표시 된 형식으로 제한 됩니다. 허용되는 패턴을 쉽게 알 수 있도록 스타일 정보가 나와 있습니다. 스타일에 대 한 자세한 내용은.NET Framework 설명서를 참조는 **System.Globalization.NumberStyles** 및 **DateTimeStyles** 열거형입니다.  
  
|범주|형식|.NET Framework 형식|사용되는 스타일|  
|--------------|----------|-------------------------|-----------------|  
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
  
### <a name="a-parse-into-datetime2"></a>1. Datetime2로 구문 분석  
  
```  
SELECT PARSE('Monday, 13 December 2010' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-13 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-parse-with-currency-symbol"></a>2. 통화 기호를 포함하는 PARSE  
  
```  
SELECT PARSE('€345,98' AS money USING 'de-DE') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
345.98  
  
(1 row(s) affected)  
```  
  
### <a name="c-parse-with-implicit-setting-of-language"></a>3. 언어의 암시적 설정을 포함하는 PARSE  
  
```  
-- The English language is mapped to en-US specific culture  
SET LANGUAGE 'English';  
SELECT PARSE('12/16/2010' AS datetime2) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-16 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
  
