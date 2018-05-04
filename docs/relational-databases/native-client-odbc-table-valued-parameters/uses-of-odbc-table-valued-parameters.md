---
title: ODBC 테이블 반환 매개 변수를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9b8042eaad34f437c860da0ae045050086e54f4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="uses-of-odbc-table-valued-parameters"></a>ODBC 테이블 반환 매개 변수 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  이 항목에서는 ODBC에서 테이블 반환 매개 변수를 사용하는 기본 사용자 시나리오를 설명합니다.  
  
-   완전히 바인딩된 여러 행 버퍼를 사용하는 테이블 반환 매개 변수(모든 값을 메모리에 로드하여 TVP로 데이터 전송)  
  
-   행 스트리밍을 사용하는 테이블 반환 매개 변수(실행 시 데이터를 사용하여 TVP로 데이터 전송)  
  
-   시스템 카탈로그에서 테이블 반환 매개 변수 메타데이터 검색  
  
-   준비된 문에서 테이블 반환 매개 변수 메타데이터 검색  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>완전히 바인딩된 여러 행 버퍼를 사용하는 테이블 반환 매개 변수(모든 값을 메모리에 로드하여 TVP로 데이터 전송)  
 완전히 바인딩된 여러 행 버퍼와 함께 사용하는 경우 모든 매개 변수 값을 메모리에서 사용할 수 있습니다. 이는 테이블 반환 매개 변수를 단일 저장 프로시저로 패키지할 수 있는 OLTP 트랜잭션의 대표적인 예입니다. 테이블 반환 매개 변수가 없다면 복잡한 다중 문 일괄 처리를 동적으로 생성하거나 서버를 여러 번 호출해야 할 수 있습니다.  
  
 자체는 테이블 반환 매개 변수를 사용 하 여 바인딩된 [SQLBindParameter](http://go.microsoft.com/fwlink/?LinkId=59328) 다른 매개 변수와 함께 합니다. 모든 매개 변수에 바인딩된 후 응용 프로그램이 테이블 반환 매개 변수에 각 매개 변수 포커스 특성 SQL_SOPT_SS_PARAM_FOCUS를 설정 하 고 테이블 반환 매개 변수 열에 대 한 SQLBindParameter를 호출 합니다.  
  
 테이블 반환 매개 변수의 서버 유형은 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고유 형식인 SQL_SS_TABLE입니다. SQL_SS_TABLE의 바인딩 C 형식은 항상 SQL_C_DEFAULT여야 합니다. 테이블 반환 매개 변수 바인딩 매개 변수에 대해서는 데이터가 전송되지 않습니다. 이 매개 변수는 테이블 메타데이터를 전달하고, 테이블 반환 매개 변수 구성 열의 데이터 전달 방법을 제어하는 데 사용됩니다.  
  
 테이블 반환 매개 변수의 길이는 서버로 전송되는 행 수로 설정됩니다. *ColumnSize* 보낼 수 있는 행의 최대 수를 지정 하는 테이블 반환 매개 변수에 대 한 SQLBindParameter의 매개 변수;이 값은 열 버퍼의 배열 크기입니다. *ParameterValuePtr* 가 SQLBindParameter에서 테이블 반환 매개 변수에 대 한 매개 변수 버퍼입니다. *ParameterValuePtr* 및 관련 *BufferLength* 필요할 때 테이블 반환 매개 변수의 형식 이름을 전달 하는 데 사용 됩니다. 형식 이름은 저장 프로시저 호출에는 필요하지 않지만 SQL 문에는 필요합니다.  
  
 SQLBindParameter에 대 한 호출에는 테이블 반환 매개 변수 형식 이름의 지정 하는 경우 항상 ANSI 응용 프로그램으로 빌드된 응용 프로그램 에서도 유니코드 값으로 지정 해야 합니다. SQLSetDescField를 사용 하 여 테이블 반환 매개 변수 형식 이름을 지정 하면 응용 프로그램 빌드 방법을 준수 하는 리터럴을 사용할 수 있습니다. ODBC 드라이버 관리자에서 필요한 모든 유니코드 변환을 수행합니다.  
  
 메타 데이터 테이블 반환 매개 변수 및 테이블 반환 매개 변수 열에 대 한 SQLGetDescRec, SQLSetDescRec, SQLGetDescField, 및 SQLSetDescField를 사용 하 여 개별적 및 명시적으로 조작할 수 있습니다. 그러나 SQLBindParameter 오버 로드 보다 편리 이며 대부분의 경우에서 명시적 설명자 액세스가 필요 하지 않습니다. 이 접근 방식은 테이블 반환 매개 변수에 대 한 영향을 받는 설명자 필드는 약간 다른 점을 제외 하 고 다른 데이터 형식에 대 한 SQLBindParameter의 정의와 일치 합니다.  
  
 응용 프로그램에서 동적 SQL에 테이블 반환 매개 변수가 사용되어 테이블 반환 매개 변수의 형식 이름을 반드시 제공해야 하는 경우도 있습니다. 이 경우 테이블 반환 매개 변수는 연결에 대 한 현재 기본 스키마에 정의 되지 않은 경우 SQL_CA_SS_TYPE_CATALOG_NAME 및 SQL_CA_SS_TYPE_SCHEMA_NAME SQLSetDescField를 사용 하 여 설정 되어야 합니다. 테이블 형식 정의와 테이블 반환 매개 변수는 동일한 데이터베이스에 있어야 하므로 응용 프로그램에서 테이블 반환 매개 변수를 사용하는 경우 SQL_CA_SS_TYPE_CATALOG_NAME을 설정해서는 안 됩니다. 그렇지 않으면 SQLSetDescField 오류를 보고 합니다.  
  
 이 시나리오에 대 한 예제 코드는 프로시저는 `demo_fixed_TVP_binding` 에 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)합니다.  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>행 스트리밍을 사용하는 테이블 반환 매개 변수(실행 시 데이터를 사용하여 TVP로 데이터 전송)  
 이 시나리오에서 응용 프로그램은 드라이버가 요청하면 행을 제공하며 제공된 행은 서버로 스트리밍됩니다. 따라서 모든 행을 메모리에 버퍼링할 필요가 없습니다. 이는 대량 삽입/업데이트 시나리오를 나타냅니다. 테이블 반환 매개 변수는 매개 변수 배열과 대량 복사의 중간 정도 수준에 해당하는 성능을 제공합니다. 즉, 테이블 반환 매개 변수는 매개 변수 배열만큼 프로그래밍하기 쉬우면서도 서버에서 더 뛰어난 융통성을 제공합니다.  
  
 테이블 반환 매개 변수와 해당 열은 완전히 바인딩된 여러 행 버퍼를 사용하는 테이블 반환 매개 변수 섹션에서 설명한 대로 바인딩되지만 테이블 반환 매개 변수 자체의 길이 표시기는 SQL_DATA_AT_EXEC로 설정됩니다. 실행 시 데이터 매개 변수에 대 한 일반적인 방식 SQLExecute 또는 SQLExecuteDirect에 응답 하는 드라이버-, 즉 SQL_NEED_DATA를 반환 하 여 합니다. SQLParamData의 값을 반환 드라이버가 테이블 반환 매개 변수에 대 한 데이터를 허용 하도록 준비 되 면 *ParameterValuePtr* SQLBindParameter에서 합니다.  
  
 응용 프로그램 테이블 반환 매개 변수에 대 한 SQLPutData를 사용 하 여 테이블 반환 매개 변수 구성 열에 대 한 데이터의 가용성을 나타냅니다. 테이블 반환 매개 변수에 대 한 SQLPutData를 호출할 때 *DataPtr* 항상 null 이어야 하 고 *StrLen_or_Ind* 해야 0 또는 숫자에 대해 지정 된 배열 크기 보다 작거나 같은 테이블 반환 매개 변수 버퍼 (의 *ColumnSize* SQLBindParameter의 매개 변수). 0은 테이블 반환 매개 변수에 대한 행이 더 이상 없어 드라이버가 다음 실제 프로시저 매개 변수를 처리하게 됨을 나타냅니다. 때 *StrLen_or_Ind* 는 0이 아닌 드라이버는 테이블 반환 매개 변수 구성 열의 같은 방식으로 처리 아닌 테이블 반환 매개 변수 바인딩 매개 변수: 각 테이블 반환 매개 변수 열 실제 데이터를 지정할 수 길이, SQL_NULL_DATA, 해당 길이/표시기 버퍼를 통해 실행 시 데이터를 지정할 수 있습니다. 개별적으로 전달 해야 하는 문자 또는 이진 값은 SQLPutData에 대 한 호출 평소와 같이 반복 테이블 반환 매개 변수 열 값으로 전달할 수 있습니다.  
  
 테이블 반환 매개 변수 열이 모두 처리되면 드라이버가 다시 테이블 반환 매개 변수로 돌아와서 테이블 반환 매개 변수 데이터의 행을 추가로 처리하기 시작합니다. 따라서 실행 시 데이터 테이블 반환 매개 변수의 경우 드라이버가 바인딩된 매개 변수를 순차적으로 검색하는 일반적인 방식을 따르지 않습니다. SQLPutData로 호출 될 때까지 바인딩된 테이블 반환 매개 변수를 폴링지 것입니다 *StrLen_Or_IndPtr* 0 될 때 드라이버가 테이블 반환 매개 변수 열을 건너뛰고 다음 실제 저장된 프로시저 매개 변수를 이동 합니다.  SQLPutData 표시기 값을 전달 하는 1 보다 크거나, 경우 드라이버가 테이블 반환 매개 변수 열 및 행 순서 대로 처리 모든 바운드 행 및 열에 대 한 값이 될 때까지 합니다. 그런 다음 드라이버는 테이블 반환 매개 변수로 돌아갑니다. SQLParamData에서 테이블 반환 매개 변수에 대 한 토큰을 수신 하 고 테이블 반환 매개 변수에 대 한 SQLPutData (hstmt, NULL, n)를 호출 사이의 응용 프로그램 설정 해야 테이블 반환 매개 변수 구성 열 데이터와 표시기에 대 한 버퍼 내용을 다음 행 또는 행이 서버에 전달 합니다.  
  
 이 시나리오에 대 한 예제 코드는 루틴에 `demo_variable_TVP_binding` 에 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)합니다.  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>시스템 카탈로그에서 테이블 반환 매개 변수 메타데이터 검색  
 응용 프로그램이 테이블 반환 매개 변수의 매개 변수가 있는 프로시저에 대 한 SQLProcedureColumns 호출, DATA_TYPE SQL_SS_TABLE TYPE_NAME은 테이블 반환 매개 변수에 대 한 테이블 형식의 이름으로 반환 됩니다. 두 개의 추가 열 SQLProcedureColumns에서 반환 된 결과 집합에 추가 됩니다: SS_TYPE_CATALOG_NAME 여기서 테이블 반환 매개 변수의 테이블 형식이 정의 하 고 ss_type_schema_name은 스키마의 이름을 반환 하는 카탈로그의 이름을 반환 위치는 여기서는 테이블 반환 매개 변수의 테이블 유형에 정의 됩니다. ODBC 사양에 따라 SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMA_NAME은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 추가된 모든 드라이버 관련 열 앞에, 그리고 ODBC 자체에서 위임한 모든 열 뒤에 표시됩니다.  
  
 새 열은 테이블 반환 매개 변수뿐만 아니라 CLR 사용자 정의 형식 매개 변수에 대해서도 채워집니다. UDT 매개 변수의 기존 스키마와 카탈로그 열도 채워지지만 스키마와 카탈로그 열이 필요한 데이터 형식에 공용 스키마 및 카탈로그 열을 사용함으로써 이후 응용 프로그램 개발 과정이 간단해집니다. XML 스키마 컬렉션은 다소 다르며 이 변경 사항이 적용되지 않습니다.  
  
 응용 프로그램 SQLTables를 사용 하 여 영구 테이블, 시스템 테이블 및 뷰에 적용 되는 동일한 방식으로 테이블 형식의 이름을 결정 합니다. 응용 프로그램에서 테이블 반환 매개 변수와 연결된 테이블 형식을 식별할 수 있도록 TABLE TYPE이라는 새로운 테이블 형식이 도입되었습니다. 테이블 형식과 일반 테이블은 서로 다른 네임스페이스를 사용합니다. 즉, 테이블 형식과 실제 테이블에 동일한 이름을 사용할 수 있습니다. 이를 처리하기 위해 SQL_SOPT_SS_NAME_SCOPE라는 새로운 문 특성이 도입되었습니다. 이 특성 SQLTables 및 테이블 이름을 매개 변수로 사용 하는 기타 카탈로그 함수는 실제 테이블의 이름으로 테이블 이름 또는 테이블 형식의 이름은 해석 해야 하는지 여부를 지정 합니다.  
  
 SQLColumns를 사용 하 여 영구 테이블 하지만 먼저 SQL_SOPT_SS_NAME_SCOPE를 실제 테이블이 아니라 테이블 형식으로 작동 하는지 나타내는 설정 해야 듯이 내에서 테이블 형식에 대 한 열을 결정 하는 응용 프로그램. SQLPrimaryKeys는 테이블 형식에 SQL_SOPT_SS_NAME_SCOPE를 사용 하 여 다시 사용할 수도 있습니다.  
  
 이 시나리오에 대 한 예제 코드는 루틴에 `demo_metadata_from_catalog_APIs` 에 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)합니다.  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>준비된 문에서 테이블 반환 매개 변수 메타데이터 검색  
 이 시나리오에서는 응용 프로그램 및 사용 하 여 SQLNumParameters SQLDescribeParam 테이블 반환 매개 변수에 대 한 메타 데이터를 검색 합니다.  
  
 테이블 반환 매개 변수의 형식 이름을 검색하는 데는 SQL_CA_SS_TYPE_NAME이라는 IPD 필드가 사용되고, 스키마와 카탈로그를 검색하는 데는 각각 SQL_CA_SS_TYPE_SCHEMA_NAME과 SQL_CA_SS_TYPE_CATALOG_NAME이라는 IPD 필드가 사용됩니다.  
  
 테이블 형식 정의와 테이블 반환 매개 변수는 동일한 데이터베이스에 있어야 합니다. SQLSetDescField는 테이블 반환 매개 변수를 사용 하는 경우 SQL_CA_SS_TYPE_CATALOG_NAME을 설정 하는 응용 프로그램 오류를 보고 합니다.  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 및 SQL_CA_SS_TYPE_SCHEMA_NAME을 함께 사용하여 CLR 사용자 정의 형식 매개 변수와 연결된 카탈로그와 스키마를 검색할 수도 있습니다. SQL_CA_SS_TYPE_CATALOG_NAME 및 SQL_CA_SS_TYPE_SCHEMA_NAME은 CLR UDT 형식에 대한 기존 형식 관련 카탈로그 스키마 특성을 대체합니다.  
  
 응용 프로그램 SQLDescribeParam 열은 테이블 반환 매개 변수 열에 대 한 메타 데이터를 반환 하지 않으므로,이 시나리오에서는 테이블 반환 매개 변수에 대 한 열 메타 데이터를 검색할 SQLColumns를 사용 합니다.  
  
 이 사용 사례에 대 한 예제 코드는 루틴에 `demo_metadata_from_prepared_statement` 에 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
