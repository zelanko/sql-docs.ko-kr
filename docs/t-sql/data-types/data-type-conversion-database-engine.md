---
title: "데이터 형식 변환 (데이터베이스 엔진) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0ed7f8e0e681de9f962e3eb963c0af315a0c25c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-conversion-database-engine"></a>데이터 형식 변환 (데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

데이터 형식은 다음 시나리오에서 변환할 수 있습니다.
-   한 개체의 데이터가 다른 개체의 데이터로 이동하거나 그 데이터와 비교되거나 결합되면 데이터는 그 개체의 데이터 형식에서 다른 개체의 데이터 형식으로 변환되어야 합니다.  
-   때 데이터를는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 데이터를 변환 해야를 프로그램 변수로 이동 결과 열, 반환 코드 또는 출력 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변수의 데이터 형식으로 시스템 데이터 형식입니다.  
  
응용 프로그램 변수와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 결과 집합 열, 반환 코드, 매개 변수 또는 매개 변수 표식 간에 변환할 때는 데이터베이스 API에 따라 지원되는 데이터 형식 변환이 정의됩니다.
  
## <a name="implicit-and-explicit-conversion"></a>암시적 및 명시적 변환
데이터 형식은 암시적으로 또는 명시적으로 변환할 수 있습니다.
  
암시적 변환은 사용자에게 보이지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터 형식을 자동으로 변환합니다. 예를 들어, 한 **smallint** 에 비해는 **int**, **smallint** 암시적으로 변환할 **int** 비교 하기 전에 진행 됩니다.
  
**Getdate ()** 날짜 스타일 0 암시적으로 변환 합니다. **SYSDATETIME()** 암시적으로 날짜 스타일 21로 변환 합니다.
  
명시적 변환은 CAST 또는 CONVERT 함수를 사용합니다.
  
[CAST 및 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수를 다른 값 (지역 변수, 열, 또는 다른 식)의 데이터 형식을 변환 합니다. 예를 들어 다음 `CAST` 함수는 `$157.27`의 숫자 값을 `'157.27'`의 문자열로 변환합니다.
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그램 코드를 ISO에 맞추려면 CONVERT 대신 CAT를 사용하고, CONVERT의 스타일 기능을 사용하려면 CAST 대신 CONVERT를 사용합니다.
  
다음 그림에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 제공 데이터 형식에 허용된 모든 명시적 및 암시적 데이터 형식 변환을 보여 줍니다. 여기에 **xml**, **bigint**, 및 **sql_variant**합니다. 할당에 암시적 변환이 이루어지지는 **sql_variant** 데이터 형식으로 암시적 변환이 있지만 **sql_variant**합니다.
  
![데이터 형식 변환 표](../../t-sql/data-types/media/lrdatahd.png "데이터 형식 변환 표")
  
## <a name="data-type-conversion-behaviors"></a>데이터 형식 변환 동작
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 데이터 형식을 변환할 때 일부 암시적 및 명시적 데이터 형식 변환은 지원되지 않습니다. 예를 들어 한 **nchar** 값을 변환할 수 없습니다는 **이미지** 값입니다. **nchar** 로 변환할 수 **이진** 으로 암시적 변환이 명시적 변환을 사용 하 여 **이진** 지원 되지 않습니다. 그러나는 **nchar** 명시적 또는 암시적으로 변환할 수 **nvarchar**합니다.
  
다음 항목에서는 해당 데이터 형식이 나타내는 변환 동작에 대해 설명합니다.
  
 - [binary 및 varbinary&#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2&#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money 및 smallmoney &#40; Transact SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [비트 &#40; Transact SQL &#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset&#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40; Transact SQL &#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char 및 varchar&#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal 및 numeric&#40; Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant&#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date&#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float 및 real &#40; Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [시간 &#40; Transact SQL &#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [날짜/시간 &#40; Transact SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint 및 tinyint &#40; Transact SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40; Transact SQL &#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>OLE Automation 저장 프로시저를 사용하여 데이터 형식 변환  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 형식을 사용하고 OLE Automation은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 데이터 형식을 사용하므로 OLE Automation 저장 프로시저는 이들 간에 전달되는 데이터를 변환해야 합니다.
  
다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 데이터 형식으로 변환하는 방법을 설명합니다.
  
|SQL Server 데이터 형식|Visual Basic 데이터 형식|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **텍스트**, **nvarchar**, **ntext**|**문자열**|  
|**10 진수**, **숫자**|**문자열**|  
|**bit**|**Boolean**|  
|**이진**, **varbinary**, **이미지**|1 차원 **byte ()** 배열|  
|**int**|**Long**|  
|**smallint**|**정수**|  
|**tinyint**|**바이트**|  
|**float**|**Double**|  
|**real**|**단일**|  
|**money**, **smallmoney**|**Currency**|  
|**날짜/시간**, **smalldatetime**|**날짜**|  
|NULL로 설정된 모든 것|**Variant** Null로 설정|  
  
모든 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값 변환 되며 단일 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 제외 값 **이진**, **varbinary**, 및 **이미지** 값입니다. 이러한 값을 1 차원으로 변환할지 **byte ()** 배열로 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]합니다. 이 배열 범위에가 **바이트 (**0 ~ *길이*1**)** 여기서 *길이* 의 바이트 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  **이진**, **varbinary**, 또는 **이미지** 값입니다.
  
이들은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 데이터 형식에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환한 것입니다.
  
|Visual Basic 데이터 형식|SQL Server 데이터 형식|  
|----------------------------|--------------------------|  
|**긴**, **정수**, **바이트**, **부울**, **개체**|**int**|  
|**이중**, **단일**|**float**|  
|**Currency**|**money**|  
|**날짜**|**datetime**|  
|**문자열** 4000 자 이하의|**varchar**/**nvarchar**|  
|**문자열** 이상 4000 자|**텍스트**/**ntext**|  
|1 차원 **byte ()** 8000 바이트 이하의 배열|**varbinary**|  
|1 차원 **byte ()** 8000 바이트 초과 된 배열|**image**|  
  
## <a name="see-also"></a>참고 항목
[OLE 자동화 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  

