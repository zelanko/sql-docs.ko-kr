---
title: 데이터 형식 변환(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- converting data types [SQL Server]
- CONVERT function
- data types [SQL Server], converting
- implicit data type conversions
- explicit data type conversions [SQL Server]
- converting data types [SQL Server], about converting data types
ms.assetid: ffacf45e-a488-48d0-9bb0-dcc7fd365299
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a9ef3df75a54b6565b1d71c0a9e4557f752f95b
ms.sourcegitcommit: 182ed49fa5a463147273b58ab99dc228413975b6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/31/2019
ms.locfileid: "68697499"
---
# <a name="data-type-conversion-database-engine"></a>데이터 형식 변환(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

데이터 형식은 다음 시나리오에서 변환할 수 있습니다.
-   한 개체의 데이터가 다른 개체의 데이터로 이동하거나 그 데이터와 비교되거나 결합되면 데이터는 그 개체의 데이터 형식에서 다른 개체의 데이터 형식으로 변환되어야 합니다.  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 결과 열, 반환 코드 또는 출력 매개 변수의 데이터가 프로그램 변수로 이동되면 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식에서 변수의 데이터 형식으로 변환해야 합니다.  
  
응용 프로그램 변수와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 결과 집합 열, 반환 코드, 매개 변수 또는 매개 변수 표식 간에 변환할 때는 데이터베이스 API에 따라 지원되는 데이터 형식 변환이 정의됩니다.
  
## <a name="implicit-and-explicit-conversion"></a>암시적 및 명시적 변환
데이터 형식은 암시적으로 또는 명시적으로 변환할 수 있습니다.
  
암시적 변환은 사용자에게 보이지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터 형식을 자동으로 변환합니다. 예를 들어 **smallint**를 **int**와 비교하는 경우 **smallint**는 비교가 진행되기 전에 암시적으로 **int**로 변환됩니다.
  
**GETDATE()** 는 암시적으로 날짜 스타일 0으로 변환합니다. **SYSDATETIME()** 은 암시적으로 날짜 스타일 21로 변환합니다.
  
명시적 변환은 CAST 또는 CONVERT 함수를 사용합니다.
  
[CAST 및 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수는 값(지역 변수, 열 또는 다른 식)을 한 데이터 형식에서 다른 형식으로 변환합니다. 예를 들어 다음 `CAST` 함수는 `$157.27`의 숫자 값을 `'157.27'`의 문자열로 변환합니다.
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그램 코드를 ISO에 맞추려면 CONVERT 대신 CAT를 사용하고, CONVERT의 스타일 기능을 사용하려면 CAST 대신 CONVERT를 사용합니다.
  
다음 그림에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 제공 데이터 형식에 허용된 모든 명시적 및 암시적 데이터 형식 변환을 보여 줍니다. 여기에는 **xml**, **bigint** 및 **sql_variant**가 포함됩니다. 할당 시 **sql_variant** 데이터 형식에서 암시적으로 변환되지는 않지만 **sql_variant**로는 암시적으로 변환됩니다.
  
![데이터 형식 변환표](../../t-sql/data-types/media/lrdatahd.png "데이터 형식 변환표")

위 차트는 SQL Server에서 허용되는 모든 명시적 및 암시적 변환을 보여 주지만 변환의 결과 데이터 형식을 나타내지는 않습니다. SQL Server가 명시적 변환을 수행하면 문 자체에서 결과 데이터 형식을 결정합니다. 암시적 변환의 경우 변수 값을 설정하거나 열에 값을 삽입하는 등의 대입문은 변수 선언 또는 열 정의에 의해 정의된 데이터 형식으로 이어집니다. 비교 연산자 또는 다른 식의 경우 결과 데이터 형식은 데이터 형식 우선 순위 규칙에 따라 달라집니다.

예를 들어 다음 스크립트는 `varchar` 형식 변수를 정의하고 변수에 `int` 형식 값을 할당한 다음 문자열과 변수의 연결을 선택합니다.

```sql
DECLARE @string varchar(10);
SET @string = 1;
SELECT @string + ' is a string.'
```

`1`의 `int` 값은 `varchar`로 변환되므로 `SELECT` 문은 `1 is a string.` 값을 반환합니다.

다음 예에서는 대신 `int` 변수를 사용하는 유사한 스크립트를 보여 줍니다.

```sql
DECLARE @notastring int;
SET @notastring = '1';
SELECT @notastring + ' is not a string.'
```

이 경우 `SELECT` 문은 다음 오류를 발생시킵니다.

`Msg 245, Level 16, State 1, Line 3`
`Conversion failed when converting the varchar value ' is not a string.' to data type int.`

`@notastring + ' is not a string.'` 식을 평가하기 위해 SQL Server는 데이터 형식 우선 순위 규칙에 따라 식 결과를 계산하기 전에 암시적 변환을 완료합니다. `int`는 `varchar`보다 우선 순위가 높기 때문에 SQL Server는 문자열을 정수로 변환하려고 시도하지만 이 문자열을 정수로 변환할 수 없으므로 실패합니다. 식이 변환할 수 있는 문자열을 제공하는 경우 다음 예제와 같이 문이 성공합니다.

```sql
DECLARE @notastring int;
SET @notastring = '1';
SELECT @notastring + '1'
```

이 경우 문자열 `1`을 정수 값 `1`로 변환할 수 있으므로 이 `SELECT` 문은 `2` 값을 반환합니다. 제공된 데이터 형식이 정수인 경우 `+` 연산자는 연결이 아닌 추가가 됩니다.

## <a name="data-type-conversion-behaviors"></a>데이터 형식 변환 동작

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 데이터 형식을 변환할 때 일부 암시적 및 명시적 데이터 형식 변환은 지원되지 않습니다. 예를 들면 **nchar** 값은 **이미지** 값으로 변환할 수 없습니다. **nchar**는 명시적 변환을 사용하여 **이진**으로만 변환할 수 있고, **이진**으로의 암시적 변환은 지원되지 않습니다. 그러나 **nchar**는 암시적으로나 명시적으로 **nvarchar**로 변환할 수 있습니다.
  
다음 항목에서는 해당 데이터 형식이 나타내는 변환 동작에 대해 설명합니다.
  
 - [binary 및 varbinary&#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2&#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money 및 smallmoney&#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40;Transact-SQL&#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset&#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char 및 varchar&#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal 및 numeric&#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant&#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date&#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float 및 real&#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint 및 tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;Transact-SQL&#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>OLE Automation 저장 프로시저를 사용하여 데이터 형식 변환  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 형식을 사용하고 OLE Automation은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 데이터 형식을 사용하므로 OLE Automation 저장 프로시저는 이들 간에 전달되는 데이터를 변환해야 합니다.
  
다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 데이터 형식으로 변환하는 방법을 설명합니다.
  
|SQL Server 데이터 형식|Visual Basic 데이터 형식|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **text**, **nvarchar**, **ntext**|**String**|  
|**decimal**, **numeric**|**String**|  
|**bit**|**Boolean**|  
|**binary**, **varbinary**, **image**|1차원 **Byte()** 배열|  
|**int**|**Long**|  
|**smallint**|**Integer**|  
|**tinyint**|**Byte**|  
|**float**|**Double**|  
|**real**|**단일**|  
|**money**, **smallmoney**|**Currency**|  
|**datetime**, **smalldatetime**|**Date**|  
|NULL로 설정된 모든 것|**Variant**가 null로 설정되었습니다|  
  
단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값은 **binary**, **varbinary** 및 **이미지** 값을 제외하고 모두 단일 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 값으로 변환됩니다. 이러한 값은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]의 1차원 **Byte()** 배열로 변환됩니다. 이 배열에는 **Byte(** _length_ 0에서 1까지 **)** 의 범위가 포함됩니다. 여기서 *length*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binary**, **varbinary** 또는 **image** 값의 바이트 수입니다.
  
이들은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 데이터 형식에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환한 것입니다.
  
|Visual Basic 데이터 형식|SQL Server 데이터 형식|  
|----------------------------|--------------------------|  
|**Long**, **Integer**, **Byte**, **Boolean**, **Object**|**int**|  
|**Double**, **Single**|**float**|  
|**Currency**|**money**|  
|**Date**|**datetime**|  
|4000자 이하의 **문자열**|**varchar**/**nvarchar**|  
|4000자를 초과하는 **문자열**|**text**/**ntext**|  
|8000바이트 이하의 1차원 **Byte()** 배열|**varbinary**|  
|8000바이트를 초과하는 1차원 **Byte()** 배열|**image**|  
  
## <a name="see-also"></a>관련 항목:
[OLE 자동화 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE&#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
