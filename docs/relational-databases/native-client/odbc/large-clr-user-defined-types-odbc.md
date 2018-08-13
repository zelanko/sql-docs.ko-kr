---
title: 큰 CLR 사용자 정의 형식 (ODBC) | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, large user-defined types
- large user-defined types [ODBC]
ms.assetid: ddce337e-bb6e-4a30-b7cc-4969bb1520a9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ac70196d3b343a0f5a4fedbbedb2367a80665abb
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565797"
---
# <a name="large-clr-user-defined-types-odbc"></a>큰 CLR 사용자 정의 형식(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  이 항목에서는 큰 CLR(공용 언어 런타임) UDT(사용자 정의 형식)를 지원하기 위한 SQL Server Native Client의 ODBC 변경 내용에 대해 설명합니다.  
  
 큰 CLR Udt에 대 한 ODBC 지원을 보여 주는 샘플을 참조 하세요 [큰 Udt에 대 한 지원](../../../relational-databases/native-client-odbc-how-to/support-for-large-udts.md)합니다.  
  
 SQL Server Native Client의 큰 CLR Udt 지원에 대 한 자세한 내용은 참조 하세요. [Large CLR User-Defined 형식](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)합니다.  
  
## <a name="data-format"></a>데이터 형식  
 SQL Server Native Client는 SQL_SS_LENGTH_UNLIMITED를 사용하여 LOB(Large Object) 형식에 대해 8,000바이트 이상인 열의 크기를 나타냅니다. SQL Server 2008부터 크기가 8,000바이트보다 큰 CLR UDT에도 같은 값이 사용됩니다.  
  
 UDT 값은 바이트 배열로 나타납니다. 16진수 문자열로의 변환 및 그 반대의 변환이 지원됩니다. 리터럴 값은 접두사 "0x"를 사용하여 16진수 문자열로 나타납니다.  
  
 다음 표에서는 매개 변수 및 결과 집합의 데이터 형식 매핑을 보여 줍니다.  
  
|SQL Server 데이터 형식|SQL 데이터 형식|값|  
|--------------------------|-------------------|-----------|  
|CLR UDT|SQL_SS_UDT|-151(sqlncli.h)|  
  
 다음 표에서는 해당되는 구조 및 ODBC C 형식을 보여 줍니다. 기본적으로 CLR UDT를 **varbinary** 추가 메타 데이터를 사용 하 여 형식입니다.  
  
|SQL 데이터 형식|메모리 레이아웃|C 데이터 형식|값(sqlext.h)|  
|-------------------|-------------------|-----------------|------------------------|  
|SQL_SS_UDT|SQLCHAR * (unsigned char \*)|SQL_C_BINARY|SQL_BINARY (-2)|  
  
## <a name="descriptor-fields-for-parameters"></a>매개 변수의 설명자 필드  
 IPD 필드에 반환되는 정보는 다음과 같습니다.  
  
|설명자 필드|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|UDT가 포함된 카탈로그의 이름입니다.|UDT가 포함된 카탈로그의 이름입니다.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|UDT가 포함된 스키마의 이름입니다.|UDT가 포함된 스키마의 이름입니다.|  
|SQL_CA_SS_UDT_TYPE_NAME|UDT의 이름입니다.|UDT의 이름입니다.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|UDT의 정규화된 이름입니다.|UDT의 정규화된 이름입니다.|  
  
 UDT 매개 변수의 경우 SQL_CA_SS_UDT_TYPE_NAME 항상 설정 해야 통해 **SQLSetDescField**합니다. SQL_CA_SS_UDT_CATALOG_NAME 및 SQL_CA_SS_UDT_SCHEMA_NAME은 선택 사항입니다.  
  
 UDT가 테이블과 다른 스키마가 있는 동일한 데이터베이스에 정의되어 있으면 SQL_CA_SS_UDT_SCHEMA_NAME을 설정해야 합니다.  
  
 UDT가 테이블과 다른 데이터베이스에 정의되어 있으면 SQL_CA_SS_UDT_CATALOG_NAME 및 SQL_CA_SS_UDT_SCHEMA_NAME을 설정해야 합니다.  
  
 SQL_CA_SS_UDT_TYPE_NAME, SQL_CA_SS_UDT_CATALOG_NAME 또는 SQL_CA_SS_UDT_SCHEMA_NAME에 대한 설정에 오류나 누락이 있으면 SQLSTATE HY000 및 서버 관련 메시지 텍스트가 있는 진단 레코드가 생성됩니다.  
  
## <a name="descriptor-fields-for-results"></a>결과의 설명자 필드  
 IRD 필드에 반환되는 정보는 다음과 같습니다.  
  
|설명자 필드|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_DISPLAY_SIZE|2*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LITERAL_PREFIX|"0x"|"0x"|  
|SQL_DESC_LITERAL_SUFFIX|""|""|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|SQL_PRED_NONE|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|UDT가 포함된 카탈로그의 이름입니다.|UDT가 포함된 카탈로그의 이름입니다.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|UDT가 포함된 스키마의 이름입니다.|UDT가 포함된 스키마의 이름입니다.|  
|SQL_CA_SS_UDT_TYPE_NAME|UDT의 이름입니다.|UDT의 이름입니다.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|UDT의 정규화된 이름입니다.|UDT의 정규화된 이름입니다.|  
  
## <a name="column-metadata-returned-by-sqlcolumns-and-sqlprocedurecolumns-catalog-metadata"></a>SQLColumns 및 SQLProcedureColumns가 반환하는 열 메타데이터(카탈로그 메타데이터)  
 UDT에 대해 다음 열 값이 반환됩니다.  
  
|열 이름|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|  
|-----------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|TYPE_NAME|UDT의 이름입니다.|UDT의 이름입니다.|  
|COLUMN_SIZE|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|BUFFER_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|DECIMAL_DIGITS|NULL|NULL|  
|SQL_DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DATETIME_SUB|NULL|NULL|  
|CHAR_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SS_UDT_CATALOG_NAME|UDT가 포함된 카탈로그의 이름입니다.|UDT가 포함된 카탈로그의 이름입니다.|  
|SS_UDT_SCHEMA_NAME|UDT가 포함된 스키마의 이름입니다.|UDT가 포함된 스키마의 이름입니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT의 정규화된 이름입니다.|UDT의 정규화된 이름입니다.|  
  
 마지막 세 개의 열은 드라이버 관련 열입니다. SQLColumns SQLProcedureColumns의 결과 집합의 모든 기존 드라이버별 열 앞 있지만 모든 ODBC 정의 열 이후 추가 됩니다.  
  
 개별 Udt 또는 일반 유형 "udt"에 대 한 SQLGetTypeInfo에서 아무 행도 반환 합니다.  
  
## <a name="bindings-and-conversions"></a>바인딩 및 변환  
 SQL에서 C 데이터 형식으로 지원되는 변환은 다음과 같습니다.  
  
|변환 원본 및 대상|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|지원 *|  
|SQL_C_BINARY|지원됨|  
|SQL_C_CHAR|지원 *|  
  
 \* 이진 데이터가 16 진수 문자열로 변환 됩니다.  
  
 C에서 SQL 데이터 형식으로 지원되는 변환은 다음과 같습니다.  
  
|변환 원본 및 대상|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|지원 *|  
|SQL_C_BINARY|지원됨|  
|SQL_C_CHAR|지원 *|  
  
 \* 16 진수 문자열에서 이진 데이터 변환이 발생합니다.  
  
## <a name="sqlvariant-support-for-udts"></a>UDT에 대한 SQL_VARIANT 지원  
 UDT는 SQL_VARIANT 열에서 지원되지 않습니다.  
  
## <a name="bcp-support-for-udts"></a>UDT에 대한 BCP 지원  
 UDT 값은 문자나 이진 값으로만 가져오고 내보낼 수 있습니다.  
  
## <a name="downlevel-client-behavior-for-udts"></a>UDT에 대한 하위 수준 클라이언트 동작  
 UDT에 적용되는 하위 수준 클라이언트와의 유형 매핑은 다음과 같습니다.  
  
|서버 버전|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|  
|--------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL Server 2005|**UDT**|**varbinary(max)**|  
|SQL Server 2008 이상|**UDT**|**UDT**|  
  
## <a name="odbc-functions-supporting-large-clr-udts"></a>큰 CLR UDT를 지원하는 ODBC 함수  
 이 섹션에서는 큰 CLR UDT를 지원하는 SQL Server Native Client ODBC 함수의 변경 내용에 대해 설명합니다.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 UDT 결과 열 값은 이 항목의 앞부분에 있는 "바인딩 및 변환" 섹션에서 설명한 것처럼 SQL에서 C 데이터 형식으로 변환됩니다.  
  
### <a name="sqlbindparameter"></a>SQLBindParameter  
 UDT에 필요한 값은 다음과 같습니다.  
  
|SQL 데이터 형식|*Parametertype*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|---------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 UDT에 대해 반환되는 값은 이 항목의 앞부분에 있는 "결과의 설명자 필드" 섹션에 설명되어 있습니다.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 UDT에 대해 반환되는 값은 이 항목의 앞부분에 있는 "SQLColumns 및 SQLProcedureColumns가 반환하는 열 메타데이터(카탈로그 메타데이터)" 섹션에 설명되어 있습니다.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 UDT에 대해 반환되는 값은 다음과 같습니다.  
  
|SQL 데이터 형식|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqldescribeparam"></a>SQLDescribeParam  
 UDT에 대해 반환되는 값은 다음과 같습니다.  
  
|SQL 데이터 형식|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlfetch"></a>SQLFetch  
 UDT 결과 열 값은 이 항목의 앞부분에 있는 "바인딩 및 변환" 섹션에서 설명한 것처럼 SQL에서 C 데이터 형식으로 변환됩니다.  
  
### <a name="sqlfetchscroll"></a>SQLFetchScroll  
 UDT 결과 열 값은 이 항목의 앞부분에 있는 "바인딩 및 변환" 섹션에서 설명한 것처럼 SQL에서 C 데이터 형식으로 변환됩니다.  
  
### <a name="sqlgetdata"></a>SQLGetData  
 UDT 결과 열 값은 이 항목의 앞부분에 있는 "바인딩 및 변환" 섹션에서 설명한 것처럼 SQL에서 C 데이터 형식으로 변환됩니다.  
  
### <a name="sqlgetdescfield"></a>SQLGetDescField  
 새 형식과 함께 사용할 수 있는 설명자 필드는 이 항목의 앞부분에 있는 "매개 변수의 설명자 필드" 및 "결과의 설명자 필드" 섹션에 설명되어 있습니다.  
  
### <a name="sqlgetdescrec"></a>SQLGetDescRec  
 UDT에 대해 반환되는 값은 다음과 같습니다.  
  
|SQL 데이터 형식|형식|하위 유형|길이|전체 자릿수|소수 자릿수|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT|0|*n*|n|0|  
|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 UDT에 대해 반환되는 값은 이 항목의 앞부분에 있는 "SQLColumns 및 SQLProcedureColumns가 반환하는 열 메타데이터(카탈로그 메타데이터)" 섹션에 설명되어 있습니다.  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 UDT에 대해 반환되는 값은 이 항목의 앞부분에 있는 "SQLColumns 및 SQLProcedureColumns가 반환하는 열 메타데이터(카탈로그 메타데이터)" 섹션에 설명되어 있습니다.  
  
### <a name="sqlputdata"></a>SQLPutData  
 UDT 매개 변수 값은 이 항목의 앞부분에 있는 "바인딩 및 변환" 섹션에서 설명한 것처럼 C에서 SQL 데이터 형식으로 변환됩니다.  
  
### <a name="sqlsetdescfield"></a>SQLSetDescField  
 새 형식과 함께 사용할 수 있는 설명자 필드는 이 항목의 앞부분에 있는 "매개 변수의 설명자 필드" 및 "결과의 설명자 필드" 섹션에 설명되어 있습니다.  
  
### <a name="sqlsetdescrec"></a>SQLSetDescRec  
 UDT에 허용되는 값은 다음과 같습니다.  
  
|SQL 데이터 형식|형식|하위 유형|길이|전체 자릿수|소수 자릿수|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (8,000바이트 이하 길이)|SQL_SS_UDT|0|*n*|*n*|0|  
|SQL_SS_UDT<br /><br /> (8,000바이트를 초과하는 길이)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlspecialcolumns"></a>SQLSpecialColumns  
 DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH 및 DECIMAL_DIGTS UDT 열에 대해 반환되는 값은 이 항목의 앞부분에 있는 "SQLColumns 및 SQLProcedureColumns가 반환하는 열 메타데이터(카탈로그 메타데이터)" 섹션에 설명되어 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [큰 CLR 사용자 정의 형식](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
  
  
