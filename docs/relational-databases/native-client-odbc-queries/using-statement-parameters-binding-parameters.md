---
title: 바인딩 매개 변수 | Microsoft Docs
description: 문을 실행 하기 전에 SQL 문의 각 매개 변수 표식을 응용 프로그램의 변수에 바인딩하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- statements [ODBC], parameters
- binding parameters [SQL Server Native Client]
- parameter markers [ODBC]
- unbound parameter markers
- SQLBindParameter function
- ODBC applications, parameters
- bound parameter markers [SQL Server Native Client]
ms.assetid: d6c69739-8f89-475f-a60a-b2f6c06576e2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a1ddbcb0f19cb62310e748da4f710b196357acbc
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478074"
---
# <a name="using-statement-parameters---binding-parameters"></a>문 매개 변수 사용 - 매개 변수 바인딩
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SQL 문을 실행하려면 먼저 SQL 문의 각 매개 변수 표식을 애플리케이션의 변수에 연결하거나 바인딩해야 합니다. [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 함수를 호출 하 여이 작업을 수행 합니다. **SQLBindParameter** 는 프로그램 변수 (주소, C 데이터 형식 등)를 드라이버에 설명 합니다. 또한 매개 변수 표식의 서수 값을 나타낸 후 해당 표식이 나타내는 SQL 개체의 특성(SQL 데이터 형식, 전체 자릿수 등)을 설명하여 매개 변수 표식을 식별합니다.  
  
 문을 실행하기 전이라면 언제라도 매개 변수 표식을 바인딩하거나 다시 바인딩할 수 있습니다. 매개 변수 바인딩은 다음 호출 중 하나가 발생하기 전까지 계속 유지됩니다.  
  
-   *Option* 매개 변수를 SQL_RESET_PARAMS 설정 하 여 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 를 호출 하면 문 핸들에 바인딩된 모든 매개 변수가 해제 됩니다.  
  
-   *Parameternumber* 가 바인딩된 매개 변수 표식의 서 수로 설정 된 **SQLBindParameter** 에 대 한 호출은 자동으로 이전 바인딩을 해제 합니다.  
  
 애플리케이션에서 매개 변수를 프로그램 변수의 배열에 바인딩하여 SQL 문을 일괄 처리할 수도 있습니다. 배열 바인딩에는 다음과 같은 두 가지 유형이 있습니다.  
  
-   열 단위 바인딩은 각 매개 변수가 고유한 변수 배열에 바인딩될 때 발생합니다.  
  
     열 단위 바인딩은 *특성* 을 SQL_ATTR_PARAM_BIND_TYPE *로 설정 하 고 SQL_PARAM_BIND_BY_COLUMN* 로 설정 된 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 를 호출 하 여 지정 합니다.  
  
-   행 단위 바인딩은 SQL 문의 모든 매개 변수가 매개 변수의 개별 변수를 포함하는 구조체 배열에 하나의 단위로 바인딩될 때 발생합니다.  
  
     행 단위 바인딩은 *특성* 을 SQL_ATTR_PARAM_BIND_TYPE로 설정 하 고 *valueptr* 을 프로그램 변수를 포함 하는 구조체의 크기로 설정 하 여 **SQLSetStmtAttr** 를 호출 하 여 지정 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 문자 또는 이진 문자열 매개 변수를 서버에 보낼 때 **SQLBindParameter** *columnsize* 매개 변수에 지정 된 길이까지 값을 채웁니다. ODBC 2.x 응용 프로그램에서 *Columnsize* 에 대해 0을 지정 하는 경우 드라이버는 매개 변수 값을 데이터 형식의 전체 자릿수로 채웁니다. 전체 자릿수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 연결할 경우 8000이고 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 경우 255입니다. *Columnsize* 는 변형 열의 경우 바이트 단위입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 저장 프로시저 매개 변수의 이름 정의를 지원합니다. ODBC 3.5에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저를 호출할 때 사용되는 명명된 매개 변수에 대한 지원이 도입되었습니다. 이 지원을 통해 다음을 수행할 수 있습니다.  
  
-   저장 프로시저를 호출하고 저장 프로시저에 대해 정의된 매개 변수의 하위 집합에 대한 값을 제공할 수 있습니다.  
  
-   저장 프로시저를 만들 때 지정한 것과 다른 순서로 애플리케이션에서 매개 변수를 지정할 수 있습니다.  
  
 명명 된 매개 변수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] **execute** 문 또는 ODBC CALL 이스케이프 시퀀스를 사용 하 여 저장 프로시저를 실행 하는 경우에만 지원 됩니다.  
  
 저장 프로시저 매개 변수에 대 한 **SQL_DESC_NAME** 설정 된 경우 쿼리의 모든 저장 프로시저 매개 변수는 **SQL_DESC_NAME** 도 설정 해야 합니다.  매개 변수가 **SQL_DESC_NAME** 설정 된 저장 프로시저 호출에 리터럴이 사용 되는 경우 리터럴은 *' name* = *value*' 형식을 사용 해야 합니다. 여기서 *name* 은 저장 프로시저 매개 변수 이름 (예: @p1 )입니다. 자세한 내용은 [이름으로 매개 변수 바인딩 (명명 된 매개 변수)](../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [문 매개 변수 사용](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
