---
title: CAST 및 CONVERT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs:
- TSQL
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f8eecd6d0a1d54d56fd93eacf96154f57e4afec6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79286947"
---
# <a name="cast-and-convert-transact-sql"></a>CAST 및 CONVERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이러한 함수는 한 데이터 형식의 식을 다른 데이터 형식의 식으로 변환합니다.  

## <a name="syntax"></a>구문  
  
```
-- CAST Syntax:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- CONVERT Syntax:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="arguments"></a>인수  
*expression*  
유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.
  
*data_type*  
대상 데이터 형식입니다. 여기에는 **xml**, **bigint** 및 **sql_variant**가 있습니다. 별칭 데이터 형식은 사용할 수 없습니다.
  
*length*  
사용자가 지정한 길이를 허용하는 데이터 형식에 대해 대상 데이터 형식의 길이를 지정하는 선택적 정수입니다. 기본값은 30입니다.
  
*style*  
CONVERT 함수가 *식*을 변환하는 방법을 지정하는 정수 식입니다. NULL 스타일 값은 NULL을 반환합니다. *data_type*은 범위를 결정합니다. 
  
## <a name="return-types"></a>반환 형식
*data_type*으로 변환된 *식*을 반환합니다.
  
## <a name="date-and-time-styles"></a>날짜 및 시간 스타일  
날짜 또는 시간 데이터 형식 *식*인 경우 *스타일*은 다음 표에 있는 값 중 하나일 수 있습니다. 다른 값은 0으로 처리됩니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 날짜 및 시간 형식에서 **datetimeoffset**으로 변환할 때 지원되는 유일한 스타일은 0 또는 1입니다. 다른 모든 변환 스타일은 오류 9809를 반환합니다.
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 쿠웨이트 알고리즘을 통해 아랍어 스타일의 날짜 형식을 지원합니다.
  
|두 자리 연도(yy) (<sup>1</sup>)|네 자리 연도(yyyy)|Standard|입/출력(<sup>3</sup>)|  
|---|---|--|---|
|-|**0** 또는 **100** (<sup>1,</sup><sup>2</sup>)|datetime 및 smalldatetime의 기본값|mon dd yyyy hh:miAM(또는 PM)|  
|**1**|**101**|미국|  1 = mm/dd/yy<br /> 101 = mm/dd/yyyy|  
|**2**|**102**|ANSI|  2 = yy.mm.dd<br /> 102 = yyyy.mm.dd|  
|**3**|**103**|영국/프랑스|  3 = dd/mm/yy<br /> 103 = dd/mm/yyyy|  
|**4**|**104**|독일어|  4 = dd.mm.yy<br /> 104 = dd.mm.yyyy|  
|**5**|**105**|이탈리아어|  5 = dd-mm-yy<br /> 105 = dd-mm-yyyy|  
|**6**|**106** <sup>(1)</sup>|-|  6 = dd mon yy<br /> 106 = dd mon yyyy|  
|**7**|**107** <sup>(1)</sup>|-|  7 = Mon dd, yy<br /> 107 = Mon dd, yyyy|  
|**8** 또는 **24**|**108**|-|hh:mi:ss|  
|-|**9** 또는 **109** (<sup>1,</sup><sup>2</sup>)|기본값 + 밀리초|mon dd yyyy hh:mi:ss:mmmAM(또는 PM)|  
|**10**|**110**|USA| 10 = mm-dd-yy<br /> 110 = mm-dd-yyyy|  
|**11**|**111**|일본| 11 = yy/mm/dd<br /> 111 = yyyy/mm/dd|  
|**12**|**112**|ISO| 12 = yymmdd<br /> 112 = yyyymmdd|  
|-|**13** 또는 **113** (<sup>1,</sup><sup>2</sup>)|유럽 기본값 + 밀리초|dd mon yyyy hh:mi:ss:mmm(24h)|  
|**14**|**114**|-|hh:mi:ss:mmm (24h)|  
|-|**20** 또는 **120** (<sup>2</sup>)|ODBC 표준|yyyy-mm-dd hh:mi:ss (24h)|  
|-|**21** 또는 **25** 또는 **121** (<sup>2</sup>)|time, date, datetime2 및 datetimeoffset의 ODBC 표준(밀리초 포함) 기본값|yyyy-mm-dd hh:mi:ss.mmm (24h)|  
|**22**|-|미국| mm/dd/yy hh:mi:ss AM (또는 PM)|
|-|**23**|ISO8601|yyyy-mm-dd|
|-|**126** (<sup>4</sup>)|ISO8601|yyyy-mm-ddThh:mi:ss.mmm(공백 없이)<br /><br /> **참고:** 밀리초(mmm) 값 0의 경우 밀리초 소수 부분 값이 표시되지 않습니다. 예를 들어 '2012-11-07T18:26:20.000' 값은 '2012-11-07T18:26:20'으로 표시됩니다.| 
|-|**127**(<sup>6, 7</sup>)|ISO8601(Z 표준 시간대)|yyyy-mm-ddThh:mi:ss.mmmZ (공백 없이)<br /><br /> **참고:** 밀리초(mmm) 값 0의 경우 밀리초 소수 값이 표시되지 않습니다. 예를 들어, '2012-11-07T18:26:20.000' 값은 '2012-11-07T18:26:20'으로 표시됩니다.|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|회교식(<sup>5</sup>)|dd mon yyyy hh:mi:ss:mmmAM<br /><br /> 이 스타일에서 **mon**은 전체 월 이름에 대한 다중 토큰 회교식 유니코드 표현을 나타냅니다. 이 값은 SSMS의 기본 미국 영어 설치에서 올바르게 렌더링되지 않습니다.|  
|-|**131** (<sup>2</sup>)|회교식(<sup>5</sup>)|dd/mm/yyyy hh:mi:ss:mmmAM|  
  
<sup>1</sup> 이러한 스타일 값은 비결정적 결과를 반환합니다. 모든 (yy)(두 자리 연도) 스타일과 (yyyy)(네 자리 연도) 스타일의 하위 집합을 포함합니다.
  
<sup>2</sup> 기본값(**0** 또는 **100**, **9** 또는 **109**, **13** 또는 **113**, **20** 또는 **120**, **23**, 및 **21** 또는 **25** 또는 **121**)은 항상 네 자리 연도(yyyy)를 반환합니다.

<sup>3</sup>**datetime**으로 변환할 때의 입력이며 문자 데이터로 변환할 때의 출력입니다.

<sup>4</sup> XML용으로 고안되었습니다. **datetime** 또는 **smalldatetime**을 문자 데이터로 변환하는 경우 출력 형식은 앞의 표를 참조하세요.

<sup>5</sup> 회교식 달력 시스템에는 여러 가지 형태가 있는데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 쿠웨이트 알고리즘을 사용합니다.

> [!IMPORTANT]
>  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 구분 연도 2049년을 기준으로 두 자리 연도를 해석합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 두 자릿수 연도 49를 2049로, 50을 1950으로 해석합니다. Automation 개체를 기반으로 하는 애플리케이션 등 많은 클라이언트 애플리케이션에서는 2030년을 구분 연도로 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 구분 연도를 변경하기 위한 두 자리 연도 구분 구성 옵션을 제공합니다. 이를 통해 날짜를 일관성 있게 처리할 수 있습니다. 네 자리 연도를 지정하는 것이 더 편리합니다.

<sup>6</sup> 문자 데이터를 **datetime** 또는 **smalldatetime**으로 캐스팅하는 경우에만 지원됩니다. 날짜 또는 시간 구성 요소만 나타내는 문자 데이터를 **datetime** 또는 **smalldatetime** 데이터 형식으로 캐스팅하면 지정되지 않은 시간 구성 요소는 00:00:00.000으로 설정되고 지정되지 않은 날짜 구성 요소는 1900-01-01로 설정됩니다.
  
<sup>7</sup> 선택적 표준 시간대 표시기 **Z**를 사용하면 표준 시간대 정보가 있는 XML **datetime** 값을 표준 시간대가 없는[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 값에 쉽게 매핑할 수 있습니다. Z는 UTC-0 시간대를 나타냅니다. \+ 또는 - 방향의 HH:MM 오프셋으로 다른 시간대를 나타냅니다. 예: `2006-12-12T23:45:12-08:00`
  
**smalldatetime**을 문자 데이터로 변환할 때는 초나 밀리초가 포함된 스타일이 해당 위치에 0으로 표시됩니다. **datetime** 또는 **smalldatetime** 값을 변환할 때는 적합한 **char** 또는 **varchar** 데이터 형식 길이를 사용하여 불필요한 날짜 부분을 자를 수 있습니다.
  
시간이 포함된 스타일을 사용하여 문자 데이터에서 **datetimeoffset**으로 변환할 때는 결과에 표준 시간대 오프셋이 추가됩니다.
  
## <a name="float-and-real-styles"></a>float 및 real 스타일
**float** 또는 **real** ‘식’인 경우 ‘스타일’은 다음 테이블에 있는 값 중 하나일 수 있습니다.   다른 값은 0으로 처리됩니다.
  
|값|출력|  
|---|---|
|**0** (기본값)|최대 6자리 수입니다. 해당되는 경우 과학 표기법을 사용하세요.|  
|**1**|항상 8자리 수입니다. 항상 과학 표기법을 사용하세요.|  
|**2**|항상 16자리 수입니다. 항상 과학 표기법을 사용하세요.|  
|**3**|항상 17자리 수입니다. 무손실 변환용입니다. 이 스타일에서는 모든 고유 부동 또는 실수 값이 고유 문자열로 변환됩니다.<br /><br /> **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**126, 128, 129**|이전 버전과의 호환성을 위해 제공되며 이후 릴리스에서는 이 값을 더 이상 사용하지 않을 수 있습니다.|  
  
## <a name="money-and-smallmoney-styles"></a>money 및 smallmoney 스타일
**money** 또는 **smallmoney** ‘식’인 경우 ‘스타일’은 다음 테이블에 있는 값 중 하나일 수 있습니다.   다른 값은 0으로 처리됩니다.
  
|값|출력|  
|---|---|
|**0** (기본값)|소수점 앞 세 자리마다 쉼표를 사용하지 않으며 소수점 이하 두 자리인 수입니다.<br /><br />예제: 4235.98.|  
|**1**|소수점 앞 세 자리마다 쉼표를 사용하며 소수점 이하 두 자리인 수입니다.<br /><br />예제: 3,510.92.|  
|**2**|소수점 앞 세 자리마다 쉼표를 사용하지 않으며 소수점 이하 4자리인 수입니다.<br /><br />예제: 4235.9819.|  
|**126**|char(n) 또는 varchar(n)으로 변환하는 경우 스타일 2와 같습니다.|  
  
## <a name="xml-styles"></a>xml 스타일
**xml**’식’인 경우 ‘스타일’은 다음 테이블에 있는 값 중 하나일 수 있습니다.   다른 값은 0으로 처리됩니다.
  
|값|출력|  
|---|---|
|**0** (기본값)|불필요한 공백을 삭제하고 내부 DTD 하위 집합을 허용하지 않는 기본 구문 분석 동작을 사용합니다.<br /><br />**참고:** **xml** 데이터 형식으로 변환할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 불필요한 공백은 XML 1.0에서와 다르게 처리됩니다. 자세한 내용은 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)를 참조하세요.|  
|**1**|불필요한 공백을 유지합니다. 이 스타일 설정은 기본 **xml: space** 처리를 **xml: space = "preserve"** 동작에 맞게 설정합니다.|  
|**2**|제한된 내부 DTD 하위 집합 처리를 설정합니다.<br /><br /> 설정된 경우 서버가 내부 DTD 하위 집합에 제공된 다음 정보를 사용하여 유효성을 검사하지 않는 구문 분석 작업을 수행합니다.<br /><br />   - 특성의 기본값이 적용됩니다.<br />   - 내부 엔터티 참조가 확인 및 확장됩니다.<br />   - DTD 콘텐츠 모델의 구문이 올바른지 확인합니다.<br /><br /> 구문 분석기가 외부 DTD 하위 집합을 무시합니다. 또한 **standalone** 특성의 값이 **yes** 또는 **no**인지 확인하기 위해 XML 선언을 평가하지 않습니다. 대신, 독자적인 문서로 XML 인스턴스를 구문 분석합니다.|  
|**3**|불필요한 공백을 유지하고 제한된 내부 DTD 하위 집합 처리를 설정합니다.|  
  
## <a name="binary-styles"></a>이진 스타일
**binary(n)** , **char(n)** , **varbinary(n)** 또는 **varchar(n)** ‘식’인 경우 ‘스타일’은 다음 테이블에 있는 값 중 하나일 수 있습니다.   여기에 없는 스타일 값은 오류를 반환합니다.
  
|값|출력|  
|---|---|
|**0** (기본값)|ASCII 문자를 이진 바이트로 또는 이진 바이트를 ASCII 문자로 변환합니다. 각 문자 또는 바이트는 1:1로 변환됩니다.<br /><br /> 이진 *data_type*인 경우 결과의 왼쪽에 문자 0x가 추가됩니다.|  
|**1**, **2**|이진 *data_type*인 경우 식이 문자 식이어야 합니다. *expression*은 **짝수** 개의 16진수(0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, a, b, c, d, e, f)여야 합니다. ‘스타일’이 1로 설정된 경우 식의 처음 두 자가 반드시 0x여야 합니다.  식에 홀수 개의 문자나 유효하지 않은 문자가 포함되어 있으면 오류가 발생합니다.<br /><br /> 변환된 식의 길이가 *data_type*의 길이보다 길면 결과의 오른쪽이 잘립니다.<br /><br /> 고정 길이 *data_types*가 변환된 결과보다 길면 결과의 오른쪽에 0이 추가됩니다.<br /><br /> 형식 문자 *data_type*에서는 이진 식을 사용해야 합니다. 각 이진 문자는 두 개의 16진수 문자로 변환됩니다. 변환된 식의 길이가 *data_type*의 길이보다 길면 오른쪽이 잘립니다.<br /><br /> 고정 크기 문자 유형 *data_type*이고 변환된 결과의 길이가 *data_type*의 길이보다 짧으면 짝수 개의 16진수가 유지되도록 변환된 식의 오른쪽에 공백이 추가됩니다.<br /><br /> *style* 1의 경우 변환된 결과의 왼쪽에 문자 0x가 추가됩니다.|  
  
## <a name="implicit-conversions"></a>암시적 변환
암시적 변환에서는 CAST 함수나 CONVERT 함수 지정이 필요하지 않습니다. 명시적 변환에서는 CAST 함수나 CONVERT 함수를 지정해야 합니다. 다음 그림에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 제공 데이터 형식에 허용된 모든 명시적 및 암시적 데이터 형식 변환을 보여 줍니다. 여기에는 **bigint**, **sql_variant** 및 **xml**이 포함됩니다. 할당 시 **sql_variant** 데이터 형식에서 암시적으로 변환되지는 않지만 **sql_variant**로는 암시적으로 변환됩니다.
  
> [!TIP]  
> 이 차트는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=35834)에서 PNG 파일로 다운로드할 수 있습니다.  
  
![데이터 형식 변환 테이블](../../t-sql/data-types/media/lrdatahd.png "데이터 형식 변환 테이블")
  
위 차트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 허용되는 모든 명시적 및 암시적 변환을 보여 주지만, 변환의 결과 데이터 형식은 수행 중인 작업에 따라 다릅니다.

-  명시적 변환의 경우 문 자체에서 결과 데이터 형식을 결정합니다.    
-  암시적 변환의 경우 변수 값을 설정하거나 열에 값을 삽입하는 등의 대입문은 변수 선언 또는 열 정의에 의해 정의된 데이터 형식으로 이어집니다.    
-  비교 연산자 또는 다른 식의 경우 결과 데이터 형식은 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md) 규칙에 따라 달라집니다.

> [!TIP]
> [변환에서 데이터 형식 우선 순위의 효과](#precedence-example)에 대한 실질적인 예는 이 섹션의 뒷부분에서 확인할 수 있습니다.

**datetimeoffset**과 **char**, **nchar**, **nvarchar** 및 **varchar** 문자 형식 간에 변환할 경우 변환된 표준 시간대 오프셋 부분의 HH 및 MM 부분은 항상 두 자리여야 합니다. 예를 들어 -08:00입니다.
  
> [!NOTE]   
> 유니코드 데이터는 항상 짝수 바이트를 사용하므로 **binary** 또는 **varbinary**와 유니코드 지원 데이터 형식을 서로 변환할 때는 주의해야 합니다. 예를 들어 다음과 같은 변환은 16진수 값 41이 아니라 4100의 16 진수 값을 반환합니다(`SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)`). 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요. 
  
## <a name="large-value-data-types"></a>큰 값 데이터 형식
큰 값 데이터 형식은 작은 데이터 형식, 특히 **nvarchar**, **varbinary** 및 **varchar** 데이터 형식과 같은 암시적 및 명시적 변환 동작을 보입니다. 그러나 다음 지침을 고려합니다.
-   **image**와 **varbinary(max)** 간 변환은 암시적 변환이며 **text**와 **varchar(max)** 간, **ntext**와 **nvarchar(max)** 간 변환도 암시적 변환입니다.  
-   **varchar(max)** 등 큰 값 데이터 형식을 **varchar** 등의 작은 데이터 형식으로 변환하는 것은 암시적 변환이지만 작은 데이터 형식에 지정된 길이에 비해 큰 값이 너무 크면 값이 잘립니다.  
-   **nvarchar**, **varbinary** 또는r **varchar**를 해당하는 큰 값 데이터 형식으로 변환하는 것은 암시적으로 수행됩니다.  
-   **sql_variant** 데이터 형식을 큰 값 데이터 형식으로 변환하는 것은 명시적 변환입니다.  
-   큰 값 데이터 형식은 **sql_variant** 데이터 형식으로 변환할 수 없습니다.  
  
**xml** 데이터 형식을 변환에 대한 자세한 내용은 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)를 참조하세요.
  
## <a name="xml-data-type"></a>XML 데이터 형식입니다.
**xml** 데이터 형식을 명시적 또는 암시적으로 문자열 또는 바이너리 데이터 형식으로 변환할 때는 **xml** 데이터 형식의 내용이 정의된 일련의 규칙에 따라 직렬화됩니다. 이러한 규칙에 대한 자세한 내용은 [XML 데이터 직렬화 정의](../../relational-databases/xml/define-the-serialization-of-xml-data.md)를 참조하세요. 다른 데이터 형식에서 **xml** 데이터 형식으로의 변환에 대한 자세한 내용은 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)를 참조하세요.
  
## <a name="text-and-image-data-types"></a>text 및 image 데이터 형식
**text** 및 **image** 데이터 형식은 자동 데이터 형식 변환을 지원하지 않습니다. 명시적으로 **text** 데이터를 문자 데이터로 변환하거나 **image** 데이터를 **binary** 또는 **varbinary**로 변환할 수 있지만 최대 길이는 8,000바이트입니다. 문자가 포함된 문자 식을 **int**로 변환하는 등 잘못된 변환을 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류 메시지를 반환합니다.
  
## <a name="output-collation"></a>출력 데이터 정렬  
CAST 또는 CONVERT 함수가 문자열을 출력하고 문자열 입력을 받으면 출력과 입력은 동일한 데이터 정렬 및 데이터 정렬 레이블을 가집니다. 입력이 문자열이 아닌 경우에는 출력에서 데이터베이스의 기본 데이터 정렬을 사용하며 강제할 수 있는 기본값의 데이터 정렬 레이블을 사용합니다. 자세한 내용은 [데이터 정렬 선행 규칙&#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)을 참조하세요.
  
출력에 다른 데이터 정렬을 할당하려면 CAST 또는 CONVERT 함수의 결과 식에 COLLATE 절을 적용합니다. 다음은 그 예입니다.
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>결과 잘라내기 및 반올림
문자 또는 이진 식(**binary**, **char**, **nchar**, **nvarchar**, **varbinary** 또는 **varchar**)을 데이터 형식이 다른 식으로 변환할 때는 변환 작업에서 출력 데이터를 잘라 출력 데이터의 일부만 표시하거나 오류를 반환할 수 있습니다. 이러한 상황은 결과가 너무 작아 표시할 수 없을 때 발생합니다. **binary**, **char**, **nchar**, **nvarchar**, **varbinary** 또는**varchar**로 변환하면 다음 표에 있는 변환을 제외하고 결과가 잘립니다.
  
|원래 데이터 형식|변경할 데이터 형식|결과|  
|---|---|---|
|**int**, **smallint** 또는 **tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**money**, **smallmoney**, **numeric**, **decimal**, **float** 또는 **real**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\* = 결과 길이가 너무 짧아 표시되지 않습니다.<br /><br />E = 결과 길이가 너무 짧아 표시되지 않으므로 오류가 반환됩니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 원래 데이터 형식을 변환한 후 다시 원래 데이터 형식으로 변환하는 왕복 변환만 버전 간에 같은 값을 생성합니다. 다음 예에서는 이러한 왕복 변환을 보여 줍니다.
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!WARNING]  
> **binary** 값을 생성한 다음, 숫자 데이터 형식 범주에 속하는 데이터 형식으로 변환하지 마세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **decimal** 또는 **numeric** 데이터 형식을 **binary**로 변환하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 간에 결과가 다를 수도 있습니다.  
  
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
  
소수 자릿수가 다른 데이터 형식을 변환할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 결과 값을 자르거나 반올림할 수 있습니다. 이 표에서는 이러한 동작을 보여 줍니다.
  
|보낸 사람|수행할 작업|동작|  
|---|---|---|
|**numeric**|**numeric**|Round|  
|**numeric**|**int**|Truncate|  
|**numeric**|**money**|Round|  
|**money**|**int**|Round|  
|**money**|**numeric**|Round|  
|**float**|**int**|Truncate|  
|**float**|**numeric**|Round<br /><br /> 과학적 표기법을 사용하는 **float** 값을 **decimal** 또는 **numerci**로 변환할 경우 전체 자릿수 값이 17자리로 제한됩니다. 17자리를 넘는 값은 0으로 반올림됩니다.|  
|**float**|**datetime**|Round|  
|**datetime**|**int**|Round|  
  
예를 들어 10.6496 및 -10.6496을 **int** 또는 **numeric** 형식으로 변환할 경우 잘리거나 반올림될 수 있습니다.
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
쿼리 결과가 다음 표에 나와 있습니다.
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
대상 데이터 형식의 소수 자릿수가 원본 데이터 형식의 소수 자릿수보다 적은 데이터 형식을 변환할 경우 값이 반올림됩니다. 예를 들어 이 변환은 `$10.3497`을 반환합니다.
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 숫자가 아닌 **char**, **nchar**, **nvarchar** 또는 **varchar** 데이터를 **decimal**, **float**, **int**, **numeric**으로 변환할 경우 오류 메시지가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 빈 문자열(" ")을 **numeric** 또는 **decimal**로 변환해도 오류가 반환됩니다.
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>일부 datetime 변환은 비결정적임
다음 표에서는 문자열에서 datetime으로의 변환이 비결정적인 스타일을 나열합니다.
  
|||  
|-|-|  
|100<sup>1</sup> 아래의 모든 스타일|106|  
|107|109|  
|113|130|  
  
<sup>1</sup> 스타일 20 및 21 제외

자세한 내용은 [날짜 값으로 리터럴 날짜 문자열의 비결정적 변환](../data-types/nondeterministic-convert-date-literals.md)을 참조하세요.

## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 SC(보조 문자) 데이터 정렬을 사용할 경우 **nchar** 또는 **nvarchar** 형식에서 길이가 작은 **nchar** 또는 **nvarchar** 형식으로 CAST 연산을 수행하면 서로게이트 쌍 안에서 자르지 않습니다. 대신 이 연산은 보조 문자 앞에서 자릅니다. 예를 들어 다음 코드 조각에서는 `@x`만 보유한 `'ab'`를 남깁니다. 공간이 부족하여 보조 문자를 포함할 수 없습니다.
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
SC 데이터 정렬을 사용할 경우 `CONVERT`의 동작은 `CAST`의 동작과 유사합니다. 자세한 내용은 [데이터 정렬 및 유니코드 지원 - 보조 문자](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters)를 참조하세요.
  
## <a name="compatibility-support"></a>호환성 지원
이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **time** 또는 **datetime2** 데이터 형식이 계산 열 식에 사용된 경우를 제외하고 해당 형식에 대한 CAST 및 CONVERT 연산의 기본 스타일은 121입니다. 계산 열의 경우 기본 스타일은 0입니다. 이 동작은 자동 매개 변수화와 관련된 쿼리에서 이러한 연산이 만들어지고 사용될 때 또는 제약 조건 정의에 사용될 때 계산 열에 영향을 줍니다.
  
[호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades) 110 이상에서 **time** 및 **datetime2** 데이터 형식에 대한 CAST 및 CONVERT 연산의 기본 스타일은 항상 121입니다. 쿼리에 이전 동작이 적용되는 경우 110보다 낮은 호환성 수준을 사용하거나, 해당 쿼리에서 스타일 0을 명시적으로 지정해야 합니다.

|[호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades) 값|CAST 및 CONVERT용 기본 스타일<sup>1</sup>|계산 열의 기본 스타일|  
|------------|------------|------------|
|< **110**|121|0|  
|> = **110**|121|121|  

<sup>1</sup> 계산 열 제외

데이터베이스를 호환성 수준 110 이상으로 업그레이드할 경우 디스크에 저장된 사용자 데이터는 변경되지 않습니다. 수동으로 이 데이터를 적절하게 수정해야 합니다. 예를 들어 SELECT INTO를 사용하여 위에서 설명한 계산 열 식이 포함된 원본에서 테이블을 만든 경우 계산 열 정의 자체가 아니라 스타일 0을 사용하는 데이터가 저장됩니다. 스타일 121과 일치하도록 이 데이터를 수동으로 업데이트해야 합니다.
  
## <a name="examples"></a><a name="BKMK_examples"></a> 예  
  
### <a name="a-using-both-cast-and-convert"></a>A. CAST 및 CONVERT 모두 사용  
각 예에서는 제품 가격 첫 자리에 `3`이 있는 제품의 이름을 검색하고 `ListPrice` 값을 `int`로 변환합니다.
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '33%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '33%';  
GO  
```  

[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 예제 결과 집합은 CAST와 CONVERT 모두에 대해 동일합니다. 

```
ProductName                    ListPrice
------------------------------ ---------------------
LL Road Frame - Black, 58      337.22
LL Road Frame - Black, 60      337.22
LL Road Frame - Black, 62      337.22
LL Road Frame - Red, 44        337.22
LL Road Frame - Red, 48        337.22
LL Road Frame - Red, 52        337.22
LL Road Frame - Red, 58        337.22
LL Road Frame - Red, 60        337.22
LL Road Frame - Red, 62        337.22
LL Road Frame - Black, 44      337.22
LL Road Frame - Black, 48      337.22
LL Road Frame - Black, 52      337.22
Mountain-100 Black, 38         3374.99
Mountain-100 Black, 42         3374.99
Mountain-100 Black, 44         3374.99
Mountain-100 Black, 48         3374.99
HL Road Front Wheel            330.06
LL Touring Frame - Yellow, 62  333.42
LL Touring Frame - Blue, 50    333.42
LL Touring Frame - Blue, 54    333.42
LL Touring Frame - Blue, 58    333.42
LL Touring Frame - Blue, 62    333.42
LL Touring Frame - Yellow, 44  333.42
LL Touring Frame - Yellow, 50  333.42
LL Touring Frame - Yellow, 54  333.42
LL Touring Frame - Yellow, 58  333.42
LL Touring Frame - Blue, 44    333.42
HL Road Tire                   32.60

(28 rows affected)
```
  
### <a name="b-using-cast-with-arithmetic-operators"></a>B. CAST에 산술 연산자 사용  
이 예에서는 총 연간 매출(`Computed`)을 커미션 비율(`SalesYTD`)로 나누어 한 열을 계산(`CommissionPCT`)합니다. 이 값은 가장 근사한 정수로 반올림된 다음, `int` 데이터 형식으로 CAST 연산이 수행됩니다.
  
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
  
### <a name="c-using-cast-to-concatenate"></a>C. CAST를 사용하여 연결  
이 예에서는 CAST를 사용하여 문자가 아닌 식을 연결합니다. AdventureWorksDW 데이터베이스를 사용합니다.
  
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
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>D. CAST를 사용하여 읽기 쉬운 텍스트 만들기  
이 예에서는 SELECT 목록에 CAST를 사용하여 `Name` 열을 **char(10)** 열로 변환합니다. AdventureWorksDW 데이터베이스를 사용합니다.
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        ListPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="e-using-cast-with-the-like-clause"></a>E. CAST에 LIKE 절 사용  
이 예에서는 `money` 열 `SalesYTD` 값을 `int` 데이터 형식으로 변환한 다음, `char(20)` 데이터 형식으로 변환하여 `LIKE` 절이 사용할 수 있게 합니다.
  
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
FirstName        LastName            SalesYTD         BusinessEntityID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289

(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. 형식화된 XML과 함께 CONVERT 또는 CAST 사용  
이 예제에서는 CONVERT와 [XML 데이터 형식 및 열&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md)을 사용하여 데이터를 형식화된 XML로 변환하는 것을 보여 줍니다.
  
다음 예에서는 공백, 텍스트 및 태그가 있는 문자열을 형식화된 XML로 변환하고 불필요한 공백(노드 사이의 경계 공백)을 모두 제거합니다.
  
```sql
SELECT CONVERT(XML, '<root><child/></root>')  
```  
  
다음 예에서는 공백, 텍스트 및 태그가 있는 비슷한 문자열을 형식화된 XML로 변환하고 불필요한 공백(노드 사이의 경계 공백)을 유지합니다.
  
```sql
SELECT CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
다음 예에서는 공백, 텍스트 및 태그가 있는 문자열을 형식화된 XML로 캐스팅합니다.
  
```sql
SELECT CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
다른 예는 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)를 참조하세요.
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>G. datetime 데이터와 함께 CAST 및 CONVERT 사용  
`GETDATE()` 값으로 시작하는 다음 예에서는 현재 날짜와 시간을 표시합니다. 즉, `CAST`를 사용하여 현재 날짜와 시간을 문자 데이터 형식으로 변경한 다음, `CONVERT`를 사용하여 `ISO 8601` 형식으로 날짜와 시간을 표시합니다.
  
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
  
이 예에서는 이전 예와 반대로 수행합니다. 이 예에서는 날짜와 시간을 문자 데이터로 표시합니다. 즉, `CAST`를 사용하여 문자 데이터를 `datetime` 데이터 형식으로 변경한 다음, `CONVERT`를 사용하여 문자 데이터를 `datetime` 데이터 형식으로 변경합니다.
  
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
  
### <a name="h-using-convert-with-binary-and-character-data"></a>H. CONVERT에 이진 및 문자 데이터 사용  
이 예에서는 다양한 스타일을 사용하여 이진 및 문자 데이터를 변환한 결과를 보여 줍니다.
  
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
 
이 예에서는 스타일 1에서 결과 잘림이 발생할 수 있음을 보여 줍니다. 결과 집합의 0x 문자로 인해 잘림이 발생합니다.  
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
 
이 예는 결과에 0x 문자가 포함되지 않았기 때문에 Style 2에서 결과가 잘리지 않았음을 보여 줍니다.  
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
  
'Name' 문자 값을 이진 값으로 변환합니다.  
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
  
### <a name="i-converting-date-and-time-data-types"></a>9\. 날짜 및 시간 데이터 형식 변환  
이 예는 date, time 및 datetime 데이터 형식의 변환을 보여 줍니다.
  
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

### <a name="j-using-convert-with-datetime-data-in-different-formats"></a>J. 다른 형식의 datetime 데이터로 CONVERT 사용  
`GETDATE()` 값에서 시작하는 이 예에서는 `CONVERT`를 사용하여 이 글의 [날짜 및 시간 스타일](#date-and-time-styles) 섹션의 모든 날짜 및 시간 스타일을 표시합니다.

|Format #|예제 쿼리|샘플 결과|
|--------|------------------------------------|------------------|
|0|`SELECT CONVERT(nvarchar, GETDATE(), 0)`|Aug 23 2019  1:39PM|
|1|`SELECT CONVERT(nvarchar, GETDATE(), 1)`|08/23/19|
|2|`SELECT CONVERT(nvarchar, GETDATE(), 2)`|19.08.23|
|3|`SELECT CONVERT(nvarchar, GETDATE(), 3)`|23/08/19|
|4|`SELECT CONVERT(nvarchar, GETDATE(), 4)`|23.08.19|
|5|`SELECT CONVERT(nvarchar, GETDATE(), 5)`|23-08-19|
|6|`SELECT CONVERT(nvarchar, GETDATE(), 6)`|23 Aug 19|
|7|`SELECT CONVERT(nvarchar, GETDATE(), 7)`|Aug 23, 19|
|8 or 24 or 108|`SELECT CONVERT(nvarchar, GETDATE(), 8)`|13:39:17|
|9 또는 109|`SELECT CONVERT(nvarchar, GETDATE(), 9)`|Aug 23 2019  1:39:17:090PM|
|10|`SELECT CONVERT(nvarchar, GETDATE(), 10)`|08-23-19|
|11|`SELECT CONVERT(nvarchar, GETDATE(), 11)`|19/08/23|
|12|`SELECT CONVERT(nvarchar, GETDATE(), 12)`|190823|
|13 또는 113|`SELECT CONVERT(nvarchar, GETDATE(), 13)`|23 Aug 2019 13:39:17:090|
|14 or 114|`SELECT CONVERT(nvarchar, GETDATE(), 14)`|13:39:17:090|
|20 또는 120|`SELECT CONVERT(nvarchar, GETDATE(), 20)`|2019-08-23 13:39:17|
|21 or 25 or 121|`SELECT CONVERT(nvarchar, GETDATE(), 21)`|2019-08-23 13:39:17.090|
|22|`SELECT CONVERT(nvarchar, GETDATE(), 22)`|08/23/19  1:39:17 PM|
|23|`SELECT CONVERT(nvarchar, GETDATE(), 23)`|2019-08-23|
|101|`SELECT CONVERT(nvarchar, GETDATE(), 101)`|08/23/2019|
|102|`SELECT CONVERT(nvarchar, GETDATE(), 102)`|2019.08.23|
|103|`SELECT CONVERT(nvarchar, GETDATE(), 103)`|23/08/2019|
|104|`SELECT CONVERT(nvarchar, GETDATE(), 104)`|23.08.2019|
|105|`SELECT CONVERT(nvarchar, GETDATE(), 105)`|23-08-2019|
|106|`SELECT CONVERT(nvarchar, GETDATE(), 106)`|23 Aug 2019|
|107|`SELECT CONVERT(nvarchar, GETDATE(), 107)`|Aug 23, 2019|
|110|`SELECT CONVERT(nvarchar, GETDATE(), 110)`|08-23-2019|
|111|`SELECT CONVERT(nvarchar, GETDATE(), 111)`|2019/08/23|
|112|`SELECT CONVERT(nvarchar, GETDATE(), 112)`|20190823|
|113|`SELECT CONVERT(nvarchar, GETDATE(), 113)`|23 Aug 2019 13:39:17.090|
|120|`SELECT CONVERT(nvarchar, GETDATE(), 120)`|2019-08-23 13:39:17|
|121|`SELECT CONVERT(nvarchar, GETDATE(), 121)`|2019-08-23 13:39:17.090|
|126|`SELECT CONVERT(nvarchar, GETDATE(), 126)`|2019-08-23T13:39:17.090|
|127|`SELECT CONVERT(nvarchar, GETDATE(), 127)`|2019-08-23T13:39:17.090|
|130|`SELECT CONVERT(nvarchar, GETDATE(), 130)`|22 ذو الحجة 1440  1:39:17.090P|
|131|`SELECT CONVERT(nvarchar, GETDATE(), 131)`|22/12/1440  1:39:17.090PM|

### <a name="k-effects-of-data-type-precedence-in-allowed-conversions"></a><a name="precedence-example"></a> K. 허용되는 변환에서 데이터 형식 우선 순위의 효과  
다음의 예는 형식 VARCHAR 변수를 정의하고 변수에 정수 값을 할당한 다음 문자열과 변수의 연결을 선택합니다.

```sql
DECLARE @string varchar(10);
SET @string = 1;
SELECT @string + ' is a string.' AS Result
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Result
-----------------------
1 is a string.
```  

정수 값 1이 VARCHAR로 변환되었습니다.

이 예에서는 int 변수를 다음 대신 사용하여 유사한 쿼리를 표시합니다.

```sql
DECLARE @notastring int;
SET @notastring = '1';
SELECT @notastring + ' is not a string.' AS Result
```

이 경우 SELECT 문은 다음 오류를 발생시킵니다.

```
Msg 245, Level 16, State 1, Line 3
Conversion failed when converting the varchar value ' is not a string.' to data type int.
```

`@notastring + ' is not a string.'` 식을 평가하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 데이터 형식 우선 순위 규칙에 따라 식 결과를 계산하기 전에 암시적 변환을 완료해야 합니다. 정수는 VARCHAR보다 우선 순위가 높기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 문자열을 정수로 변환하려고 시도하지만 이 문자열을 정수로 변환할 수 없으므로 실패합니다. 

변환할 수 있는 문자열을 제공하는 경우 다음 예제에 표시된 것처럼 문이 성공합니다.

```SQL
DECLARE @notastring int;
SET @notastring = '1';
SELECT @notastring + '1'
```

이 경우 문자열 `'1'`을 정수 값 1로 변환할 수 있으므로 이 SELECT 문은 값 2를 반환합니다. 제공된 데이터 형식이 정수인 경우 + 연산자는 문자열 연결이 아닌 더하기 수치 연산자가 됩니다.

## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="l-using-cast-and-convert"></a>12. CAST 및 CONVERT 사용  
이 예에서는 제품 가격 첫 자리에 `3`이 있는 제품의 이름을 검색하고 이 제품의 `ListPrice`를 **int**로 변환합니다. `AdventureWorksDW2016` 데이터베이스를 사용합니다.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
이 예는 CAST 대신 CONVERT를 사용하여 동일한 쿼리를 보여줍니다. `AdventureWorksDW2016` 데이터베이스를 사용합니다.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="m-using-cast-with-arithmetic-operators"></a>13. CAST에 산술 연산자 사용  
이 예에서는 제품 단가(`UnitPrice`)를 할인율(`UnitPriceDiscountPct`)로 나누어 한 열 값을 계산합니다. 그런 다음, 이 결과를 가장 가까운 정수로 반올림한 후 `int` 데이터 형식으로 변환합니다. 다음 예에서는 `AdventureWorksDW2016` 데이터베이스를 사용합니다.
  
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
  
### <a name="n-using-cast-with-the-like-clause"></a>14. CAST에 LIKE 절 사용  
이 예에서는 **money** 열 `ListPrice`를 **int** 형식으로 변환한 다음, LIKE 절에 사용할 수 있도록 **char(20)** 형식으로 변환합니다. 다음 예에서는 `AdventureWorksDW2016` 데이터베이스를 사용합니다.  
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="o-using-cast-and-convert-with-datetime-data"></a>15. datetime 데이터와 함께 CAST 및 CONVERT 사용  
이 예에서는 현재 날짜와 시간을 표시하고, CAST를 사용하여 현재 날짜와 시간을 문자 데이터 형식으로 변환한 다음, CONVERT를 사용하여 날짜와 시간을 ISO 8601 형식으로 표시합니다. 다음 예에서는 `AdventureWorksDW2016` 데이터베이스를 사용합니다.
  
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
  
이 예에서는 이전 예와 거의 반대로 수행됩니다. 이 예에서는 날짜와 시간을 문자 데이터로 표시합니다. 즉, CAST를 사용하여 문자 데이터를 **datetime** 데이터 형식으로 변경한 다음, CONVERT를 사용하여 문자 데이터를 **datetime** 데이터 형식으로 변경합니다. 다음 예에서는 `AdventureWorksDW2016` 데이터베이스를 사용합니다.
  
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
[데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)       
[데이터 형식 변환&#40;Database Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)     
[형식 &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)      
[STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)     
[SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)      
[시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)      
[데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)      
[국가별 Transact-SQL 문 작성](../../relational-databases/collations/write-international-transact-sql-statements.md)       
  
