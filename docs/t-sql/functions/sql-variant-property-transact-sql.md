---
title: SQL_VARIANT_PROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: bd9b181c04a96ee90b0bbb54546a1d925761224f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/13/2017

---
# <a name="sqlvariantproperty-transact-sql"></a>SQL_VARIANT_PROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  에 대 한 기본 데이터 형식 및 기타 정보가 반환는 **sql_variant** 값입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 형식의 식 **sql_variant**합니다.  
  
 *속성*  
 이름을 포함 된 **sql_variant** 정보 제공 해야 하는 속성입니다. *속성* 은 **varchar (**128**)**, 이며 다음 값 중 하나를 사용할 수 있습니다.  
  
|값|Description|반환된 sql_variant의 기본 형식|  
|-----------|-----------------|----------------------------------------|  
|**BaseType**|다음과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식<br /><br /> **bigint**<br /><br /> **binary**<br /><br /> **char**<br /><br /> **date**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **int**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **smallint**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**정밀도**|숫자 기본 데이터 형식의 전체 자릿수<br /><br /> **날짜/시간** = 23<br /><br /> **smalldatetime** = 16<br /><br /> **float** = 53<br /><br /> **실제** = 24<br /><br /> **10 진수** (p, s) 및 **숫자** (p, s) = p<br /><br /> **money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **비트** = 1<br /><br /> 기타 모든 유형 = 0|**int**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**소수 자릿수**|숫자 기반 데이터 형식의 소수점 이하 자릿수<br /><br /> **10 진수** (p, s) 및 **숫자** (p, s) = s<br /><br /> **money** 및 **smallmoney** = 4<br /><br /> **날짜/시간** = 3<br /><br /> 기타 모든 유형 = 0|**int**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**TotalBytes**|메타데이터 및 값의 모든 데이터를 저장하는 데 필요한 바이트 수입니다. 이 정보 데이터에 대 한 최대치를 확인 하는 중에 유용 하다는 **sql_variant** 열입니다. 값이 900 보다 크면 인덱스 생성이 실패 합니다.|**int**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**데이터 정렬**|특정 데이터 정렬을 나타내는 **sql_variant** 값입니다.|**sysname**<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**MaxLength**|최대 데이터 형식 길이(바이트)입니다. 예를 들어 **MaxLength** 의 **nvarchar (**50**)** 는 100, **MaxLength** 의 **int** 은 4입니다.|**int**<br /><br /> NULL = 입력이 잘못되었습니다.|  
  
## <a name="return-types"></a>반환 형식  
 **sql_variant**  
  
## <a name="examples"></a>예  
### <a name="a-using-a-sqlvariant-in-a-table"></a>1. 테이블에서 sql_variant 사용  
 다음 예제에서는 검색 `SQL_VARIANT_PROPERTY` 에 대 한 정보는 `colA` 값 `46279.1` 여기서 `colB`  = `1689`있다고 가정, `tableA` 가 `colA` 형식의 `sql_variant` 및 `colB`.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]다음 세 값 중 각는 **sql_variant**합니다.  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>2. 변수는 sql_variant를 사용 하 여   
 다음 예제에서는 검색 `SQL_VARIANT_PROPERTY` 라는 변수에 대 한 정보 @v1합니다.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sql_variant&#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  


