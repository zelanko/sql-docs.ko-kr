---
title: sp_columns_ex (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aaf644b6a8795e9c68e0053eaed0023c4b9299b6
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588407"
---
# <a name="spcolumnsex-transact-sql"></a>sp_columns_ex(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 연결된 서버 테이블에 대해 각 열마다 한 행씩 열 정보를 반환합니다. **sp_columns_ex** 경우에 특정 열에 대 한 열 정보를 반환 *열* 지정 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@table_server =** ] **'**_table_server_**'**  
 열 정보를 반환할 연결된 서버의 이름입니다. *table_server* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@table_name =** ] **'**_table_name_**'**  
 열 정보를 반환할 대상이 되는 테이블의 이름입니다. *table_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@table_schema =** ] **'**_table_schema_**'**  
 열 정보를 반환할 대상이 되는 테이블의 스키마 이름입니다. *table_schema* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@table_catalog =** ] **'**_table_catalog_**'**  
 열 정보를 반환할 대상이 되는 테이블의 카탈로그 이름입니다. *table_catalog* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@column_name =** ] **'**_열_**'**  
 정보를 제공할 대상이 되는 데이터베이스 열의 이름입니다. *열* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@ODBCVer =** ] **'**_ODBCVer_**'**  
 사용하고 있는 ODBC의 버전입니다. *ODBCVer* 됩니다 **int**, 기본값은 2입니다. 이 값은 ODBC 버전 2를 나타내며 유효한 값은 2 또는 3입니다. 버전 2와 버전 3의 동작 차이에 대한 자세한 내용은 ODBC SQLColumns 사양을 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|테이블 또는 뷰 한정자 이름입니다. 다양 한 DBMS 제품에서는 테이블에 대해 세 부분으로 이루어진 이름 (_한정자_**.** _소유자_**.** _이름을_). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_SCHEM 순**|**sysname**|테이블 또는 뷰 소유자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 테이블을 만든 데이터베이스 사용자의 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|테이블 또는 뷰 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**COLUMN_NAME**|**sysname**|각 열에 대 한 열 이름에는 **TABLE_NAME** 반환 합니다. 이 필드는 항상 값을 반환합니다.|  
|**DATA_TYPE**|**smallint**|ODBC 형식 식별자에 해당하는 정수 값입니다. ODBC 형식에 매핑될 수 없는 데이터 형식인 경우에 이 값은 NULL이 됩니다. 네이티브 데이터 형식 이름을 반환 되는 **TYPE_NAME** 열입니다.|  
|**TYPE_NAME**|**varchar (** 13 **)**|데이터 형식을 나타내는 문자열입니다. 이 이름은 기본 DBMS에서 제공합니다.|  
|**COLUMN_SIZE**|**int**|유효 자릿수입니다. 반환 값을 **정밀도** 열은 10 진수로 합니다.|  
|**BUFFER_LENGTH**|**int**|데이터의 전송 크기입니다.1|  
|**DECIMAL_DIGITS**|**smallint**|소수점 오른쪽 자릿수입니다.|  
|**NUM_PREC_RADIX**|**smallint**|숫자 데이터 형식의 기준입니다.|  
|**NULLABLE**|**smallint**|NULL 허용 여부를 지정합니다.<br /><br /> 1 = NULL을 사용할 수 있습니다.<br /><br /> 0 = NULL을 사용할 수 없습니다.|  
|**설명**|**varchar (** 254 **)**|이 필드는 항상 NULL을 반환합니다.|  
|**COLUMN_DEF**|**varchar (** 254 **)**|열의 기본값입니다.|  
|**SQL_DATA_TYPE**|**smallint**|설명자의 TYPE 필드에 표시되는 SQL 데이터 형식의 값입니다. 이 열은 동일 합니다 **DATA_TYPE** 열을 제외 하 고는 **datetime** 및 SQL-92 **간격** 데이터 형식입니다. 이 열은 항상 값을 반환합니다.|  
|**SQL_DATETIME_SUB**|**smallint**|하위 형식 코드입니다 **날짜/시간** 및 SQL-92 **간격** 데이터 형식입니다. 이 열은 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHAR_OCTET_LENGTH**|**int**|문자 또는 정수 데이터 형식 열의 최대 길이를 바이트로 표시한 것입니다. 이 열은 다른 모든 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**ORDINAL_POSITION**|**int**|테이블에 있는 열의 순서 위치입니다. 테이블의 첫 번째 열은 1입니다. 이 열은 항상 값을 반환합니다.|  
|**IS_NULLABLE**|**varchar (** 254 **)**|테이블에 있는 열의 Null 허용 여부입니다. ISO 규칙을 따라서 null 허용 여부를 결정합니다. ISO SQL-호환 DBMS에서는 빈 문자열을 반환할 수 없습니다.<br /><br /> YES = 열이 NULL을 포함할 수 있습니다.<br /><br /> NO = 열이 NULL을 포함할 수 없습니다.<br /><br /> Null 허용 여부를 알 수 없으면 이 열에서는 길이가 0인 문자열을 반환합니다.<br /><br /> 이 열에 대 한 반환 값과 다른 지에서에 대 한 값을 반환 합니다 **NULLABLE** 열입니다.|  
|**SS_DATA_TYPE**|**tinyint**|확장 저장 프로시저에 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.|  
  
 자세한 내용은 Microsoft ODBC 설명서를 참조하십시오.  
  
## <a name="remarks"></a>Remarks  
 **sp_columns_ex** 의 COLUMNS 행 집합을 쿼리하여 실행 되는 **IDBSchemaRowset** 에 해당 하는 OLE DB 공급자의 인터페이스 *table_server*합니다. 합니다 *table_name*를 *table_schema*를 *table_catalog*, 및 *열* 매개 변수는 행을 제한 하려면이 인터페이스에 전달 됩니다 반환 됩니다.  
  
 **sp_columns_ex** 지정 된 연결 된 서버의 OLE DB 공급자의 COLUMNS 행 집합을 지원 하지 않는 경우 설정 하는 빈 결과 반환 합니다 **IDBSchemaRowset** 인터페이스입니다.  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
 **sp_columns_ex** 구분된 식별자에 대 한 요구 사항을 따릅니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 연결된 서버 `JobTitle`의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 `HumanResources.Employee` 테이블의 `Seattle1` 열에 대한 데이터 형식을 반환합니다.  
  
```  
EXEC sp_columns_ex 'Seattle1',   
   'Employee',   
   'HumanResources',   
   'AdventureWorks2012',   
   'JobTitle';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_foreignkeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
