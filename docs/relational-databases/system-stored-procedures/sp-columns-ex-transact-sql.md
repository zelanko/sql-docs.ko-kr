---
description: sp_columns_ex(Transact-SQL)
title: sp_columns_ex (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_ex
- sp_columns_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns_ex
ms.assetid: c12ef6df-58c6-4391-bbbf-683ea874bd81
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b1a185ef8fe998a614de8ca56451966894a461f4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549954"
---
# <a name="sp_columns_ex-transact-sql"></a>sp_columns_ex(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정한 연결된 서버 테이블에 대해 각 열마다 한 행씩 열 정보를 반환합니다. *열* 이 지정 된 경우 **sp_columns_ex** 는 특정 열에 대해서만 열 정보를 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_columns_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @table_server = ] 'table_server'` 열 정보를 반환할 연결 된 서버의 이름입니다. *table_server* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @table_name = ] 'table_name'` 열 정보를 반환할 테이블의 이름입니다. *table_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_schema = ] 'table_schema'` 열 정보를 반환할 테이블의 스키마 이름입니다. *table_schema* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_catalog = ] 'table_catalog'` 열 정보를 반환할 테이블의 카탈로그 이름입니다. *table_catalog* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @column_name = ] 'column'` 정보를 제공 하는 데이터베이스 열의 이름입니다. *열* 은 **sysname**이며 기본값은 NULL입니다.  
  
`[ @ODBCVer = ] 'ODBCVer'` 사용 중인 ODBC의 버전입니다. *ODBCVer* 는 **int**이며 기본값은 2입니다. 이 값은 ODBC 버전 2를 나타내며 유효한 값은 2 또는 3입니다. 버전 2와 버전 3의 동작 차이에 대한 자세한 내용은 ODBC SQLColumns 사양을 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|테이블 또는 뷰 한정자 이름입니다. 다양 한 DBMS 제품에서 테이블에 대해 세 부분으로 구성 되는 이름 (_한정자_)을 지원**합니다.** _소유자_**.** _이름_). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_SCHEM**|**sysname**|테이블 또는 뷰 소유자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 테이블을 만든 데이터베이스 사용자의 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|테이블 또는 뷰 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**COLUMN_NAME**|**sysname**|반환 된 **TABLE_NAME** 의 각 열에 대 한 열 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**DATA_TYPE**|**smallint**|ODBC 형식 식별자에 해당하는 정수 값입니다. ODBC 형식에 매핑될 수 없는 데이터 형식인 경우에 이 값은 NULL이 됩니다. Native data 형식 이름은 **TYPE_NAME** 열에 반환 됩니다.|  
|**TYPE_NAME**|**varchar (** 13 **)**|데이터 형식을 나타내는 문자열입니다. 이 이름은 기본 DBMS에서 제공합니다.|  
|**COLUMN_SIZE**|**int**|유효 자릿수입니다. **전체 자릿수** 열의 반환 값은 밑수 10에 있습니다.|  
|**BUFFER_LENGTH**|**int**|데이터의 전송 크기입니다.1|  
|**DECIMAL_DIGITS**|**smallint**|소수점 오른쪽 자릿수입니다.|  
|**NUM_PREC_RADIX**|**smallint**|숫자 데이터 형식의 기준입니다.|  
|**않는**|**smallint**|NULL 허용 여부를 지정합니다.<br /><br /> 1 = NULL을 사용할 수 있습니다.<br /><br /> 0 = NULL을 사용할 수 없습니다.|  
|**설명**|**varchar (** 254 **)**|이 필드는 항상 NULL을 반환합니다.|  
|**COLUMN_DEF**|**varchar (** 254 **)**|열의 기본값입니다.|  
|**SQL_DATA_TYPE**|**smallint**|설명자의 TYPE 필드에 표시되는 SQL 데이터 형식의 값입니다. 이 열은 **datetime** 및 SQL-92 **interval** 데이터 형식을 제외 하 고 **DATA_TYPE** 열과 동일 합니다. 이 열은 항상 값을 반환합니다.|  
|**SQL_DATETIME_SUB**|**smallint**|**Datetime** 및 SQL-92 **interval** 데이터 형식에 대 한 하위 형식 코드입니다. 이 열은 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHAR_OCTET_LENGTH**|**int**|문자 또는 정수 데이터 형식 열의 최대 길이를 바이트로 표시한 것입니다. 이 열은 다른 모든 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**ORDINAL_POSITION**|**int**|테이블에 있는 열의 순서 위치입니다. 테이블의 첫 번째 열은 1입니다. 이 열은 항상 값을 반환합니다.|  
|**IS_NULLABLE**|**varchar (** 254 **)**|테이블에 있는 열의 Null 허용 여부입니다. ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS에서는 빈 문자열을 반환할 수 없습니다.<br /><br /> YES = 열이 NULL을 포함할 수 있습니다.<br /><br /> NO = 열이 NULL을 포함할 수 없습니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> 이 열에 대해 반환 되는 값은 **NULLABLE** 열에 대해 반환 되는 값과 다릅니다.|  
|**SS_DATA_TYPE**|**tinyint**|확장 저장 프로시저에 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.|  
  
 자세한 내용은 Microsoft ODBC 설명서를 참조하십시오.  
  
## <a name="remarks"></a>설명  
 **sp_columns_ex** 는 *table_server*에 해당 하는 OLE DB 공급자의 **IDBSchemaRowset** 인터페이스의 columns 행 집합을 쿼리하여 실행 됩니다. *Table_name*, *table_schema*, *table_catalog*및 *열* 매개 변수는 반환 되는 행을 제한 하기 위해이 인터페이스에 전달 됩니다.  
  
 지정한 연결 된 서버의 OLE DB 공급자가 **IDBSchemaRowset** 인터페이스의 columns 행 집합을 지원 하지 않는 경우 빈 결과 집합을 반환 합니다. **sp_columns_ex**  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 **sp_columns_ex** 구분 식별자에 대 한 요구 사항을 따릅니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 연결된 서버 `JobTitle`의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 `HumanResources.Employee` 테이블의 `Seattle1` 열에 대한 데이터 형식을 반환합니다.  
  
```  
EXEC sp_columns_ex 'Seattle1',   
   'Employee',   
   'HumanResources',   
   'AdventureWorks2012',   
   'JobTitle';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_catalogs &#40;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [Transact-sql&#41;sp_foreignkeys &#40;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [Transact-sql&#41;sp_indexes &#40;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [Transact-sql&#41;sp_primarykeys &#40;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [Transact-sql&#41;sp_tables_ex &#40;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [Transact-sql&#41;sp_table_privileges &#40;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
