---
title: SQLBindParameter | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74122d531eba1f714e16c168838ee1653a8f1293
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302684"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLBindParameter** 를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 데이터를 제공할 때 데이터 변환을 수행하지 않아도 되기 때문에 애플리케이션의 클라이언트 및 서버 구성 요소 모두에서 성능이 크게 향상됩니다. 이 외에도 근사치 데이터 형식을 삽입하거나 업데이트할 경우의 전체 자릿수 손실을 줄일 수 있습니다.  
  
> [!NOTE]  
>  **char** 및 **wchar** 형식 데이터를 이미지 열에 삽입할 경우 이진 형식으로 변환된 후의 데이터 크기가 아니라 전달되는 데이터의 크기가 사용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 매개 변수 배열의 배열 요소 하나에 오류가 발생하면 드라이버는 나머지 배열 요소에 대해 문을 계속해서 실행합니다. 애플리케이션에서 문에 대해 매개 변수 상태 요소의 배열을 바인딩한 경우에는 오류가 발생한 매개 변수의 행을 배열에서 확인할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용할 경우 입력 매개 변수를 바인딩할 때 SQL_PARAM_INPUT을 지정합니다. OUTPUT 키워드를 사용하여 정의된 저장 프로시저 매개 변수를 바인딩할 경우에는 SQL_PARAM_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT만 지정합니다.  
  
 바인딩된 매개 변수 배열의 배열 요소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 문 실행 시 오류가 발생 하는 경우에는 NATIVE Client ODBC 드라이버를 사용 하 여 [sqlrowcount](../../relational-databases/native-client-odbc-api/sqlrowcount.md) 를 신뢰할 수 없습니다. ODBC 문 특성 SQL_ATTR_PARAMS_PROCESSED_PTR은 오류가 발생하기 전까지 처리된 행 수를 보고합니다. 그러면 필요한 경우 애플리케이션에서는 해당 매개 변수 상태 배열을 확인하여 성공적으로 실행된 문 수를 파악할 수 있습니다.  
  
## <a name="binding-parameters-for-sql-character-types"></a>SQL 문자 형식에 대한 매개 변수 바인딩  
 전달된 SQL 데이터 형식이 문자 형식인 경우 *ColumnSize* 는 문자 수입니다(바이트 아님). 바이트의 데이터 문자열 길이가 8000보다 큰 경우 *ColumnSize* 는 **SQL_SS_LENGTH_UNLIMITED**로 설정되어야 하며 이는 SQL 형식 크기에 제한이 없음을 나타냅니다.  
  
 예를 들어 SQL 데이터 형식이 **SQL_WVARCHAR**인 경우 *ColumnSize* 는 4000보다 크지 않아야 합니다. 실제 데이터 길이가 4000보다 큰 경우 *ColumnSize* 를 **SQL_SS_LENGTH_UNLIMITED** 로 설정하여 **nvarchar(max)** 가 드라이버에서 사용되도록 해야 합니다.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter와 테이블 반환 매개 변수  
 다른 매개 변수 형식과 마찬가지로 테이블 반환 매개 변수는 SQLBindParameter에 의해 바인딩됩니다.  
  
 테이블 반환 매개 변수가 바인딩된 후에는 해당 열도 바인딩됩니다. 열을 바인딩하려면 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 을 호출하여 테이블 반환 매개 변수의 서수에 SQL_SOPT_SS_PARAM_FOCUS를 설정합니다. 그런 다음 테이블 반환 매개 변수의 각 열에 대해 SQLBindParameter를 호출 합니다. SQL_SOPT_SS_PARAM_FOCUS를 0으로 설정하면 최상위 매개 변수 바인딩으로 돌아갈 수 있습니다.  
  
 매개 변수를 테이블 반환 매개 변수의 설명자 필드에 매핑하는 방법에 대 한 자세한 내용은 [테이블 반환 매개 변수 및 열 값의 바인딩 및 데이터 전송](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)을 참조 하세요.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLBindParameter 지원  
 날짜/시간 형식의 매개 변수 값은 [C에서 SQL로 변환](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)에 설명 된 대로 변환 됩니다. **time** 및 **datetimeoffset** 형식의 매개 변수는 해당되는 구조( *ValueType* 및 **SQL_C_DEFAULT** )를 사용할 경우 **SQL_C_BINARY** 을**SQL_SS_TIME2_STRUCT** 또는 **SQL_SS_TIMESTAMPOFFSET_STRUCT**로 지정해야 합니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLBindParameter 지원  
 **SQLBindParameter** 는 큰 CLR UDT(사용자 정의 형식)를 지원합니다. 자세한 내용은 [ODBC&#41;&#40;LARGE CLR 사용자 정의 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 구현 세부 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLBindParameter 함수](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
