---
description: SQLColAttribute
title: SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColAttribute function
ms.assetid: a5387d9e-a243-4cfe-b786-7fad5842b1d6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2d1ef030815e701f0b1b7cdeac02c4827641ff2
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809892"
---
# <a name="sqlcolattribute"></a>SQLColAttribute
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **Sqlcolattribute** 를 사용 하 여 준비 또는 실행 된 ODBC 문에 대 한 결과 집합 열의 특성을 검색할 수 있습니다. 준비 된 문에 대해 **Sqlcolattribute** 를 호출 하면로 왕복이 발생 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 문 실행의 일부로 결과 집합 열 데이터를 받으므로 **sqlexecute** 또는 **sqlcolattribute** 가 완료 된 후 **sqlcolattribute** 를 호출 하면 서버 왕복이 포함 되지 않습니다.  
  
> [!NOTE]  
>  일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 결과 집합에는 ODBC 열 식별자 특성을 사용할 수 없습니다.  
  
|필드 식별자|Description|  
|----------------------|-----------------|  
|SQL_COLUMN_TABLE_NAME|서버 커서를 생성하는 문에서 검색된 결과 집합 또는 FOR BROWSE 절을 포함하는 실행된 SELECT 문에서 사용할 수 있습니다.|  
|SQL_DESC_BASE_COLUMN_NAME|서버 커서를 생성하는 문에서 검색된 결과 집합 또는 FOR BROWSE 절을 포함하는 실행된 SELECT 문에서 사용할 수 있습니다.|  
|SQL_DESC_BASE_TABLE_NAME|서버 커서를 생성하는 문에서 검색된 결과 집합 또는 FOR BROWSE 절을 포함하는 실행된 SELECT 문에서 사용할 수 있습니다.|  
|SQL_DESC_CATALOG_NAME|데이터베이스 이름 서버 커서를 생성하는 문에서 검색된 결과 집합 또는 FOR BROWSE 절을 포함하는 실행된 SELECT 문에서 사용할 수 있습니다.|  
|SQL_DESC_LABEL|모든 결과 집합에서 사용할 수 있습니다. 값은 SQL_DESC_NAME 필드의 값과 동일합니다.<br /><br /> 열이 레이블 할당이 포함되지 않은 식의 결과이면 필드 길이가 0입니다.|  
|SQL_DESC_NAME|모든 결과 집합에서 사용할 수 있습니다. 값은 SQL_DESC_LABEL 필드의 값과 동일합니다.<br /><br /> 열이 레이블 할당이 포함되지 않은 식의 결과이면 필드 길이가 0입니다.|  
|SQL_DESC_SCHEMA_NAME|소유자 이름입니다. 서버 커서를 생성하는 문에서 검색된 결과 집합 또는 FOR BROWSE 절을 포함하는 실행된 SELECT 문에서 사용할 수 있습니다.<br /><br /> SELECT 문에서 열에 대해 소유자 이름이 지정된 경우에만 사용할 수 있습니다.|  
|SQL_DESC_TABLE_NAME|서버 커서를 생성하는 문에서 검색된 결과 집합 또는 FOR BROWSE 절을 포함하는 실행된 SELECT 문에서 사용할 수 있습니다.|  
|SQL_DESC_UNNAMED|열이 레이블 할당이 포함되지 않은 식의 결과인 경우를 제외하고는 결과 집합의 모든 열에 대해 SQL_NAMED입니다. SQL_DESC_UNNAMED가 SQL_UNNAMED를 반환하면 모든 ODBC 열 식별자 특성이 열에 대해 길이가 0인 문자열을 포함함을 나타냅니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 SET FMTONLY 문을 사용 하 여 준비 되었지만 명령의 문에 대해 **Sqlcolattribute** 를 호출할 때 서버 오버 헤드를 줄입니다.  
  
 값 형식이 클 경우 **Sqlcolattribute** 는 다음 값을 반환 합니다.  
  
|필드 식별자|변경 내용 설명|  
|----------------------|---------------------------|  
|SQL_DESC_DISPLAY_SIZE|열의 데이터를 표시하는 데 필요한 최대 문자 수입니다. 큰 값 유형 열에 대해서는 SQL_SS_LENGTH_UNLIMITED 값을 반환합니다.|  
|SQL_DESC_LENGTH|결과 집합에 있는 열의 실제 길이를 반환합니다. 큰 값 유형 열에 대해서는 SQL_SS_LENGTH_UNLIMITED 값을 반환합니다.|  
|SQL_DESC_OCTET_LENGTH|큰 값 유형 열의 최대 길이를 반환합니다. 크기가 무제한임을 나타낼 때는 SQL_SS_LENGTH_UNLIMITED를 사용합니다.|  
|SQL_DESC_PRECISION|큰 값 유형 열에 대해 SQL_SS_LENGTH_UNLIMITED 값을 반환합니다.|  
|SQL_DESC_TYPE|큰 값 유형에 대해 SQL_VARCHAR, SQL_WVARCHAR 및 SQL_VARBINARY를 반환합니다.|  
|SQL_DESC_TYPE_NAME|큰 값 유형에 대해 "varchar", "varbinary", "nvarchar"를 반환합니다.|  
  
 버전에 관계없이, 준비된 SQL 문의 일괄 처리에서 여러 개의 결과 집합이 생성될 경우 첫 번째 결과 집합에 대해서만 열 특성이 보고됩니다.  
  
 다음 열 특성은 Native Client ODBC 드라이버에 의해 노출 되는 확장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 *NumericAttrPtr* 매개 변수의 모든 값을 반환 합니다. WORD 배열에 대한 포인터인 SQL_CA_SS_COMPUTE_BYLIST를 제외하고는 SDWORD(signed long) 값을 반환합니다.  
  
|필드 식별자|반환 값|  
|----------------------|--------------------|  
|SQL_CA_SS_COLUMN_HIDDEN*|참조된 열이 FOR BROWSE가 포함된 Transact-SQL SELECT 문을 지원하기 위해 생성된 숨겨진 기본 키의 일부인 경우 TRUE입니다.|  
|SQL_CA_SS_COLUMN_ID|현재 Transact-SQL SELECT 문 내 COMPUTE 절 결과 열의 서수 위치입니다.|  
|SQL_CA_SS_COLUMN_KEY*|참조된 열이 행 기본 키의 일부이고 Transact-SQL SELECT 문에 FOR BROWSE가 포함된 경우 TRUE입니다.|  
|SQL_CA_SS_COLUMN_OP|COMPUTE 절 열의 값에 대한 집계 연산자를 지정하는 정수입니다. 정수 값에 대한 정의는 sqlncli.h에 있습니다.|  
|SQL_CA_SS_COLUMN_ORDER|ODBC 또는 Transact-SQL SELECT 문의 ORDER BY 절 내 열의 서수 위치입니다.|  
|SQL_CA_SS_COLUMN_SIZE|열에서 검색된 데이터 값을 SQL_C_BINARY 변수에 바인딩하는 데 필요한 최대 길이(바이트)입니다.|  
|SQL_CA_SS_COLUMN_SSTYPE|SQL Server 열에 저장된 데이터의 네이티브 데이터 형식입니다. 형식 값에 대한 정의는 sqlncli.h에 있습니다.|  
|SQL_CA_SS_COLUMN_UTYPE|SQL Server 열의 사용자 정의 데이터 형식에 대한 기본 데이터 형식입니다. 형식 값에 대한 정의는 sqlncli.h에 있습니다.|  
|SQL_CA_SS_COLUMN_VARYLEN|열의 데이터 길이가 가변적인 경우 TRUE이고, 그렇지 않으면 FALSE입니다.|  
|SQL_CA_SS_COMPUTE_BYLIST|COMPUTE 절의 BY 구에 사용되는 열을 지정하는 WORD(unsigned short) 배열에 대한 포인터입니다. COMPUTE 절에 BY 구가 지정되어 있지 않으면 NULL 포인터를 반환합니다.<br /><br /> 배열의 첫 번째 요소는 BY 목록 열의 개수를 포함하고 나머지 요소는 열 서수입니다.|  
|SQL_CA_SS_COMPUTE_ID|현재 Transact-sql SELECT 문에서 COMPUTE 절의 결과인 행의 계산 *eid* 입니다.|  
|SQL_CA_SS_NUM_COMPUTES|현재 Transact-SQL SELECT 문에 지정된 COMPUTE 절의 수입니다.|  
|SQL_CA_SS_NUM_ORDERS|ODBC 또는 Transact-SQL SELECT 문의 ORDER BY 절에 지정된 열의 수입니다.|  
  
 \*   If 문 특성 SQL_SOPT_SS_HIDDEN_COLUMNS SQL_HC_ON로 설정 되어 있습니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에는 각각 XML 스키마 컬렉션 이름, 스키마 이름 및 카탈로그 이름을 나타내는 추가 정보를 제공 하는 드라이버별 설명자 필드가 도입 되었습니다. 이러한 속성에는 영숫자가 아닌 문자가 포함된 경우 따옴표나 이스케이프 문자가 필요하지 않습니다. 다음 표에는 새로 도입된 설명자 필드가 나와 있습니다.  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME|CharacterAttributePtr|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름입니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.<br /><br /> 이 정보는 읽기/쓰기 필드인 IRD의 SQL_DESC_SS_XML_SCHEMACOLLECTION_CATALOG_NAME 레코드 필드에서 반환됩니다.|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|CharacterAttributePtr|XML 스키마 컬렉션 이름이 정의된 스키마의 이름입니다. 스키마 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.<br /><br /> 이 정보는 읽기/쓰기 필드인 IRD의 SQL_DESC_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME 레코드 필드에서 반환됩니다.|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_NAME|CharacterAttributePtr|XML 스키마 컬렉션의 이름입니다. 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.<br /><br /> 이 정보는 읽기/쓰기 필드인 IRD의 SQL_DESC_SS_XML_SCHEMACOLLECTION_NAME 레코드 필드에서 반환됩니다.|  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에는 결과 집합의 UDT(사용자 정의 형식) 열 또는 저장 프로시저나 매개 변수가 있는 쿼리의 UDT 매개 변수에 대한 추가 정보를 제공하기 위한 새 드라이버 관련 설명자 필드도 도입되었습니다. 이러한 속성에는 영숫자가 아닌 문자가 포함된 경우 따옴표나 이스케이프 문자가 필요하지 않습니다. 다음 표에는 새로 도입된 설명자 필드가 나와 있습니다.  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_UDT_CATALOG_NAME|CharacterAttributePtr|UDT가 포함된 카탈로그의 이름입니다.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|CharacterAttributePtr|UDT가 포함된 스키마의 이름입니다.|  
|SQL_CA_SS_UDT_TYPE_NAME|CharacterAttributePtr|UDT의 이름입니다.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|CharacterAttributePtr|UDT의 정규화된 어셈블리 이름입니다.|  
  
 기존 설명자 필드 식별자인 SQL_DESC_TYPE_NAME은 UDT의 이름을 나타내는 데 사용됩니다. UDT 형식 열에 대한 SQL_DESC_TYPE 필드는 SQL_SS_UDT입니다.  
  
## <a name="sqlcolattribute-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLColAttribute 지원  
 날짜/시간 형식에 대해 반환 되는 값은 [매개 변수 및 결과 메타 데이터](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)의 "IRD 필드에서 반환 되는 정보" 섹션을 참조 하세요.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlcolattribute-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLColAttribute 지원  
 **Sqlcolattribute** 는 크기가 높은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC&#41;&#40;LARGE CLR 사용자 정의 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="sqlcolattribute-support-for-sparse-columns"></a>스파스 열에 대한 SQLColAttribute 지원  
 SQLColAttribute는 새 IRD (구현 행 설명자) 필드 SQL_CA_SS_IS_COLUMN_SET를 쿼리하여 열이 **column_set** 열인지 확인 합니다.  
  
 자세한 내용은 [스파스 열 지원 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLColAttribute 함수](../../odbc/reference/syntax/sqlcolattribute-function.md)   
 [ODBC API 구현 세부 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
