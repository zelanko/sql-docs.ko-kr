---
title: 위치 지정 업데이트 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2336944b583b6077d75bd5155bb4b52c66d9a852
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63200528"
---
# <a name="positioned-updates-odbc"></a>위치 지정 업데이트(ODBC)
  ODBC는 커서에서 위치 지정 업데이트를 수행하는 두 가지 방법을 지원합니다.  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 절  
  
 가장 일반적인 방법은 **SQLSetPos**를 사용 하는 것입니다. 여기에는 다음 옵션이 있습니다.  
  
 SQL_POSITION  
 커서를 현재 행 집합의 특정 행에 위치시킵니다.  
  
 SQL_REFRESH  
 커서가 현재 위치한 행으로부터 가져온 값을 갖는 결과 집합 열에 바인딩된 프로그램 변수를 새로 고칩니다.  
  
 SQL_UPDATE  
 결과 집합 열에 바인딩된 프로그램 변수에 저장된 값으로 커서의 현재 행을 업데이트합니다.  
  
 SQL_DELETE  
 커서에서 현재 행을 삭제합니다.  
  
 서버 커서를 사용 하도록 문 핸들 커서 특성을 설정 하면 **SQLSetPos** 를 모든 문 결과 집합과 함께 사용할 수 있습니다. 결과 집합 열은 프로그램 변수에 바인딩되어야 합니다. 응용 프로그램이 행을 인출 하는 즉시 **SQLSetPos**(SQL_POSTION)를 호출 하 여 커서를 행에 배치 합니다. 그런 다음 SQLSetPos(SQL_DELETE)를 호출하여 현재 행을 삭제하거나, 새 데이터 값을 바인딩된 프로그램 변수로 이동하고 SQLSetPos(SQL_UPDATE)를 호출하여 현재 행을 업데이트할 수 있습니다.  
  
 응용 프로그램은 **SQLSetPos**를 사용 하 여 행 집합의 모든 행을 업데이트 하거나 삭제할 수 있습니다. **SQLSetPos** 호출은 SQL 문을 생성 하 고 실행 하는 편리한 대안입니다. **SQLSetPos** 는 현재 행 집합에서 작동 하며 [sqlfetchscroll](../native-client-odbc-api/sqlfetchscroll.md)을 호출한 후에만 사용할 수 있습니다.  
  
 행 집합 크기는 SQL_ATTR_ROW_ARRAY_SIZE 특성 인수를 사용 하 여 [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) 에 대 한 호출로 설정 됩니다. **SQLSetPos** 는 **Sqlfetch** 또는 **sqlfetchscroll**을 호출한 후에만 새 행 집합 크기를 사용 합니다. 예를 들어 행 집합 크기가 변경 되 면 **SQLSetPos** 를 호출한 다음 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 합니다. **SQLSetPos** 를 호출 하면 이전 행 집합 크기가 사용 되지만 **Sqlfetch** 또는 **sqlfetchscroll** 은 새 행 집합 크기를 사용 합니다.  
  
 행 집합의 첫 번째 행 번호는 1입니다. **SQLSetPos** 의 RowNumber 인수는 행 집합에서 행을 식별 해야 합니다. 즉, 해당 값은 1에서 가장 최근에 인출 된 행 수 사이의 범위에 있어야 합니다. 이 값은 행 집합 크기보다 작을 수 있습니다. RowNumber가 0이면 행 집합의 모든 행에 작업이 적용됩니다.  
  
 **SQLSetPos** 의 삭제 작업은 데이터 원본에서 하나 이상의 선택 된 테이블 행을 삭제 합니다. **Sqlsetpos**를 사용 하 여 행을 삭제 하기 위해 응용 프로그램은 작업을 SQL_DELETE로 설정 하 고 RowNumber를 삭제할 행 번호로 설정 하 여 **SQLSetPos** 를 호출 합니다. RowNumber가 0이면 행 집합의 모든 행이 삭제됩니다.  
  
 **SQLSetPos** 가 반환 된 후 삭제 된 행은 현재 행 이며 상태는 SQL_ROW_DELETED입니다. [SQLGetData](../native-client-odbc-api/sqlgetdata.md) 또는 **SQLSetPos**호출과 같은 추가 위치 지정 작업에는 행을 사용할 수 없습니다.  
  
 행 집합의 모든 행을 삭제 하는 경우 (RowNumber가 0 인 경우) 응용 프로그램은 **SQLSetPos**의 업데이트 작업과 마찬가지로 행 작업 배열을 사용 하 여 드라이버가 특정 행을 삭제 하지 못하도록 할 수 있습니다.  
  
 삭제되는 모든 행은 결과 집합에 있는 행이여야 합니다. 인출로 인해 애플리케이션 버퍼가 가득 차고 행 상태 배열이 유지되는 경우 이러한 각각의 행 위치에서 값은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW일 수 없습니다.  
  
 위치 지정 업데이트는 UPDATE, DELETE 및 INSERT 문에 WHERE CURRENT OF 절을 사용하여 수행할 수도 있습니다. 여기서 CURRENT를 사용 하려면 [SQLGetCursorName](../native-client-odbc-api/sqlgetcursorname.md) 함수를 호출 하거나 **SQLSetCursorName**를 호출 하 여 지정할 수 있는 커서 이름이 ODBC에서 생성 됩니다. 다음은 ODBC 애플리케이션에서 WHERE CURRENT OF 업데이트를 수행하는 일반적인 단계입니다.  
  
-   **SQLSetCursorName** 를 호출 하 여 문 핸들에 대 한 커서 이름을 설정 합니다.  
  
-   FOR UPDATE OF 절을 사용하여 SELECT 문을 작성하고 실행합니다.  
  
-   **Sqlfetchscroll** 을 호출 하 여 행 집합 또는 **sqlfetch** 를 검색 하 여 행을 검색 합니다.  
  
-   **SQLSetPos** (SQL_POSITION)를 호출 하 여 커서를 행에 배치 합니다.  
  
-   **SQLSetCursorName**로 설정 된 커서 이름을 사용 하 여 WHERE CURRENT OF 절이 있는 UPDATE 문을 빌드하고 실행 합니다.  
  
 또는 SELECT 문을 실행 하기 전에 **SQLSetCursorName** 를 호출 하는 대신 select 문을 실행 한 후에는 **SQLGetCursorName** 를 호출할 수 있습니다. **SQLGetCursorName** 는 **SQLSetCursorName**를 사용 하 여 커서 이름을 설정 하지 않은 경우 ODBC에서 할당 한 기본 커서 이름을 반환 합니다.  
  
 서버 커서를 사용 하는 경우 현재 위치 보다 **SQLSetPos** 를 사용 하는 것이 좋습니다. ODBC 커서 라이브러리에 업데이트 가능한 정적 커서를 사용하면 커서 라이브러리가 기본 테이블의 키 값을 통해 WHERE 절을 추가하는 방법으로 WHERE CURRENT OF 업데이트를 구현합니다. 이 경우 테이블의 키가 고유하지 않으면 불필요한 업데이트가 수행될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 사용](using-cursors-odbc.md)  
  
  
