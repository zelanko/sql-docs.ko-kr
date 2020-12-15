---
description: ODBC 테이블 반환 매개 변수 사용
title: ODBC Table-Valued 매개 변수 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6d4337c24d50ec1971edf759e9568e190ceaebbd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473494"
---
# <a name="uses-of-odbc-table-valued-parameters"></a>ODBC 테이블 반환 매개 변수 사용
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  이 항목에서는 ODBC에서 테이블 반환 매개 변수를 사용하는 기본 사용자 시나리오를 설명합니다.  
  
-   완전히 바인딩된 여러 행 버퍼를 사용하는 테이블 반환 매개 변수(모든 값을 메모리에 로드하여 TVP로 데이터 전송)  
  
-   행 스트리밍을 사용하는 테이블 반환 매개 변수(실행 시 데이터를 사용하여 TVP로 데이터 전송)  
  
-   시스템 카탈로그에서 테이블 반환 매개 변수 메타데이터 검색  
  
-   준비된 문에서 테이블 반환 매개 변수 메타데이터 검색  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>완전히 바인딩된 여러 행 버퍼를 사용하는 테이블 반환 매개 변수(모든 값을 메모리에 로드하여 TVP로 데이터 전송)  
 완전히 바인딩된 여러 행 버퍼와 함께 사용하는 경우 모든 매개 변수 값을 메모리에서 사용할 수 있습니다. 이는 테이블 반환 매개 변수를 단일 저장 프로시저로 패키지할 수 있는 OLTP 트랜잭션의 대표적인 예입니다. 테이블 반환 매개 변수가 없다면 복잡한 다중 문 일괄 처리를 동적으로 생성하거나 서버를 여러 번 호출해야 할 수 있습니다.  
  
 테이블 반환 매개 변수 자체는 다른 매개 변수와 함께 [SQLBindParameter](../../odbc/reference/syntax/sqlbindparameter-function.md) 를 사용 하 여 바인딩됩니다. 모든 매개 변수가 바인딩된 후 응용 프로그램은 각 테이블 반환 매개 변수에 SQL_SOPT_SS_PARAM_FOCUS 매개 변수 포커스 특성을 설정 하 고 테이블 반환 매개 변수의 열에 대해 SQLBindParameter를 호출 합니다.  
  
 테이블 반환 매개 변수의 서버 유형은 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고유 형식인 SQL_SS_TABLE입니다. SQL_SS_TABLE의 바인딩 C 형식은 항상 SQL_C_DEFAULT여야 합니다. 테이블 반환 매개 변수 바인딩 매개 변수에 대해서는 데이터가 전송되지 않습니다. 이 매개 변수는 테이블 메타데이터를 전달하고, 테이블 반환 매개 변수 구성 열의 데이터 전달 방법을 제어하는 데 사용됩니다.  
  
 테이블 반환 매개 변수의 길이는 서버로 전송되는 행 수로 설정됩니다. 테이블 반환 매개 변수에 대 한 SQLBindParameter의 *Columnsize* 매개 변수는 전송할 수 있는 최대 행 수를 지정 합니다. 열 버퍼의 배열 크기입니다. *Parametervalueptr* 은 SQLBindParameter의 테이블 반환 매개 변수에 대 한 매개 변수 버퍼입니다. *Parametervalueptr* 및 관련 *bufferlength* 는 필요할 때 테이블 반환 매개 변수의 형식 이름을 전달 하는 데 사용 됩니다. 형식 이름은 저장 프로시저 호출에는 필요하지 않지만 SQL 문에는 필요합니다.  
  
 SQLBindParameter에 대 한 호출에 테이블 반환 매개 변수 형식 이름을 지정 하는 경우 ANSI 응용 프로그램으로 빌드된 응용 프로그램 에서도 항상 유니코드 값으로 지정 해야 합니다. SQLSetDescField를 사용 하 여 테이블 반환 매개 변수 형식 이름을 지정 하는 경우 응용 프로그램을 빌드하는 방법에 맞는 리터럴을 사용할 수 있습니다. ODBC 드라이버 관리자에서 필요한 모든 유니코드 변환을 수행합니다.  
  
 테이블 반환 매개 변수 및 테이블 반환 매개 변수 열에 대 한 메타 데이터는 SQLGetDescRec, SQLSetDescRec, SQLGetDescField 및 SQLSetDescField를 사용 하 여 개별적으로 또는 명시적으로 조작할 수 있습니다. 그러나 일반적으로 SQLBindParameter를 오버 로드 하는 것이 더 편리 하며 대부분의 경우 명시적 설명자 액세스가 필요 하지 않습니다. 이 방법은 다른 데이터 형식에 대 한 SQLBindParameter의 정의와 일치 합니다. 단, 테이블 반환 매개 변수의 경우 영향을 받는 설명자 필드가 약간 다릅니다.  
  
 애플리케이션에서 동적 SQL에 테이블 반환 매개 변수가 사용되어 테이블 반환 매개 변수의 형식 이름을 반드시 제공해야 하는 경우도 있습니다. 이 경우 연결에 대 한 현재 기본 스키마에 테이블 반환 매개 변수가 정의 되어 있지 않으면 SQLSetDescField를 사용 하 여 SQL_CA_SS_TYPE_CATALOG_NAME 및 SQL_CA_SS_TYPE_SCHEMA_NAME를 설정 해야 합니다. 테이블 형식 정의와 테이블 반환 매개 변수는 동일한 데이터베이스에 있어야 하므로 애플리케이션에서 테이블 반환 매개 변수를 사용하는 경우 SQL_CA_SS_TYPE_CATALOG_NAME을 설정해서는 안 됩니다. 그렇지 않으면 SQLSetDescField는 오류를 보고 합니다.  
  
 이 시나리오에 대 한 샘플 코드는 `demo_fixed_TVP_binding` [ODBC&#41;&#40;Table-Valued 매개 변수 사용 ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)의 절차에 있습니다.  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>행 스트리밍을 사용하는 테이블 반환 매개 변수(실행 시 데이터를 사용하여 TVP로 데이터 전송)  
 이 시나리오에서 애플리케이션은 드라이버가 요청하면 행을 제공하며 제공된 행은 서버로 스트리밍됩니다. 따라서 모든 행을 메모리에 버퍼링할 필요가 없습니다. 이는 대량 삽입/업데이트 시나리오를 나타냅니다. 테이블 반환 매개 변수는 매개 변수 배열과 대량 복사의 중간 정도 수준에 해당하는 성능을 제공합니다. 즉, 테이블 반환 매개 변수는 매개 변수 배열만큼 프로그래밍하기 쉬우면서도 서버에서 더 뛰어난 융통성을 제공합니다.  
  
 테이블 반환 매개 변수와 해당 열은 완전히 바인딩된 여러 행 버퍼를 사용하는 테이블 반환 매개 변수 섹션에서 설명한 대로 바인딩되지만 테이블 반환 매개 변수 자체의 길이 표시기는 SQL_DATA_AT_EXEC로 설정됩니다. 이 드라이버는 실행 시 데이터 매개 변수에 대해 일반적인 방법으로 (즉, SQL_NEED_DATA 반환) SQLExecute 또는 SQLExecuteDirect에 응답 합니다. 드라이버가 테이블 반환 매개 변수에 대 한 데이터를 받아들일 준비가 되 면 SQLParamData는 SQLBindParameter에서 *Parametervalueptr* 의 값을 반환 합니다.  
  
 응용 프로그램은 테이블 반환 매개 변수에 대해 SQLPutData를 사용 하 여 테이블 반환 매개 변수 구성 열의 데이터를 사용할 수 있는지 여부를 표시 합니다. 테이블 반환 매개 변수에 대해 SQLPutData를 호출 하는 경우 *Dataptr* 은 항상 null 이어야 하 고 *StrLen_or_Ind* 는 0 이거나 테이블 반환 매개 변수 버퍼에 지정 된 배열 크기 (SQLBindParameter의 *columnsize* 매개 변수) 보다 작거나 같은 숫자 여야 합니다. 0은 테이블 반환 매개 변수에 대한 행이 더 이상 없어 드라이버가 다음 실제 프로시저 매개 변수를 처리하게 됨을 나타냅니다. *StrLen_or_Ind* 가 0이 아닌 경우 드라이버는 테이블 반환 매개 변수 구성 열을 테이블 반환 매개 변수를 바인딩되지 않은 매개 변수와 같은 방식으로 처리 합니다. 각 테이블 반환 매개 변수 열은 실제 데이터 길이 SQL_NULL_DATA를 지정 하거나 길이/표시기 버퍼를 통해 실행 시 데이터를 지정할 수 있습니다. 문자 또는 이진 값을 조각으로 전달 하는 경우 일반적으로 SQLPutData에 대 한 반복적인 호출로 테이블 반환 매개 변수 열 값을 전달할 수 있습니다.  
  
 테이블 반환 매개 변수 열이 모두 처리되면 드라이버가 다시 테이블 반환 매개 변수로 돌아와서 테이블 반환 매개 변수 데이터의 행을 추가로 처리하기 시작합니다. 따라서 실행 시 데이터 테이블 반환 매개 변수의 경우 드라이버가 바인딩된 매개 변수를 순차적으로 검색하는 일반적인 방식을 따르지 않습니다. 바인딩된 테이블 반환 매개 변수는 SQLPutData가 0과 같은 *StrLen_Or_IndPtr* 를 사용 하 여 호출 될 때까지 폴링됩니다 .이 경우 드라이버가 테이블 반환 매개 변수 열을 건너뛰고 다음 실제 저장 프로시저 매개 변수로 이동 합니다.  SQLPutData가 1 보다 크거나 같은 표시기 값을 전달 하는 경우 드라이버는 모든 바인딩된 행과 열에 대 한 값이 있을 때까지 테이블 반환 매개 변수 열 및 행을 순차적으로 처리 합니다. 그런 다음 드라이버는 테이블 반환 매개 변수로 돌아갑니다. SQLParamData에서 테이블 반환 매개 변수에 대 한 토큰을 받고 테이블 반환 매개 변수에 대해 Sqlparamdata (hstmt, NULL, n)를 호출 하는 동안 응용 프로그램은 서버에 전달할 다음 행에 대 한 테이블 반환 매개 변수 구성 열 데이터와 표시기 버퍼 내용을 설정 해야 합니다.  
  
 이 시나리오에 대 한 샘플 코드는 `demo_variable_TVP_binding` [ODBC&#41;&#40;Table-Valued 매개 변수 사용 ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)의 루틴에 있습니다.  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>시스템 카탈로그에서 테이블 반환 매개 변수 메타데이터 검색  
 응용 프로그램에서 테이블 반환 매개 변수 매개 변수를 포함 하는 프로시저에 대해 SQLProcedureColumns를 호출 하면 DATA_TYPE SQL_SS_TABLE으로 반환 되 고 TYPE_NAME은 테이블 반환 매개 변수에 대 한 테이블 형식의 이름입니다. SQLProcedureColumns에서 반환 하는 결과 집합에 두 개의 추가 열이 추가 됩니다. SS_TYPE_CATALOG_NAME은 테이블-값 매개 변수의 테이블 형식이 정의 된 카탈로그의 이름을 반환 하 고 SS_TYPE_SCHEMA_NAME는 테이블 반환 매개 변수의 테이블 형식이 정의 된 스키마의 이름을 반환 합니다. ODBC 사양에 따라 SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMA_NAME은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 추가된 모든 드라이버 관련 열 앞에, 그리고 ODBC 자체에서 위임한 모든 열 뒤에 표시됩니다.  
  
 새 열은 테이블 반환 매개 변수뿐만 아니라 CLR 사용자 정의 형식 매개 변수에 대해서도 채워집니다. UDT 매개 변수의 기존 스키마와 카탈로그 열도 채워지지만 스키마와 카탈로그 열이 필요한 데이터 형식에 공용 스키마 및 카탈로그 열을 사용함으로써 이후 애플리케이션 개발 과정이 간단해집니다. XML 스키마 컬렉션은 다소 다르며 이 변경 사항이 적용되지 않습니다.  
  
 응용 프로그램은 SQLTables를 사용 하 여 영구 테이블, 시스템 테이블 및 뷰와 동일한 방식으로 테이블 형식의 이름을 확인 합니다. 애플리케이션에서 테이블 반환 매개 변수와 연결된 테이블 형식을 식별할 수 있도록 TABLE TYPE이라는 새로운 테이블 형식이 도입되었습니다. 테이블 형식과 일반 테이블은 서로 다른 네임스페이스를 사용합니다. 즉, 테이블 형식과 실제 테이블에 동일한 이름을 사용할 수 있습니다. 이를 처리하기 위해 SQL_SOPT_SS_NAME_SCOPE라는 새로운 문 특성이 도입되었습니다. 이 특성은 테이블 이름을 매개 변수로 사용 하는 SQLTables 및 기타 카탈로그 함수가 테이블 이름을 실제 테이블의 이름 또는 테이블 형식의 이름으로 해석 해야 하는지 여부를 지정 합니다.  
  
 응용 프로그램에서는 SQLColumns를 사용 하 여 영구 테이블에 대해 수행 되는 것과 같은 방식으로 테이블 형식에 대 한 열을 확인 하지만, 먼저 SQL_SOPT_SS_NAME_SCOPE를 설정 하 여 실제 테이블이 아닌 테이블 형식으로 작업 하 고 있음을 나타내야 합니다. SQLPrimaryKeys를 테이블 형식과 함께 사용 하 여 SQL_SOPT_SS_NAME_SCOPE을 다시 사용할 수도 있습니다.  
  
 이 시나리오에 대 한 샘플 코드는 `demo_metadata_from_catalog_APIs` [ODBC&#41;&#40;Table-Valued 매개 변수 사용 ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)의 루틴에 있습니다.  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>준비된 문에서 테이블 반환 매개 변수 메타데이터 검색  
 이 시나리오에서 응용 프로그램은 SQLNumParameters 및 SQLDescribeParam를 사용 하 여 테이블 반환 매개 변수의 메타 데이터를 검색 합니다.  
  
 테이블 반환 매개 변수의 형식 이름을 검색하는 데는 SQL_CA_SS_TYPE_NAME이라는 IPD 필드가 사용되고, 스키마와 카탈로그를 검색하는 데는 각각 SQL_CA_SS_TYPE_SCHEMA_NAME과 SQL_CA_SS_TYPE_CATALOG_NAME이라는 IPD 필드가 사용됩니다.  
  
 테이블 형식 정의와 테이블 반환 매개 변수는 동일한 데이터베이스에 있어야 합니다. SQLSetDescField는 응용 프로그램이 테이블 반환 매개 변수를 사용할 때 SQL_CA_SS_TYPE_CATALOG_NAME를 설정 하는 경우 오류를 보고 합니다.  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 및 SQL_CA_SS_TYPE_SCHEMA_NAME을 함께 사용하여 CLR 사용자 정의 형식 매개 변수와 연결된 카탈로그와 스키마를 검색할 수도 있습니다. SQL_CA_SS_TYPE_CATALOG_NAME 및 SQL_CA_SS_TYPE_SCHEMA_NAME은 CLR UDT 형식에 대한 기존 형식 관련 카탈로그 스키마 특성을 대체합니다.  
  
 SQLDescribeParam가 테이블 반환 매개 변수 열 열에 대 한 메타 데이터를 반환 하지 않기 때문에 응용 프로그램은이 시나리오에서 테이블 반환 매개 변수에 대 한 열 메타 데이터를 검색 하는 데 SQLColumns를 사용 합니다.  
  
 이 사용 사례에 대 한 샘플 코드는 `demo_metadata_from_prepared_statement` [ODBC&#41;&#40;Table-Valued 매개 변수 사용 ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)의 루틴에 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
