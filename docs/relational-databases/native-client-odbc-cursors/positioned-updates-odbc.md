---
title: 위치 업데이트 (ODBC) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 52495f670986638cac02661240e349713424256e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305331"
---
# <a name="positioned-updates-odbc"></a>위치 지정 업데이트(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC는 커서에서 위치 지정 업데이트를 수행하는 두 가지 방법을 지원합니다.  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 절  
  
 더 일반적인 방법은 **SQLSetPos를**사용하는 것입니다. 여기에는 다음 옵션이 있습니다.  
  
 SQL_POSITION  
 커서를 현재 행 집합의 특정 행에 위치시킵니다.  
  
 SQL_REFRESH  
 커서가 현재 위치한 행으로부터 가져온 값을 갖는 결과 집합 열에 바인딩된 프로그램 변수를 새로 고칩니다.  
  
 SQL_UPDATE  
 결과 집합 열에 바인딩된 프로그램 변수에 저장된 값으로 커서의 현재 행을 업데이트합니다.  
  
 SQL_DELETE  
 커서에서 현재 행을 삭제합니다.  
  
 **SQLSetPos는** 명령문 핸들 커서 특성이 서버 커서를 사용하도록 설정된 경우 모든 문 결과 집합과 함께 사용할 수 있습니다. 결과 집합 열은 프로그램 변수에 바인딩되어야 합니다. 응용 프로그램이 행을 가져오는 즉시 **SQLSetPos(SQL_POSTION)를**호출하여 행에 커서를 배치합니다. 그런 다음 SQLSetPos(SQL_DELETE)를 호출하여 현재 행을 삭제하거나, 새 데이터 값을 바인딩된 프로그램 변수로 이동하고 SQLSetPos(SQL_UPDATE)를 호출하여 현재 행을 업데이트할 수 있습니다.  
  
 응용 프로그램은 **SQLSetPos**를 사용 하 고 행 집합의 행을 업데이트 하거나 삭제할 수 있습니다. **SQLSetPos호출은** SQL 문을 생성하고 실행하는 대신 편리한 대안입니다. **SQLSetPos는** 현재 행 집합에서 작동하며 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)을 호출한 후에만 사용할 수 있습니다.  
  
 행 집합 크기는 [sqlSetStmtAttr에](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 대한 호출에 의해 설정되며 SQL_ATTR_ROW_ARRAY_SIZE 특성 인수가 있습니다. **SQLSetPos는** 새 행 집합 크기를 사용하지만 **SQLFetch** 또는 **SQLFetchScroll**을 호출한 후에만 사용됩니다. 예를 들어 행 집합 크기가 변경되면 **SQLSetPos가** 호출된 다음 **SQLFetch** 또는 **SQLFetchScroll가** 호출됩니다. **SQLSetPos에** 대 한 호출은 이전 행 집합 크기를 사용 하지만 **SQLFetch** 또는 **SQLFetchScroll** 새 행 집합 크기를 사용 합니다.  
  
 행 집합의 첫 번째 행 번호는 1입니다. **SQLSetPos의** RowNumber 인수는 행 집합에서 행을 식별해야 합니다. 즉, 해당 값은 가장 최근에 가져온 행 수와 1 사이의 범위에 있어야 합니다. 이 값은 행 집합 크기보다 작을 수 있습니다. RowNumber가 0이면 행 집합의 모든 행에 작업이 적용됩니다.  
  
 **SQLSetPos의** 삭제 작업을 수행하면 데이터 원본이 테이블의 선택된 행 중 하나 이상을 삭제합니다. **SQLSetPos를**사용 하 고 행을 삭제 하려면 응용 프로그램은 SQL_DELETE 작업으로 설정 된 **SQLSetPos** 를 호출 하 고 RowNumber 삭제 할 행의 수로 설정 합니다. RowNumber가 0이면 행 집합의 모든 행이 삭제됩니다.  
  
 **SQLSetPos가** 반환되면 삭제된 행이 현재 행이며 해당 상태가 SQL_ROW_DELETED. 이 행은 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 또는 **SQLSetPos**에 대한 호출과 같은 추가 위치가 있는 작업에서는 사용할 수 없습니다.  
  
 행 집합의 모든 행을 삭제하면 (RowNumber가 0과 같음) 응용 프로그램은 **SQLSetPos의**업데이트 작업에 대해와 마찬가지로 행 작업 배열을 사용하여 드라이버가 특정 행을 삭제하지 못하게 할 수 있습니다.  
  
 삭제되는 모든 행은 결과 집합에 있는 행이여야 합니다. 인출로 인해 애플리케이션 버퍼가 가득 차고 행 상태 배열이 유지되는 경우 이러한 각각의 행 위치에서 값은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW일 수 없습니다.  
  
 위치 지정 업데이트는 UPDATE, DELETE 및 INSERT 문에 WHERE CURRENT OF 절을 사용하여 수행할 수도 있습니다. WHERE CURRENT OF에는 [SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) 함수가 호출될 때 ODBC가 생성하거나 **SQLSetCursorName**을 호출하여 지정할 수 있는 커서 이름이 필요합니다. 다음은 ODBC 애플리케이션에서 WHERE CURRENT OF 업데이트를 수행하는 일반적인 단계입니다.  
  
-   **SQLSetCursorName을** 호출하여 명령문 핸들에 대한 커서 이름을 설정합니다.  
  
-   FOR UPDATE OF 절을 사용하여 SELECT 문을 작성하고 실행합니다.  
  
-   **SQLFetchScroll를** 호출하여 행 집합 또는 **SQLFetch를** 검색하여 행을 검색합니다.  
  
-   **SQLSetPos(SQL_POSITION)를** 호출하여 행에 커서를 배치합니다.  
  
-   **SQLSetCursorName으로**설정된 커서 이름을 사용하여 WHERE CURRENT OF 절을 사용하여 UPDATE 문을 작성하고 실행합니다.  
  
 또는 SELECT 문을 실행하기 전에 **SQLSetCursorName을** 호출하는 대신 SELECT 문을 실행한 후 **SQLGetCursorName을** 호출할 수 있습니다. **SQLGetCursorName 을** 사용하여 커서 이름을 설정하지 않은 경우 ODBC에서 할당한 기본 커서 이름을 **반환합니다.**  
  
 **SQLSetPos는** 서버 커서를 사용할 때 현재 위치 보다 선호 됩니다. ODBC 커서 라이브러리에 업데이트 가능한 정적 커서를 사용하면 커서 라이브러리가 기본 테이블의 키 값을 통해 WHERE 절을 추가하는 방법으로 WHERE CURRENT OF 업데이트를 구현합니다. 이 경우 테이블의 키가 고유하지 않으면 불필요한 업데이트가 수행될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 사용](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
