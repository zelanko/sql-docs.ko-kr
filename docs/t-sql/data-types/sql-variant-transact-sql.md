---
description: sql_variant(Transact-SQL)
title: sql_variant(Transact-SQL)
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a1b6f93654e312f8c7a0266b3500c18a38ff511a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445925"
---
# <a name="sql_variant-transact-sql"></a>sql_variant(Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원하는 여러 가지 데이터 형식의 값을 저장하는 데이터 형식입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
sql_variant  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명  
**sql_variant**는 열, 매개 변수, 변수 및 사용자 정의 함수의 반환 값으로 사용될 수 있습니다. **sql_variant**는 이 데이터베이스 개체들이 다른 데이터 형식의 값을 지원할 수 있게 합니다.
  
**sql_variant** 형식의 열은 다른 데이터 형식의 행을 포함할 수 있습니다. 예를 들어 **sql_variant**로 정의된 열은 **int**, **binary** 및 **char** 값을 저장할 수 있습니다.
  
**sql_variant**는 최대 8016바이트의 길이를 가질 수 있습니다. 여기에는 기본 유형 정보 및 기본 유형 값이 모두 포함됩니다. 실제 기본 유형 값의 최대 길이는 8,000바이트입니다.
  
**sql_variant** 데이터 형식은 덧셈 및 뺄셈과 같은 연산에 사용되기 전에 먼저 기본 데이터 형식 값으로 캐스팅되어야 합니다.
  
**sql_variant**에 기본값을 할당할 수 있습니다. 이 데이터 형식은 NULL을 기초값으로 가질 수는 있지만 NULL 값은 연결된 기본 유형을 갖지 않습니다. 또한 **sql_variant**는 기본 유형으로 다른 **sql_variant**를 가질 수 없습니다.
  
고유 키, 기본 키 또는 외래 키는 **sql_variant** 형식의 열을 포함할 수 있지만 특정 행의 키를 구성하는 데이터 값의 총 길이는 인덱스의 최대 길이(900바이트)보다 크면 안 됩니다.
  
테이블은 **sql_variant** 열을 얼마든지 포함할 수 있습니다.
  
**sql_variant**를 CONTAINSTABLE 및 FREETEXTTABLE에 사용할 수 없습니다.
  
ODBC에서는 **sql_variant**를 모두 지원하지는 않습니다. 따라서 Microsoft OLE DB Provider for ODBC(MSDASQL)를 사용할 때 **sql_variant** 열을 쿼리하면 이진 데이터로 반환됩니다. 예를 들어 문자열 데이터 'PS2091'를 포함하는 **sql_variant** 열은 0x505332303931로 반환됩니다.
  
## <a name="comparing-sql_variant-values"></a>sql_variant 값 비교  
**sql_variant** 데이터 형식은 변환을 위한 데이터 형식 계층 구조 목록의 맨 위에 속합니다. **sql_variant** 비교를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 계층 구조 순서는 데이터 형식 패밀리로 그룹화됩니다.
  
|데이터 형식 계층|데이터 형식 패밀리|  
|---|---|
|**sql_variant**|sql_variant |  
|**datetime2**|날짜 및 시간|  
|**datetimeoffset**|날짜 및 시간|  
|**datetime**|날짜 및 시간|  
|**smalldatetime**|날짜 및 시간|  
|**date**|날짜 및 시간|  
|**time**|날짜 및 시간|  
|**float**|근사치|  
|**real**|근사치|  
|**decimal**|정확한 수치|  
|**money**|정확한 수치|  
|**smallmoney**|정확한 수치|  
|**bigint**|정확한 수치|  
|**int**|정확한 수치|  
|**smallint**|정확한 수치|  
|**tinyint**|정확한 수치|  
|**bit**|정확한 수치|  
|**nvarchar**|Unicode|  
|**nchar**|Unicode|  
|**varchar**|Unicode|  
|**char**|Unicode|  
|**varbinary**|이진|  
|**binary**|이진|  
|**uniqueidentifier**|Uniqueidentifier |  
  
**sql_variant** 비교에는 다음 규칙이 적용됩니다.
-   서로 다른 기본 데이터 형식의 **sql_variant** 값을 비교할 때 기본 데이터 형식이 서로 다른 데이터 형식 패밀리에 있으면 계층 구조 차트에서 더 높은 데이터 형식 패밀리의 값이 두 값 중 더 큰 것으로 간주됩니다.  
-   서로 다른 기본 데이터 형식의 **sql_variant** 값을 비교할 때 기본 데이터 형식이 동일한 데이터 형식 패밀리에 있으면 계층 구조 차트에서 더 낮은 기본 데이터 형식의 값이 암시적으로 다른 데이터 형식으로 변환된 다음, 비교됩니다.  
-   **char**, **varchar**, **nchar** 또는 **nvarchar** 데이터 형식의 **sql_variant** 값을 비교하는 경우 해당 데이터 정렬은 먼저 LCID, LCID 버전, 비교 플래그 및 정렬 ID와 같은 기준에 따라 비교됩니다. 이러한 조건은 각각 정수 값으로, 그리고 나열된 순서대로 비교됩니다. 이러한 모든 조건이 같다면 실제 문자열 값은 데이터 정렬에 따라 비교됩니다.  
  
## <a name="converting-sql_variant-data"></a>sql_variant 데이터 변환  
**sql_variant** 데이터 형식을 처리할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 개체의 데이터 형식을 **sql_variant** 형식으로 암시적으로 변환할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 **sql_variant** 데이터에서 다른 데이터 형식의 개체로의 암시 적 변환을 지원하지 않습니다.
  
## <a name="restrictions"></a>제한

아래에는 **sql_variant**를 사용하여 저장할 수 없는 값 형식이 나열되어 있습니다.

- **datetimeoffset**<sup>1</sup>
- **geography**
- **geometry**
- **hierarchyid**
- **image**
- **ntext**
- **nvarchar(max)**
- **rowversion**(**timestamp**)
- **text**
- **varchar(max)**
- **varbinary(max)**
- **sql_variant**
- 사용자 정의 형식
- **xml**

<sup>1</sup> SQL Server 2012 이상에서는 **datetimeoffset**을 제한하지 않습니다.

## <a name="examples"></a>예  

### <a name="a-using-a-sql_variant-in-a-table"></a>A. 테이블에서 sql_variant 사용  
 다음 예에서는 sql_variant 데이터 형식이 있는 테이블을 만듭니다. 그런 다음, 예제는 `tableA`에 `sql_variant` 및 `colB` 유형인 `colA`가 있는 경우 `colB` =`1689`인 `colA`값`46279.1`에 대한 `SQL_VARIANT_PROPERTY` 정보를 검색합니다.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] 이 세 값은 각각 **sql_variant**입니다.  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sql_variant-as-a-variable"></a>B. 변수로 sql_variant 사용   
 다음 예제에서는 sql_variant 데이터 형식을 사용하여 변수를 만든 다음, @v1 변수에 대한 `SQL_VARIANT_PROPERTY` 정보를 검색합니다.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```    


## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  
