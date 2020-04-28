---
title: 추가 테이블 반환 매개 변수 메타 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), catalog functions to retrieve metadata
- table-valued parameters (ODBC), metadata
ms.assetid: 6c193188-5185-4373-9a0d-76cfc150c828
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b52f83e36c315ccd86d1516df9e11b913c80ba8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304541"
---
# <a name="additional-table-valued-parameter-metadata"></a>추가 테이블 반환 매개 변수 메타데이터
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  응용 프로그램은 테이블 반환 매개 변수에 대 한 메타 데이터를 검색 하기 위해 SQLProcedureColumns를 호출 합니다. 테이블 반환 매개 변수의 경우 SQLProcedureColumns는 단일 행을 반환 합니다. 테이블 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]매개 변수와 연결 된 테이블 형식에 대 한 스키마 및 카탈로그 정보를 제공 하기 위해 두 개의 추가 열 SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMA_NAME가 추가 되었습니다. ODBC 사양에 따라 SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMA_NAME은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 추가된 모든 드라이버별 열 앞에, 그리고 ODBC 자체에서 지정한 모든 열 뒤에 표시됩니다.  
  
 다음 표에서는 테이블 반환 매개 변수에서 중요한 열을 나열합니다.  
  
|열 이름|데이터 형식|값/설명|  
|-----------------|---------------|---------------------|  
|DATA_TYPE|NULL이 아닌 Smallint|SQL_SS_TABLE|  
|TYPE_NAME|NULL이 아닌 WVarchar(128)|테이블 반환 매개 변수의 형식 이름입니다.|  
|COLUMN_SIZE|정수|NULL|  
|BUFFER_LENGTH|정수|0|  
|DECIMAL_DIGITS|Smallint|NULL|  
|NUM_PREC_RADIX|Smallint|NULL|  
|NULLABLE|NULL이 아닌 Smallint|SQL_NULLABLE|  
|REMARKS|Varchar|NULL|  
|COLUMN_DEF|WVarchar(4000)|NULL|  
|SQL_DATA_TYPE|NULL이 아닌 Smallint|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULL|  
|CHAR_OCTET_LENGTH|정수|NULL|  
|ORDINAL_POSITION|NULL이 아닌 Integer|매개 변수의 서수 위치입니다.|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|NULL이 아닌 WVarchar(128)|테이블 반환 매개 변수의 테이블 형식에 대한 형식 정의를 포함하는 카탈로그입니다.|  
|SS_TYPE_SCHEMA_NAME|NULL이 아닌 WVarchar(128)|테이블 반환 매개 변수의 테이블 형식에 대한 형식 정의를 포함하는 스키마입니다.|  
  
 WVarchar 열은 ODBC 사양에 Varchar로 정의되어 있지만 실제로는 최근의 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버에서 WVarchar로 반환됩니다. 이러한 변경 내용은 ODBC 3.5 사양에 유니코드 지원이 추가될 때 적용되었지만 명시적으로 발표되지는 않았습니다.  
  
 응용 프로그램은 테이블 반환 매개 변수에 대 한 추가 메타 데이터를 가져오기 위해 SQLColumns 및 SQLPrimaryKeys 카탈로그 함수를 사용 합니다. 이러한 함수를 호출하여 테이블 반환 매개 변수를 얻으려면 애플리케이션에서 문 특성 SQL_SOPT_SS_NAME_SCOPE를 SQL_SS_NAME_SCOPE_TABLE_TYPE으로 설정해야 합니다. 이 값은 애플리케이션에서 실제 테이블이 아니라 테이블 형식의 메타데이터를 요구한다는 것을 나타냅니다. 그런 다음 응용 프로그램은 테이블 반환 매개 변수의 TYPE_NAME를 *TableName* 매개 변수로 전달 합니다. SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMA_NAME는 각각 *CatalogName* 및 *SchemaName* 매개 변수와 함께 사용 되어 테이블 반환 매개 변수의 카탈로그와 스키마를 식별 합니다. 애플리케이션이 테이블 반환 매개 변수의 메타데이터 검색을 마치면 SQL_SOPT_SS_NAME_SCOPE가 기본값인 SQL_SS_NAME_SCOPE_TABLE로 다시 설정됩니다.  
  
 SQL_SOPT_SS_NAME_SCOPE가 SQL_SS_NAME_SCOPE_TABLE로 설정되면 연결된 서버에 대한 쿼리가 실패합니다. 서버 구성 요소를 포함 하는 카탈로그를 사용 하 여 SQLColumns 또는 Sqlprimarykey를 호출 하면 실패 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 반환 매개 변수](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
