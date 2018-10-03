---
title: sp_columns (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c768b2d64c38fdda66d6abeea0aef2010b4dfe35
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653002"
---
# <a name="spcolumns-transact-sql"></a>sp_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 환경에서 쿼리할 수 있는 지정된 개체에 대한 열 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@table_name=**] *object*  
 카탈로그 정보를 반환하는 데 사용되는 개체의 이름입니다. *개체* 테이블, 뷰 또는 테이블 반환 함수 같은 열이 있는 다른 개체 일 수 있습니다. *개체* 됩니다 **nvarchar(384)**, 기본값은 없습니다. 와일드카드 패턴 일치가 지원됩니다.  
  
 [  **@table_owner* * * =**] *소유자*  
 카탈로그 정보를 반환하는 데 사용되는 개체의 개체 소유자입니다. *소유자* 됩니다 **nvarchar(384)**, 기본값은 NULL입니다. 와일드카드 패턴 일치가 지원됩니다. 하는 경우 *소유자* 지정 하지 않으면 기본 DBMS의 기본 개체 표시 규칙이 적용 됩니다.  
  
 현재 사용자가 지정된 이름의 개체를 소유한 경우 해당 개체의 열이 반환됩니다. 하는 경우 *소유자* 지정 하지 않으면 현재 사용자 지정 된 개체를 소유 하지 않는 한 *개체*합니다 **sp_columns** 지정 된 개체를 찾습니다  *개체* 데이터베이스 소유자가 소유 합니다. 개체가 있으면 개체의 열이 반환됩니다.  
  
 [ **@table_qualifier****=**] *qualifier*  
 개체 한정자의 이름입니다. *한정자* 됩니다 **sysname**, 기본값은 NULL입니다. 다양 한 DBMS 제품에서는 세 부분으로 구성 된 개체에 대 한 이름 (*한정자 ***.*** 소유자 ***.*** 이름*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 개체 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
 [  **@column_name=**] *열*  
 카탈로그 정보 중 한 열만을 사용하고자 할 때 지정하는 단일 열입니다. *열* 됩니다 **nvarchar(384)**, 기본값은 NULL입니다. 하는 경우 *열* 은 지정 하지 않으면 모든 열 반환 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *열* 에 나열 된 열 이름을 나타냅니다 합니다 **syscolumns** 테이블입니다. 와일드카드 패턴 일치가 지원됩니다. 상호 운용성을 극대화하려면 게이트웨이 클라이언트가 SQL-92 표준 패턴 일치(% 및 _ 와일드카드 문자)만을 사용해야 합니다.  
  
 [ **@ODBCVer=**] *ODBCVer*  
 사용하고 있는 ODBC의 버전입니다. *ODBCVer* 됩니다 **int**, 기본값은 2입니다. 이 값은 ODBC 버전 2를 나타내며 유효한 값은 2 또는 3입니다. 버전 2와 3 간의 동작 차이점에 대 한 참조는 ODBC **SQLColumns** 사양입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
 합니다 **sp_columns** 카탈로그 저장 프로시저는 같음 **SQLColumns** ODBC에서. 반환 된 결과 정렬할 **TABLE_QUALIFIER**를 **TABLE_OWNER**, 및 **TABLE_NAME**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|개체 한정자 이름입니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_OWNER**|**sysname**|개체 소유자 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|개체 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**COLUMN_NAME**|**sysname**|각 열에 대 한 열 이름에는 **TABLE_NAME** 반환 합니다. 이 필드는 항상 값을 반환합니다.|  
|**DATA_TYPE**|**smallint**|ODBC 데이터 형식을 나타내는 정수 코드입니다. ODBC 형식에 매핑될 수 없는 데이터 형식인 경우에는 NULL이 됩니다. 네이티브 데이터 형식 이름을 반환 되는 **TYPE_NAME** 열입니다.|  
|**TYPE_NAME**|**sysname**|데이터 형식을 나타내는 문자열입니다. 이 이름은 기본 DBMS에서 제공합니다.|  
|**PRECISION**|**int**|유효 자릿수입니다. 반환 값을 **정밀도** 열은 10 진수로 합니다.|  
|**LENGTH**|**int**|데이터의 크기를 전송 합니다. <sup>1</sup>|  
|**크기 조정**|**smallint**|소수점 오른쪽 자릿수입니다.|  
|**기 수**|**smallint**|숫자 데이터 형식의 기수입니다.|  
|**NULLABLE**|**smallint**|NULL 허용 여부를 지정합니다.<br /><br /> 1 = NULL을 사용할 수 있습니다.<br /><br /> 0 = NULL을 사용할 수 없습니다.|  
|**설명**|**varchar(254)**|이 필드는 항상 NULL을 반환합니다.|  
|**COLUMN_DEF**|**nvarchar(4000)**|열의 기본값입니다.|  
|**SQL_DATA_TYPE**|**smallint**|설명자의 TYPE 필드에 표시되는 SQL 데이터 형식의 값입니다. 이 열은 동일 합니다 **DATA_TYPE** 열을 제외 하 고는 **datetime** 및 SQL-92 **간격** 데이터 형식입니다. 이 열은 항상 값을 반환합니다.|  
|**SQL_DATETIME_SUB**|**smallint**|하위 형식 코드입니다 **날짜/시간** 및 SQL-92 **간격** 데이터 형식입니다. 이 열은 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHAR_OCTET_LENGTH**|**int**|문자 또는 정수 데이터 형식 열의 최대 길이를 바이트로 표시한 것입니다. 이 열은 다른 모든 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**ORDINAL_POSITION**|**int**|개체에 있는 열의 서수 위치입니다. 개체의 첫 번째 열은 1입니다. 이 열은 항상 값을 반환합니다.|  
|**IS_NULLABLE**|**varchar(254)**|개체에 있는 열의 null 허용 여부입니다. ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS에서는 빈 문자열을 반환할 수 없습니다.<br /><br /> YES = 열이 NULL을 포함할 수 있습니다.<br /><br /> NO = 열이 NULL을 포함할 수 없습니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> 이 열에 대 한 반환 값과 다른 지에서에 대 한 값을 반환 합니다 **NULLABLE** 열입니다.|  
|**SS_DATA_TYPE**|**tinyint**|확장 저장 프로시저에 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.|  
  
 <sup>1</sup> 자세한 내용은 Microsoft ODBC 설명서를 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 스키마에서 SELECT 및 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
 **sp_columns** 구분된 식별자에 대 한 요구 사항을 따릅니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정된 테이블의 열 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 지정된 테이블의 열 정보를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [카탈로그 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


