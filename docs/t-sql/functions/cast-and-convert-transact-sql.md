---
title: "CAST 및 CONVERT (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs: TSQL
helpviewer_keywords:
- CAST function
- automatic data type conversion
- varbinary data type
- CONVERT function
- data types [SQL Server], converting
- large value data types
- implicit data type conversions
- image data type, converting
- explicit data type conversions [SQL Server]
- binary [SQL Server], converting
- text data type, converting
- date and time [SQL Server], cast and convert
- truncating conversions
- converting data types [SQL Server], conversion functions
- time zones [SQL Server]
- roundtrip conversions
ms.assetid: a87d0850-c670-4720-9ad5-6f5a22343ea8
caps.latest.revision: "136"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 56326d7862c004ac056e329e6cc05f7bbe056aea
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="cast-and-convert-transact-sql"></a>CAST 및 CONVERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

식을 다른 데이터 형식으로 변환합니다.  
예를 들어 다음 예제에서는 두 개의 다른 데이터 형식, 정밀도 수준이 다른으로 입력된 datatype을 변경 합니다.
```sql  
SELECT 9.5 AS Original, CAST(9.5 AS int) AS int, 
    CAST(9.5 AS decimal(6,4)) AS decimal;
SELECT 9.5 AS Original, CONVERT(int, 9.5) AS int, 
    CONVERT(decimal(6,4), 9.5) AS decimal;
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
|원문 언어   |int    |decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

> [!TIP]
> 많은 [예제](#BKMK_examples) 이 항목의 아래쪽에 있습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
-- Syntax for CAST:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- Syntax for CONVERT:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>인수  
*expression*  
유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다.
  
*data_type*  
대상 데이터 형식입니다. 여기에 **xml**, **bigint**, 및 **sql_variant**합니다. 별칭 데이터 형식은 사용할 수 없습니다.
  
*length*  
대상 데이터 형식의 길이를 지정하는 선택적 정수입니다. 기본값은 30입니다.
  
*style*  
CONVERT 함수를 변환 하는 방법을 지정 하는 정수 식 *식*합니다. style이 NULL이면 NULL이 반환됩니다. 범위 따라 사용자가 *data_type*합니다. 
  
## <a name="return-types"></a>반환 형식
반환 *식* 변환할 *data_type*합니다.

## <a name="date-and-time-styles"></a>날짜 및 시간 스타일  
때 *식* 날짜 또는 시간 데이터 형식, *스타일* 다음 표에 표시 된 값 중 하나일 수 있습니다. 다른 값은 0으로 처리됩니다. 부터는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 변환할 때 지원 되는 유일한 스타일 날짜 및 시간에 형식을 **datetimeoffset** 은 0 또는 1입니다. 다른 모든 변환 스타일은 오류 9809를 반환합니다.
  
>  [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 쿠웨이트 알고리즘을 사용하여 아랍어 스타일의 날짜 형식을 지원합니다.
  
|두 자리 연도 (yy) (<sup>1</sup>)|네 자리 연도(yyyy)|Standard|입/출력 (<sup>3</sup>)|  
|---|---|--|---|
|-|**0** 또는 **100** (<sup>1,</sup><sup>2</sup>)|datetime 및 smalldatetime의 기본값|mon dd yyyy hh:miAM(또는 PM)|  
|**1**|**101**|미국|1 = mm/dd/yy<br /> 101 = mm/dd/yyyy|  
|**2**|**102**|ANSI|2 = yy.mm.dd<br /> 102 = yyyy.mm.dd|  
|**3**|**103**|영국/프랑스|3 = dd/mm/yy<br /> 103 = dd/mm/yyyy|  
|**4**|**104**|독일어|4 = dd.mm.yy<br /> 104 = dd.mm.yyyy|  
|**5**|**105**|이탈리아어|5 = dd-mm-yy<br /> 105 = dd-mm-yyyy|  
|**6**|**106** <sup>(1)</sup>|-|6 = dd mon yy<br /> 106 = dd mon yyyy|  
|**7**|**107** <sup>(1)</sup>|-|7 = Mon dd, yy<br /> 107 = Mon dd, yyyy|  
|**8**|**108**|-|hh:mi:ss|  
|-|**9** 또는 **109** (<sup>1,</sup><sup>2</sup>)|기본값 + 밀리초|mon dd yyyy hh:mi:ss:mmmAM(또는 PM)|  
|**10**|**110**|USA|10 = mm-dd-yy<br /> 110 = mm-dd-yyyy|  
|**11**|**111**|일본|11 = yy/mm/dd<br /> 111 = yyyy/mm/dd|  
|**12**|**112**|ISO|12 = yymmdd<br /> 112 = yyyymmdd|  
|-|**13** 또는 **113** (<sup>1,</sup><sup>2</sup>)|유럽 기본값 + 밀리초|dd mon yyyy hh:mi:ss:mmm(24h)|  
|**14**|**114**|-|hh:mi:ss:mmm(24h)|  
|-|**20** 또는 **120** (<sup>2</sup>)|ODBC 표준|yyyy-mm-dd hh:mi:ss(24h)|  
|-|**21** 또는 **121** (<sup>2</sup>)|time, date, datetime2 및 datetimeoffset의 ODBC 표준(밀리초 포함) 기본값|yyyy-mm-dd hh:mi:ss.mmm(24h)|  
|-|**126** (<sup>4</sup>)|ISO8601|yyyy-mm-ddThh:mi:ss.mmm(공백 없이)<br /> 참고: (mmm) 시간 (밀리초)에 대 한 값이 0 이면 밀리초 값 표시 되지 않습니다. 예를 들어, 값 '2012-11-07T18:26:20.000은 '2012-11-07T18:26:20'으로 표시됩니다.|  
|-|**127**(<sup>6, 7</sup>)|ISO8601(Z 표준 시간대)|yyyy-mm-ddThh:mi:ss.mmmZ (공백 없이)<br /> 참고: (mmm) 시간 (밀리초)에 대 한 값이 0 이면 밀리초 값 표시 되지 않습니다. 예를 들어, 값 '2012-11-07T18:26:20.000은 '2012-11-07T18:26:20'으로 표시됩니다.|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|회교식 (<sup>5</sup>)|dd mon yyyy hh:mi:ss:mmmAM<br /> 이 스타일에서 mon은 전체 월 이름에 대한 다중 토큰 회교식 유니코드 표현을 나타냅니다. 이 값 않습니다에서 올바르게 렌더링 되지 기본 미국 SSMS 설치 합니다.|  
|-|**131** (<sup>2</sup>)|회교식 (<sup>5</sup>)|dd/mm/yyyy hh:mi:ss:mmmAM|  
  
<sup>1</sup> 이러한 스타일 값 비결 정적 결과 반환 합니다. 모든 (yy)(두 자리 연도) 스타일과 (yyyy)(네 자리 연도) 스타일의 하위 집합을 포함합니다.
  
<sup>2</sup> 기본값 (*스타일** *0** 또는 **100**, **9** 또는 **109**, **13** 또는 **113**, **20** 또는 **120**, 및 **21** 또는 **121**) 항상 네 자리 연도 (yyyy)를 반환 합니다.
  
<sup>3</sup> 변환할 때 입력 **datetime**; 출력를 문자 데이터로 변환 하는 경우.
  
<sup>4</sup> XML 사용 하도록 설계 되었습니다. 변환에 대 한 **datetime** 또는 **smalldatetime** 를 문자 데이터로 위의 표에 설명 된 대로 출력 형식은입니다.
  
<sup>5</sup> 회교식 달력 시스템에는 여러 가지 형태가 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 쿠웨이트 알고리즘을 사용합니다.
  
> [!IMPORTANT]  
>  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 구분 연도 2049년을 기준으로 두 자리 연도를 해석합니다. 즉 두 자리 연도 49는 2049년을 의미하고 두 자리 연도 50은 1950년을 의미합니다. Automation 개체를 기반으로 하는 응용 프로그램 등 많은 클라이언트 응용 프로그램에서는 2030년을 구분 연도로 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]사용 하는 구분 연도 변경 하는 두 자리 연도 구분 구성 옵션을 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜를 일관성 있게 처리할 수 있습니다. 네 자리 연도를 지정하는 것이 더 편리합니다.  
  
<sup>6</sup> 에서 문자 데이터를 캐스팅 하는 경우에 지원 **datetime** 또는 **smalldatetime**합니다. 만 나타내는 문자 데이터를 날짜 또는 시간 구성 요소만 때로 캐스팅 되는 **datetime** 또는 **smalldatetime** 데이터 형식 지정 되지 않은 시간 구성 요소가로 설정 되어 00:00:00.000, 있고는 지정 되지 않은 날짜 구성 요소는 1900-01-01로 설정 됩니다.
  
<sup>7</sup>선택적 표준 시간대 표시기 Z, 하는 데 XML을 매핑할 쉽게 **datetime** 시간대 정보가 있는 값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 시간대가 없는 밑줄이 있는 값 . Z는 표준 시간대 UTC-0에 대한 표시기입니다. 다른 표준 시간대는 + 또는 - 방향의 HH:MM 오프셋으로 나타냅니다. 예를 들면 `2006-12-12T23:45:12-08:00`과 같습니다.
  
문자 데이터로 변환 하는 경우 **smalldatetime**, 초 나 밀리초가 포함 된 스타일이 해당이 위치에 0을 표시 합니다. 변환 하면 원치 않는 날짜 부분을 잘라낼 수 **datetime** 또는 **smalldatetime** 적절 한 사용 하 여 값 **char** 또는 **varchar** 데이터 길이 입력 합니다.
  
변환할 때 **datetimeoffset** 에서 한 번 포함 하는 스타일을 사용 하 여 문자 데이터, 표준 시간대 오프셋은 결과에 추가 합니다.
  
## <a name="float-and-real-styles"></a>float 및 real 스타일
때 *식* 은 **float** 또는 **실제**, *스타일* 다음 표에 표시 된 값 중 하나일 수 있습니다. 다른 값은 0으로 처리됩니다.
  
|Value|출력|  
|---|---|
|**0** (기본값)|최대 6자리 수입니다. 해당되는 경우 과학 표기법을 사용하세요.|  
|**1**|항상 8 자리 수입니다. 항상 과학 표기법을 사용하세요.|  
|**2**|항상 16자리 수입니다. 항상 과학 표기법을 사용하세요.|  
|**3**|항상 17 자리 수입니다. 무손실 변환에 사용 됩니다. 이 스타일으로 모든 고유 float 또는 real 값을 고유한 문자 문자열로 변환 하도록 보장 됩니다.<br /> **적용 대상:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 시작 하 고 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다.|  
|**126, 128, 129**|이전 버전과의 호환성을 위해 제공되며 이후 릴리스에서는 더 이상 사용되지 않을 수 있습니다.|  
  
## <a name="money-and-smallmoney-styles"></a>money 및 smallmoney 스타일
때 *식* 은 **money** 또는 **smallmoney**, *스타일* 다음 표에 표시 된 값 중 하나일 수 있습니다. 다른 값은 0으로 처리됩니다.
  
|Value|출력|  
|---|---|
|**0** (기본값)|소수점 앞 세 자리마다 쉼표를 사용하지 않으며 소수점 이하 두 자리인 수입니다(예: 4235.98).|  
|**1**|소수점 앞 세 자리마다 쉼표가 있으며 소수점 이하 두 자리인 수입니다(예: 3,510.92).|  
|**2**|소수점 앞 세 자리마다 쉼표를 사용하지 않으며 소수점 이하 네 자리인 수입니다(예: 4235.9819).|  
|**126**|char(n) 또는 varchar(n)으로 변환하는 경우 스타일 2와 같습니다.|  
  
## <a name="xml-styles"></a>xml 스타일
때 *식* 은 **xml * * *, 스타일* 다음 표에 표시 된 값 중 하나일 수 있습니다. 다른 값은 0으로 처리됩니다.
  
|Value|출력|  
|---|---|
|**0** (기본값)|불필요한 공백을 삭제하고 내부 DTD 하위 집합을 허용하지 않는 기본 구문 분석 동작을 사용합니다.<br /> **참고:** 변환할 때는 **xml** 데이터 형식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 무효 공백을 다르게 처리 보다 XML 1.0에 있습니다. 자세한 내용은 참조 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)합니다.|  
|**1**|불필요한 공백을 유지합니다. 이 스타일 설정 기본 **xml: space** 동일 하 게 작동 하기 위한 처리 처럼 **xml: space = "preserve"** 가 대신 지정 된 합니다.|  
|**2**|제한된 내부 DTD 하위 집합 처리를 설정합니다.<br /><br /> 설정된 경우 서버가 내부 DTD 하위 집합에 제공된 다음 정보를 사용하여 유효성을 검사하지 않는 구문 분석 작업을 수행합니다.<br /> -특성에 대 한 기본값이 적용 됩니다.<br /> -내부 엔터티 참조가 해결 되 고 확장 합니다.<br /> -DTD 콘텐츠 모델은 구문이 올바른지 확인 합니다.<br /> 파서가 외부 DTD 하위 집합을 무시합니다. 또한 참조 위해 XML 선언을 평가 하지 않습니다 여부는 **독립 실행형** 특성이 설정 되어 **예** 또는 **없습니다**, 대신 독립 실행형 말 이죠 XML 인스턴스를 구문 분석 되지만 문서입니다.|  
|**3**|불필요한 공백을 유지하고 제한된 내부 DTD 하위 집합 처리를 설정합니다.|  
  
## <a name="binary-styles"></a>이진 스타일
때 *식* 은 **binary (n)**, **varbinary (n)**, **char (n)**, 또는 **varchar (n)**, *스타일* 다음 표에 표시 된 값 중 하나일 수 있습니다. 여기에 없는 스타일 값은 오류를 반환합니다.
  
|Value|출력|  
|---|---|
|**0** (기본값)|ASCII 문자를 이진 바이트로 또는 이진 바이트를 ASCII 문자로 변환합니다. 각 문자 또는 바이트는 1:1로 변환됩니다.<br /> 경우는 *data_type* 이진 형식이 문자 0x는 결과의 왼쪽에 추가 됩니다.|  
|**1**, **2**|경우는 *data_type* 이 binary 형식이 식에는 문자 식 이어야 합니다. *식* 짝수 개의 16 진수 숫자의 수로 구성 해야 (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, a, b, c, d, e, f). 경우는 *스타일* 1로 설정 되는 문자 0 x 이어야 합니다 처음 두 문자 식에 있습니다. 식에 홀수 개의 문자나 유효하지 않은 문자가 포함되어 있으면 오류가 발생합니다.<br /> 변환된 된 식의 길이가의 길이 보다 큰 경우는 *data_type* 결과 오른쪽이 잘렸습니다.<br /> 고정 길이 *data_types* 변환된 된 결과 결과의 오른쪽에 0이 추가 보다 크거나 합니다.<br /> data_type이 문자 유형이면 식이 이진 식이어야 합니다. 각 이진 문자는 두 개의 16진수 문자로 변환됩니다. 변환된 된 식의 길이 보다 크면는 *data_type* 길이, 오른쪽 잘릴 수 있습니다.<br /> 경우는 *data_type* 은 고정 크기 문자 유형이 고 변환된 된 결과의 길이가의 길이 보다 작으면는 *data_type*; 한도 유지 하기 위해 변환된 된 식의 오른쪽에 공백이 추가 되어 16 진수의 수입니다.<br /> 0 x에 대 한 변환된 된 결과의 왼쪽에 추가할 문자 *스타일* 1입니다.|  
  
## <a name="implicit-conversions"></a>암시적 변환
암시적 변환은 CAST 또는 CONVERT 함수를 지정하지 않은 상태에서 발생하는 변환이고 명시적 변환은 CAST 또는 CONVERT 함수를 지정해야 발생하는 변환입니다. 다음 그림에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 제공 데이터 형식에 허용된 모든 명시적 및 암시적 데이터 형식 변환을 보여 줍니다. 여기에 **xml**, **bigint**, 및 **sql_variant**합니다. 할당에 암시적 변환이 이루어지지는 **sql_variant** 데이터 형식으로 암시적 변환이 있지만 **sql_variant**합니다.
  
> [!TIP]  
>  이 차트는의 다운로드 가능한 PDF 파일로 사용할 수는 [Microsoft 다운로드 센터](http://www.microsoft.com/download/details.aspx?id=35834)합니다.  
  
![데이터 형식 변환 표](../../t-sql/data-types/media/lrdatahd.png "데이터 형식 변환 표")
  
간에 변환 하는 경우 **datetimeoffset** 및 문자 형식 **char**, **varchar**, **nchar**, 및 **nvarchar**  변환 된 표준 시간대 오프셋된 부분의 HH 및 MM-08 예를 들어, 두 자리는 항상: 00입니다.
  
> [!NOTE]  
>  유니코드 데이터는 항상 짝수 바이트의 수를 사용 하므로 주의 변환할 때 **이진** 또는 **varbinary** 유니코드 데이터 형식을 지원 합니다. 예를 들어 `SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)` 변환은 16진수 값 41이 아니라 4100을 반환합니다.  
  
## <a name="large-value-data-types"></a>큰 값 데이터 형식
큰 값 데이터 형식 발생 보다 작은 같은 암시적 및 명시적 변환 동작 구체적으로 **varchar**, **nvarchar** 및 **varbinary**데이터 형식입니다. 그러나 다음 지침을 고려해야 합니다.
-   변환 **이미지** 를 **varbinary (max)** 그 반대로 변환 하는 암시적 변환이 되 고 간의 변환 **텍스트** 및 **varchar (max)**, 및 **ntext** 및 **nvarchar (max)**합니다.  
-   와 같은 큰 값 데이터에서 변환 형식을 **varchar (max)**을 같은 더 작은 정수 데이터 형식 **varchar**, 암시적 변환이 있지만 큰 값에 대 한 너무 큰 경우에 잘림이 지정 된 길이 보다 작은 데이터 형식입니다.  
-   변환 **varchar**, **nvarchar**, 또는 **varbinary** 해당의 큰 값 데이터 형식을 암시적으로 수행 합니다.  
-   변환 된 **sql_variant** 큰 값 데이터 형식에 데이터 형식이 명시적 변환 합니다.  
-   큰 값 데이터 형식을 변환할 수 없습니다는 **sql_variant** 데이터 형식입니다.  
  
변환 하는 방법에 대 한 자세한 내용은 **xml** 참조 데이터 형식, [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)합니다.
  
## <a name="xml-data-type"></a>XML 데이터 형식입니다.
명시적 또는 암시적으로 캐스팅할 때는 **xml** 데이터 형식을 문자열 또는 바이너리 데이터 형식으로의 콘텐츠는 **xml** 데이터 형식이 규칙의 집합에 따라 직렬화 됩니다. 이러한 규칙에 대 한 정보를 참조 하십시오. [XML 데이터 직렬화 정의](../../relational-databases/xml/define-the-serialization-of-xml-data.md)합니다. 다른 데이터 형식으로 변환 하는 방법에 대 한 내용은 **xml** 참조 데이터 형식, [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)합니다.
  
## <a name="text-and-image-data-types"></a>text 및 image 데이터 형식
에 대 한 자동 데이터 형식 변환은 지원 되지 않습니다는 **텍스트** 및 **이미지** 데이터 형식입니다. 명시적으로 변환할 수 **텍스트** 데이터를 문자 데이터로 및 **이미지** 데이터를 **이진** 또는 **varbinary**, 최대 길이 8000 하지만 바이트 수입니다. 문자를 포함 하는 문자 식으로 변환 하는 등 잘못 된 변환을 시도 하면는 **int**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지를 반환 합니다.
  
## <a name="output-collation"></a>출력 데이터 정렬  
CAST 또는 CONVERT의 출력이 문자열이고 입력도 문자열이면 출력과 입력은 동일한 데이터 정렬 및 데이터 정렬 레이블을 가집니다. 입력이 문자열이 아닌 경우에는 출력에서 데이터베이스의 기본 데이터 정렬을 사용하며 강제할 수 있는 기본값의 데이터 정렬 레이블을 사용합니다. 자세한 내용은 참조 [데이터 정렬 선행 규칙 &#40; Transact SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).
  
출력에 다른 데이터 정렬을 할당하려면 CAST 또는 CONVERT 함수의 결과 식에 COLLATE 절을 적용합니다. 예를 들어
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>결과 잘라내기 및 반올림
변환 하는 경우 문자 또는 이진 식 (**char**, **nchar**, **nvarchar**, **varchar**, **이진**, 또는 **varbinary**)을 다른 데이터 형식의 식으로 데이터를 자르기 일부만 표시 또는 결과 길이가 너무 짧아 표시 하면 오류가 반환 됩니다. 으로 변환은 **char**, **varchar**, **nchar**, **nvarchar**, **이진**, 및  **varbinary** 다음 표에 있는 변환을 제외 하 고 잘립니다.
  
|원래 데이터 형식|변경할 데이터 형식|결과|  
|---|---|---|
|**int**, **smallint**, 또는 **tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**money**, **smallmoney**, **숫자**, **10 진수**, **float**, 또는 **실제**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\*= 결과 길이가 너무 짧아 표시 합니다. E = 결과 길이가 너무 짧아 표시되지 않으므로 오류가 반환됩니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]왕복 변환만 있는 데이터 형식을 원래 데이터 형식에서 변환 변환한 후 다시 변환 생성 버전 간에 같은 값을 보장 합니다. 다음 예에서는 이러한 왕복 변환을 보여 줍니다.
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  생성 하려고 하지 마십시오 **이진** 값을 숫자 데이터 형식 범주의 데이터 형식으로 변환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]결과 되지는지 않습니다는 **10 진수** 또는 **숫자** 데이터 형식 변환에 **이진** 것의 버전 간에 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
다음 예에서는 길이가 짧아 표시할 수 없는 결과 식을 보여 줍니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, SUBSTRING(p.Title, 1, 25) AS Title,
    CAST(e.SickLeaveHours AS char(1)) AS [Sick Leave]  
FROM HumanResources.Employee e JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID  
WHERE NOT e.BusinessEntityID >5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```   
FirstName   LastName      Title   Sick Leave
---------   ------------- ------- --------`
Ken         Sanchez       NULL   *
Terri       Duffy         NULL   *
Roberto     Tamburello    NULL   *
Rob         Walters       NULL   *
Gail        Erickson      Ms.    *
(5 row(s) affected)  
```
  
소수 자릿수가 다른 데이터 형식을 변환할 경우 결과 값이 잘리거나 반올림될 수 있습니다. 다음 표에서는 이러한 동작을 보여 줍니다.
  
|보낸 사람|수행할 작업|동작|  
|---|---|---|
|**numeric**|**numeric**|반올림|  
|**numeric**|**int**|잘라내기|  
|**numeric**|**money**|반올림|  
|**money**|**int**|반올림|  
|**money**|**numeric**|반올림|  
|**float**|**int**|잘라내기|  
|**float**|**numeric**|반올림<br /><br /> 변환 **float** 과학적 표기법을 사용 하는 값 **10 진수** 또는 **숫자** 전체 자릿수가 17 자리로의 값으로 제한 됩니다. 17자리를 넘는 값은 0으로 반올림됩니다.|  
|**float**|**datetime**|반올림|  
|**datetime**|**int**|반올림|  
  
예를 들어 10.6496 및-10.6496 값 잘린 되었거나 변환 하는 동안 반올림 **int** 또는 **숫자** 유형:
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
쿼리의 결과 다음과 같습니다.
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
대상 데이터 형식의 소수 자릿수가 원본 데이터 형식의 소수 자릿수보다 적은 데이터 형식을 변환할 경우 값이 반올림됩니다. 예를 들어 다음 변환의 결과는 `$10.3497`입니다.
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]숫자가 아닌 경우 오류 메시지가 반환 **char**, **nchar**, **varchar**, 또는 **nvarchar** 데이터 변환할 **int** , **float**, **숫자**, 또는 **10 진수**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]빈 문자열이 될 경우 오류도 반환 ("")으로 변환 **숫자** 또는 **10 진수**합니다.
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>일부 datetime 변환은 비결 정적 됩니다.
다음 표에서는 문자열에서 datetime으로의 변환이 비결정적인 스타일을 나열합니다.
  
|||  
|-|-|  
|100 아래의 모든 스타일<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup> 스타일 20 및 21 제외
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자 (서로게이트 쌍)
부터는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SC (보조 문자) 데이터 정렬 캐스트 연산에서 사용 하는 경우, **nchar** 또는 **nvarchar** 에 **nchar** 또는  **nvarchar** 길이가 더 짧은 형식의 서로게이트 쌍 안에서 자르지 않고; 보충 문자 앞에서 자릅니다. 예를 들어 다음 코드 조각에서는 `@x`만 보유한 `'ab'`를 남깁니다. 공간이 부족하여 보조 문자를 포함할 수 없습니다.
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
SC 데이터 정렬을 사용할 경우 `CONVERT`의 동작은 `CAST`의 동작과 유사합니다.
  
## <a name="compatibility-support"></a>호환성 지원
이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CAST 및 CONVERT 작업에 대 한 기본 스타일 **시간** 및 **datetime2** 데이터 형식 유형 중 하나는 계산된 열 식에 사용 되는 경우를 제외 하 고는 121입니다. 계산 열의 경우 기본 스타일은 0입니다. 이 동작은 자동 매개 변수화와 관련된 쿼리에서 이러한 연산이 만들어지고 사용될 때 또는 제약 조건 정의에 사용될 때 계산 열에 영향을 줍니다.
  
호환성 수준 110 이상에서 기본 스타일에 대 한 CAST 및 CONVERT 연산에 **시간** 및 **datetime2** 데이터 형식을 항상 121입니다. 쿼리에 이전 동작이 적용되는 경우 110보다 낮은 호환성 수준을 사용하거나, 해당 쿼리에서 스타일 0을 명시적으로 지정해야 합니다.
  
데이터베이스를 호환성 수준 110 이상으로 업그레이드할 경우 디스크에 저장된 사용자 데이터는 변경되지 않습니다. 수동으로 이 데이터를 적절하게 수정해야 합니다. 예를 들어 SELECT INTO를 사용하여 위에서 설명한 계산 열 식이 포함된 원본에서 테이블을 만든 경우 계산 열 정의 자체가 아니라 스타일 0을 사용하는 데이터가 저장됩니다. 스타일 121과 일치하도록 이 데이터를 수동으로 업데이트해야 합니다.
  
## <a name="BKMK_examples"></a> 예  
  
### <a name="a-using-both-cast-and-convert"></a>1. CAST 및 CONVERT 모두 사용  
각 예에서는 제품 가격 첫 자리에 `3`이 있는 제품의 이름을 검색하고 `ListPrice`를 `int`로 변환합니다.
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '3%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
GO  
```  
  
### <a name="b-using-cast-with-arithmetic-operators"></a>2. CAST에 산술 연산자 사용  
다음 예에서는 총 연간 매출(`Computed`)을 커미션 비율(`SalesYTD`)로 나누어 한 열을 계산(`CommissionPCT`)합니다. 이 결과는 가장 근사한 정수로 반올림된 후 `int` 데이터 형식으로 변환됩니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT CAST(ROUND(SalesYTD/CommissionPCT, 0) AS int) AS Computed  
FROM Sales.SalesPerson   
WHERE CommissionPCT != 0;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```  
Computed
------
379753754
346698349
257144242
176493899
281101272
0  
301872549
212623750
298948202
250784119
239246890
101664220
124511336
97688107
(14 row(s) affected)  
```  
  
### <a name="c-using-cast-to-concatenate"></a>3. CAST를 사용하여 연결  
다음 예에서는 캐스팅을 사용 하 여 문자가 아닌 식을 연결 합니다. AdventureWorksDW를 사용합니다.
  
```sql
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM dbo.DimProduct  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09  
```  
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>4. CAST를 사용하여 읽기 쉬운 텍스트 만들기  
다음 예제에서는 SELECT 목록에서 변환 하려면 CAST가 사용 된 `Name` 열을 한 **char (10)** 열. AdventureWorksDW를 사용합니다.
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        UnitPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="e-using-cast-with-the-like-clause"></a>5. CAST에 LIKE 절 사용  
다음 예에서는 `money` 절과 함께 사용할 수 있도록 `SalesYTD` 열인 `int`를 `char(20)`로 변환한 다음 `LIKE` 열로 변환합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, s.SalesYTD, s.BusinessEntityID  
FROM Person.Person AS p   
JOIN Sales.SalesPerson AS s   
    ON p.BusinessEntityID = s.BusinessEntityID  
WHERE CAST(CAST(s.SalesYTD AS int) AS char(20)) LIKE '2%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
FirstName        LastName            SalesYTD         SalesPersonID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>6. 형식화된 XML과 함께 CONVERT 또는 CAST 사용  
사용 하 여 형식화 된 XML로 변환 하기 위해 CONVERT를 사용 하 여 보여 주는 몇 가지 예는 다음과 같은 [XML 데이터 형식 및 열 &#40; SQL Server &#41; ](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md).
  
다음 예에서는 공백, 텍스트 및 태그가 있는 문자열을 형식화된 XML로 변환하고 불필요한 공백(노드 사이의 경계 공백)을 모두 제거합니다.
  
```sql
CONVERT(XML, '<root><child/></root>')  
```  
  
다음 예에서는 공백, 텍스트 및 태그가 있는 비슷한 문자열을 형식화된 XML로 변환하고 불필요한 공백(노드 사이의 경계 공백)을 유지합니다.
  
```sql
CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
다음 예에서는 공백, 텍스트 및 태그가 있는 문자열을 형식화된 XML로 캐스팅합니다.
  
```sql
CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
더 많은 예제를 참조 하십시오. [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)합니다.
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>7. datetime 데이터와 함께 CAST 및 CONVERT 사용  
다음 예에서는 현재 날짜와 시간을 표시합니다. 즉, `CAST`를 사용하여 현재 날짜와 시간을 문자 데이터 형식으로 변경한 다음 `CONVERT`를 사용하여 `ISO 8901` 형식으로 날짜와 시간을 표시합니다.
  
```sql
SELECT   
   GETDATE() AS UnconvertedDateTime,  
   CAST(GETDATE() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), GETDATE(), 126) AS UsingConvertTo_ISO8601  ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast              UsingConvertTo_ISO8601
----------------------- ---------------------- ------------------------------
2006-04-18 09:58:04.570 Apr 18 2006  9:58AM    2006-04-18T09:58:04.570
(1 row(s) affected)  
```
  
다음 예에서는 이전 예와 반대로 수행합니다. 다음 예에서는 날짜와 시간을 문자 데이터로 표시합니다. 즉, `CAST`를 사용하여 문자 데이터를 `datetime` 데이터 형식으로 변경한 다음 `CONVERT`를 사용하여 문자 데이터를 `datetime` 데이터 형식으로 변경합니다.
  
```sql
SELECT   
   '2006-04-25T15:50:59.997' AS UnconvertedText,  
   CAST('2006-04-25T15:50:59.997' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2006-04-25T15:50:59.997', 126) AS UsingConvertFrom_ISO8601 ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2006-04-25T15:50:59.997 2006-04-25 15:50:59.997 2006-04-25 15:50:59.997
(1 row(s) affected)  
```
  
### <a name="h-using-convert-with-binary-and-character-data"></a>8. CONVERT에 이진 및 문자 데이터 사용  
다음 예에서는 다양한 스타일을 사용하여 이진 및 문자 데이터를 변환한 결과를 보여 줍니다.
  
```sql
--Convert the binary value 0x4E616d65 to a character value.  
SELECT CONVERT(char(8), 0x4E616d65, 0) AS [Style 0, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, binary to character
----------------------------
Name  
(1 row(s) affected)  
```
 
다음 예에서는 스타일 1 잘릴 결과 강제로 수행할 수는 방법을 보여 줍니다. 잘림을 원인은 공백으로 0 x 결과에서입니다.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 1) AS [Style 1, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, binary to character
------------------------------
0x4E616D
(1 row(s) affected)  
```  
 
다음 예에서는 스타일 2 때문에 결과 truncate 하지 않는 문자 0 x 결과에 포함 되지 않습니다.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 2) AS [Style 2, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, binary to character
------------------------------
4E616D65
(1 row(s) affected)  
```
  
'Name' 문자 값을 이진 값으로 변환 합니다.  
```sql
SELECT CONVERT(binary(8), 'Name', 0) AS [Style 0, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, character to binary
----------------------------
0x4E616D6500000000
(1 row(s) affected)  
```
  
```sql
SELECT CONVERT(binary(4), '0x4E616D65', 1) AS [Style 1, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, character to binary
---------------------------- 
0x4E616D65
(1 row(s) affected)  
```  

```sql
SELECT CONVERT(binary(4), '4E616D65', 2) AS [Style 2, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, character to binary  
----------------------------------  
0x4E616D65
(1 row(s) affected)  
```  
  
### <a name="i-converting-date-and-time-data-types"></a>9. 날짜 및 시간 데이터 형식 변환  
다음 예제는 date, time 및 datetime 데이터 형식의 변환을 보여 줍니다.
  
```sql
DECLARE @d1 date, @t1 time, @dt1 datetime;  
SET @d1 = GETDATE();  
SET @t1 = GETDATE();  
SET @dt1 = GETDATE();  
SET @d1 = GETDATE();  
-- When converting date to datetime the minutes portion becomes zero.  
SELECT @d1 AS [date], CAST (@d1 AS datetime) AS [date as datetime];  
-- When converting time to datetime the date portion becomes zero   
-- which converts to January 1, 1900.  
SELECT @t1 AS [time], CAST (@t1 AS datetime) AS [time as datetime];  
-- When converting datetime to date or time non-applicable portion is dropped.  
SELECT @dt1 AS [datetime], CAST (@dt1 AS date) AS [datetime as date], 
   CAST (@dt1 AS time) AS [datetime as time];  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>10. CAST 및 CONVERT를 사용 하 여  
이러한 제품에 대해 제품의 이름을 검색 하는이 예제는 `3` 정가 변환의 첫 자리에 해당 `ListPrice` 를 **int**합니다. AdventureWorksDW를 사용합니다.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
이 예제에는 CAST 대신 CONVERT를 사용 하 여 동일한 쿼리를 보여 줍니다. AdventureWorksDW를 사용합니다.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>11. CAST에 산술 연산자 사용  
다음 예제에서는 제품 단가 분할 하 여 단일 열 계산을 계산 (`UnitPrice`)는 할인 백분율 (`UnitPriceDiscountPct`). 이 결과는 가장 근사한 정수로 반올림된 후 `int` 데이터 형식으로 변환됩니다. AdventureWorksDW를 사용합니다.
  
```sql
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,  
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice  
FROM dbo.FactResellerSales  
WHERE SalesOrderNumber = 'SO47355'   
      AND UnitPriceDiscountPct > .02;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1  
```  
  
### <a name="l-using-cast-with-the-like-clause"></a>12. CAST에 LIKE 절 사용  
다음 예제는 **money** 열 `ListPrice` 에 **int** 형식 다음는 **char(20)** LIKE 절과 함께 사용할 수 있도록 입력 합니다. AdventureWorksDW를 사용합니다.
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="m-using-cast-and-convert-with-datetime-data"></a>13. datetime 데이터와 함께 CAST 및 CONVERT 사용  
다음 예제에서는 표시에서 현재 날짜 및 시간을 사용 하 여 문자 데이터 형식으로 현재 날짜 및 시간을 변경 하려면 CAST 및 CONVERT를 사용 하 여 ISO 8601 형식에 날짜와 시간을 표시 합니다. AdventureWorksDW를 사용합니다.
  
```sql
SELECT TOP(1)  
   SYSDATETIME() AS UnconvertedDateTime,  
   CAST(SYSDATETIME() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), SYSDATETIME(), 126) AS UsingConvertTo_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast                     UsingConvertTo_ISO8601  
---------------------   ---------------------------   ---------------------------  
07/20/2010 1:44:31 PM   2010-07-20 13:44:31.5879025   2010-07-20T13:44:31.5879025  
```  
  
다음 예에서는 이전 예와 반대로 수행합니다. 이 예제에서는 문자 데이터로 표시 되는 날짜와 시간을 표시, 캐스트를 사용 하 여 문자 데이터를 변경는 **datetime** 데이터 형식 및 사용 하 여 문자 데이터를 변경 하려면 CONVERT는 **datetime** 데이터 형식입니다. AdventureWorksDW를 사용합니다.
  
```sql
SELECT TOP(1)   
   '2010-07-25T13:50:38.544' AS UnconvertedText,  
CAST('2010-07-25T13:50:38.544' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2010-07-25T13:50:38.544', 126) AS UsingConvertFrom_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2010-07-25T13:50:38.544 07/25/2010 1:50:38 PM   07/25/2010 1:50:38 PM  
```  
  
## <a name="see-also"></a>참고 항목
 [데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
 [형식 &#40; Transact SQL &#41;](../../t-sql/functions/format-transact-sql.md)  
 [STR &#40; Transact SQL &#41;](../../t-sql/functions/str-transact-sql.md)  
 [SELECT &#40;TRANSACT-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
 [시스템 함수 &#40; Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
 [국가별 Transact-SQL 문 작성](../../relational-databases/collations/write-international-transact-sql-statements.md)
  
