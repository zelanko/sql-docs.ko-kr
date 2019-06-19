---
title: SQL_VARIANT_PROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_VARIANT_PROPERTY_TSQL
- SQL_VARIANT_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- SQL_VARIANT_PROPERTY function
- sql_variant data type
ms.assetid: 50e5c1d9-4e95-4ed0-9c92-435c872a399e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a9f7c245f08ffcd3211277a4d201ed884d66caa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65947658"
---
# <a name="sqlvariantproperty-transact-sql"></a>SQL_VARIANT_PROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  **sql_variant** 값에 대한 기본 데이터 형식 및 기타 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 **sql_variant** 형식의 식입니다.  
  
 *property*  
 정보를 제공할 **sql_variant** 속성의 이름이 포함됩니다. *속성*은 **varchar(** 128 **)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|반환된 sql_variant의 기본 형식|  
|-----------|-----------------|----------------------------------------|  
|**BaseType**|다음과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식<br /><br /> **bigint**<br /><br /> **binary**<br /><br /> **char**<br /><br /> **date**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **ssNoversion**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **smallint**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**정밀도**|숫자 기본 데이터 형식의 전체 자릿수<br /><br /> **datetime** = 23<br /><br /> **smalldatetime** = 16<br /><br /> **float** = 53<br /><br /> **real** = 24<br /><br /> **decimal** (p,s) 및 **numeric** (p,s) = p<br /><br /> **money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **bit** = 1<br /><br /> 기타 모든 유형 = 0|**ssNoversion**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**소수 자릿수**|숫자 기반 데이터 형식의 소수점 이하 자릿수<br /><br /> **decimal** (p,s) 및 **numeric** (p,s) = s<br /><br /> **money** 및 **smallmoney** = 4<br /><br /> **datetime** = 3<br /><br /> 기타 모든 유형 = 0|**ssNoversion**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**TotalBytes**|메타데이터 및 값의 모든 데이터를 저장하는 데 필요한 바이트 수입니다. 이 정보는 **sql_variant** 열의 데이터에 대한 최대치를 확인하는 데 유용합니다. 값이 900을 초과하면 인덱스를 만들 수 없습니다.|**ssNoversion**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**데이터 정렬**|특정 **sql_variant** 값의 데이터 정렬을 나타냅니다.|**sysname**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**MaxLength**|최대 데이터 형식 길이(바이트)입니다. 예를 들어 **nvarchar(** 50 **)** 의 **MaxLength**는 100이고, **int**의 **MaxLength**는 4입니다.|**ssNoversion**<br /><br /> NULL = 입력이 잘못되었습니다.|  
  
## <a name="return-types"></a>반환 형식  
 **sql_variant**  
  
## <a name="examples"></a>예  
### <a name="a-using-a-sqlvariant-in-a-table"></a>1\. 테이블에서 sql_variant 사용  
 다음 예에서는 `tableA`에 `sql_variant` 및 `colB` 형식의 `colA`가 있는 경우 `colB` =`1689`일 때 `colA` 값 `46279.1`에 대한 `SQL_VARIANT_PROPERTY` 정보를 검색합니다.  
  
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
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>2\. 변수로 sql_variant 사용   
 다음 예에서는 변수 @v1에 대한 `SQL_VARIANT_PROPERTY` 정보를 검색합니다.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>참고 항목  
 [sql_variant&#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  

