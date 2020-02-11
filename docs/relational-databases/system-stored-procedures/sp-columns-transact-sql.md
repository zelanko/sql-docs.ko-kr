---
title: sp_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_TSQL
- sp_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns
ms.assetid: 2dec79cf-2baf-4c0f-8cbb-afb1a8654e1e
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8eb18a81ff7910418e5b3c8a3b36a0e4cd94cc36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070350"
---
# <a name="sp_columns-transact-sql"></a>sp_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 환경에서 쿼리할 수 있는 지정된 개체에 대한 열 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_columns [ @table_name = ] object  
     [ , [ @table_owner = ] owner ]   
     [ , [ @table_qualifier = ] qualifier ]   
     [ , [ @column_name = ] column ]   
     [ , [ @ODBCVer = ] ODBCVer ]  
```  
  
## <a name="arguments"></a>인수  
`[ \@table_name = ] object`카탈로그 정보를 반환 하는 데 사용 되는 개체의 이름입니다. *개체* 는 테이블 반환 함수 등의 열을 포함 하는 테이블, 뷰 또는 기타 개체 일 수 있습니다. *개체* 는 **nvarchar (384)** 이며 기본값은 없습니다. 와일드카드 패턴 일치가 지원됩니다.  
  
`[ \@table_owner = ] owner`카탈로그 정보를 반환 하는 데 사용 되는 개체의 개체 소유자입니다. *owner* 는 **nvarchar (384)** 이며 기본값은 NULL입니다. 와일드카드 패턴 일치가 지원됩니다. *Owner* 를 지정 하지 않은 경우 기본 DBMS의 기본 개체 표시 규칙이 적용 됩니다.  
  
 현재 사용자가 지정된 이름의 개체를 소유한 경우 해당 개체의 열이 반환됩니다. *Owner* 를 지정 하지 않고 현재 사용자가 지정 된 *개체*의 개체를 소유 하 고 있지 않은 경우 **sp_columns** 는 데이터베이스 소유자가 소유한 지정 된 *개체* 를 사용 하 여 개체를 찾습니다. 개체가 있으면 개체의 열이 반환됩니다.  
  
`[ \@table_qualifier = ] qualifier`개체 한정자의 이름입니다. *한정자* 는 **sysname**이며 기본값은 NULL입니다. 다양 한 DBMS 제품에서 개체 (_한정자_)에 대해 세 부분으로 구성 되는 이름을 지원**합니다.** _소유자_**.** _이름_). 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 개체 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
`[ \@column_name = ] column`단일 열 이며 카탈로그 정보의 열이 한 개만 필요한 경우에 사용 됩니다. *열* 은 **nvarchar (384)** 이며 기본값은 NULL입니다. *열* 을 지정 하지 않으면 모든 열이 반환 됩니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *열* 은 **syscolumns** 테이블에 나열 된 열 이름을 나타냅니다. 와일드카드 패턴 일치가 지원됩니다. 상호 운용성을 극대화하려면 게이트웨이 클라이언트가 SQL-92 표준 패턴 일치(% 및 _ 와일드카드 문자)만을 사용해야 합니다.  
  
`[ \@ODBCVer = ] ODBCVer`사용 중인 ODBC의 버전입니다. *ODBCVer* 는 **int**이며 기본값은 2입니다. 이 값은 ODBC 버전 2를 나타내며 유효한 값은 2 또는 3입니다. 버전 2와 3의 동작 차이에 대 한 자세한 내용은 ODBC **Sqlcolumns** 사양을 참조 하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
 **Sp_columns** 카탈로그 저장 프로시저는 ODBC의 **sqlcolumns** 와 동일 합니다. 반환 되는 결과는 **TABLE_QUALIFIER**, **TABLE_OWNER**및 **TABLE_NAME**순으로 정렬 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|개체 한정자 이름입니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_OWNER**|**sysname**|개체 소유자 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|개체 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**COLUMN_NAME**|**sysname**|반환 된 **TABLE_NAME** 의 각 열에 대 한 열 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**DATA_TYPE**|**smallint**|ODBC 데이터 형식을 나타내는 정수 코드입니다. ODBC 형식에 매핑될 수 없는 데이터 형식인 경우에는 NULL이 됩니다. Native data 형식 이름은 **TYPE_NAME** 열에 반환 됩니다.|  
|**TYPE_NAME**|**sysname**|데이터 형식을 나타내는 문자열입니다. 이 이름은 기본 DBMS에서 제공합니다.|  
|**소수**|**int**|유효 자릿수입니다. **전체 자릿수** 열의 반환 값은 밑수 10에 있습니다.|  
|**길이**|**int**|데이터의 전송 크기입니다. <sup>1</sup>|  
|**배율을**|**smallint**|소수점 오른쪽 자릿수입니다.|  
|**RADIX**|**smallint**|숫자 데이터 형식의 기수입니다.|  
|**않는**|**smallint**|NULL 허용 여부를 지정합니다.<br /><br /> 1 = NULL을 사용할 수 있습니다.<br /><br /> 0 = NULL을 사용할 수 없습니다.|  
|**설명**|**varchar (254)**|이 필드는 항상 NULL을 반환합니다.|  
|**COLUMN_DEF**|**nvarchar(4000)**|열의 기본값입니다.|  
|**SQL_DATA_TYPE**|**smallint**|설명자의 TYPE 필드에 표시되는 SQL 데이터 형식의 값입니다. 이 열은 **datetime** 및 SQL-92 **interval** 데이터 형식을 제외 하 고 **DATA_TYPE** 열과 동일 합니다. 이 열은 항상 값을 반환합니다.|  
|**SQL_DATETIME_SUB**|**smallint**|**Datetime** 및 SQL-92 **interval** 데이터 형식에 대 한 하위 형식 코드입니다. 이 열은 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHAR_OCTET_LENGTH**|**int**|문자 또는 정수 데이터 형식 열의 최대 길이를 바이트로 표시한 것입니다. 이 열은 다른 모든 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**ORDINAL_POSITION**|**int**|개체에 있는 열의 서수 위치입니다. 개체의 첫 번째 열은 1입니다. 이 열은 항상 값을 반환합니다.|  
|**IS_NULLABLE**|**varchar (254)**|개체에 있는 열의 null 허용 여부입니다. ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS에서는 빈 문자열을 반환할 수 없습니다.<br /><br /> YES = 열이 NULL을 포함할 수 있습니다.<br /><br /> NO = 열이 NULL을 포함할 수 없습니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> 이 열에 대해 반환 되는 값은 **NULLABLE** 열에 대해 반환 되는 값과 다릅니다.|  
|**SS_DATA_TYPE**|**tinyint**|확장 저장 프로시저에 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.|  
  
 <sup>1</sup> 자세한 내용은 Microsoft ODBC 설명서를 참조 하십시오.  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대 한 SELECT 및 VIEW DEFINITION 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 **sp_columns** 구분 식별자에 대 한 요구 사항을 따릅니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정된 테이블의 열 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 지정된 테이블의 열 정보를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_tables &#40;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [Transact-sql&#41;카탈로그 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


