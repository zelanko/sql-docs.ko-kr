---
title: 바인딩 매개 변수 | 마이크로 소프트 문서
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01e179d2abc6ef786f94b6d7938f0e21938c5a59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304636"
---
# <a name="using-statement-parameters---binding-parameters"></a>문 매개 변수 사용 - 매개 변수 바인딩
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL 문을 실행하려면 먼저 SQL 문의 각 매개 변수 표식을 애플리케이션의 변수에 연결하거나 바인딩해야 합니다. 이 작업은 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 함수를 호출하여 수행됩니다. **SQLBindParameter는** 드라이버에 대한 프로그램 변수(주소, C 데이터 형식 등)를 설명합니다. 또한 매개 변수 표식의 서수 값을 나타낸 후 해당 표식이 나타내는 SQL 개체의 특성(SQL 데이터 형식, 전체 자릿수 등)을 설명하여 매개 변수 표식을 식별합니다.  
  
 문을 실행하기 전이라면 언제라도 매개 변수 표식을 바인딩하거나 다시 바인딩할 수 있습니다. 매개 변수 바인딩은 다음 호출 중 하나가 발생하기 전까지 계속 유지됩니다.  
  
-   *옵션* 매개 변수를 SQL_RESET_PARAMS 설정된 [SQLFreeStmt를](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 호출하여 문 핸들에 바인딩된 모든 매개 변수를 해제합니다.  
  
-   *매개 변수번호가* 바인딩된 매개 변수 마커의 서수로 설정된 **SQLBindParameter호출은** 이전 바인딩을 자동으로 해제합니다.  
  
 애플리케이션에서 매개 변수를 프로그램 변수의 배열에 바인딩하여 SQL 문을 일괄 처리할 수도 있습니다. 배열 바인딩에는 다음과 같은 두 가지 유형이 있습니다.  
  
-   열 단위 바인딩은 각 매개 변수가 고유한 변수 배열에 바인딩될 때 발생합니다.  
  
     열별 바인딩은 SQL_ATTR_PARAM_BIND_TYPE 설정된 *특성을* 사용하여 [SQLSetStmtAttr을](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 호출하여 지정하고 *ValuePtr은* SQL_PARAM_BIND_BY_COLUMN 설정합니다.  
  
-   행 단위 바인딩은 SQL 문의 모든 매개 변수가 매개 변수의 개별 변수를 포함하는 구조체 배열에 하나의 단위로 바인딩될 때 발생합니다.  
  
     행 별 바인딩은 SQL_ATTR_PARAM_BIND_TYPE 설정 된 *특성을* 가진 **SQLSetStmtAttr을** 호출 하 여 지정 하 고 *ValuePtr* 프로그램 변수를 보유 하는 구조의 크기에 설정 합니다.  
  
 네이티브 클라이언트 ODBC 드라이버가 문자 또는 이진 문자열 매개 변수를 서버에 보내면 **SQLBindParameter** *ColumnSize* 매개 변수에 지정된 길이로 값을 압축합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 2.x 응용 프로그램이 *ColumnSize에*대해 0을 지정하는 경우 드라이버는 매개 변수 값을 데이터 형식의 정밀도에 보전합니다. 전체 자릿수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 연결할 경우 8000이고 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 경우 255입니다. *ColumnSize는* 변형 열에 대해 바이트로 되어 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 저장 프로시저 매개 변수의 이름 정의를 지원합니다. ODBC 3.5에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저를 호출할 때 사용되는 명명된 매개 변수에 대한 지원이 도입되었습니다. 이 지원을 통해 다음을 수행할 수 있습니다.  
  
-   저장 프로시저를 호출하고 저장 프로시저에 대해 정의된 매개 변수의 하위 집합에 대한 값을 제공할 수 있습니다.  
  
-   저장 프로시저를 만들 때 지정한 것과 다른 순서로 애플리케이션에서 매개 변수를 지정할 수 있습니다.  
  
 명명된 매개 변수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE** 문 또는 ODBC CALL 이스케이프 시퀀스를 사용하여 저장 프로시저를 실행할 때만 지원됩니다.  
  
 **SQL_DESC_NAME** 저장 프로시저 매개 변수에 대해 설정된 경우 쿼리의 모든 저장 프로시저 매개 변수도 **SQL_DESC_NAME**설정해야 합니다.  매개 변수가 **설정된** 저장 프로시저 호출에서 리터럴을 사용하는 경우 SQL_DESC_NAME *'name*= *name* @p1*값'이라는*형식을 사용해야 합니다. 자세한 내용은 [이름별 바인딩 매개 변수(명명된 매개 변수)를](https://go.microsoft.com/fwlink/?LinkId=167215)참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [문 매개 변수 사용](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
