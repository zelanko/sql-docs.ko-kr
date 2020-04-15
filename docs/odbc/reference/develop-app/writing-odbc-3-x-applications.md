---
title: ODBC 3.x 응용 프로그램 작성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ba48d76babcaa5fcc49a541088f7c4cc349b569
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288991"
---
# <a name="writing-odbc-3x-applications"></a>ODBC 3.x 애플리케이션 작성
ODBC *2.x* 응용 프로그램이 ODBC *3.x로*업그레이드되면 ODBC *2.x* 및 *3.x* 드라이버모두에서 작동하도록 작성해야 합니다. 응용 프로그램은 ODBC *3.x* 기능을 최대한 활용하기 위해 조건부 코드를 통합해야 합니다.  
  
 SQL_ATTR_ODBC_VERSION 환경 특성은 SQL_OV_ODBC2 설정해야 합니다. 이렇게 하면 동작 [변경](../../../odbc/reference/develop-app/behavioral-changes.md)섹션에 설명된 변경 내용과 관련하여 드라이버가 ODBC *2.x* 드라이버처럼 동작합니다.  
  
 응용 프로그램이 섹션에 설명된 기능을 사용하는 경우 [새 기능,](../../../odbc/reference/develop-app/new-features.md)조건부 코드를 사용하여 드라이버가 ODBC *3.x* 또는 ODBC *2.x* 드라이버인지 여부를 결정해야 합니다. 이 응용 프로그램은 **SQLGetDiagField** 및 **SQLGetDiagRec를** 사용하여 ODBC *3.x* SQLSTATEs를 가져오는 동시에 이러한 조건부 코드 조각에서 오류 처리를 수행합니다. 새 기능에 대한 다음 사항을 고려해야 합니다.  
  
-   행 집합 크기 동작의 변경에 의해 영향을 받는 응용 프로그램은 배열 크기가 1보다 큰 경우 **SQLFetch를** 호출하지 않도록 주의해야 합니다. 이러한 응용 프로그램은 **SQLExtendedFetch호출을** **SQLSetStmtAttr호출로** 대체하여 SQL_ATTR_ARRAY_STATUS_PTR 문 특성을 설정하고 **SQLFetchScroll에**대해 ODBC *3.x* 및 ODBC *2.x* 드라이버모두에서 작동하는 공통 코드를 갖도록 해야 합니다. SQL_ATTR_ROW_ARRAY_SIZE 있는 **SQLSetStmtAttr은** ODBC *2.x* 드라이버에 대한 SQL_ROWSET_SIZE 있는 **SQLSetStmtAttr에** 매핑되므로 응용 프로그램은 다중 가져오기 작업에 대해 SQL_ATTR_ROW_ARRAY_SIZE 설정할 수 있습니다.  
  
-   업그레이드하는 대부분의 응용 프로그램은 SQLSTATE 코드의 변경 에 의해 실제로 영향을 받지 않습니다. 영향을 받는 응용 프로그램의 경우 대부분의 경우 "SQLSTATE 매핑" 섹션의 오류 변환 테이블을 사용하여 ODBC *3.x* 오류 코드를 ODBC *2.x* 코드로 변환하는 기계식 검색을 수행하고 대체할 수 있습니다. ODBC *3.x* 드라이버 관리자는 ODBC *2.x* SQLSTATEs에서 ODBC *3.x* SQLSTATE에 매핑을 수행하므로 이러한 응용 프로그램 작성자는 ODBC *3.x* SQLSTATE만 확인해야 하며 조건부 코드에 ODBC *2.x* SQLSTATE를 포함할 염려가 없습니다.  
  
-   응용 프로그램이 날짜, 시간 및 타임스탬프 데이터 형식을 많이 사용하는 경우 응용 프로그램은 자신을 ODBC *2.x* 응용 프로그램으로 선언하고 컨디셔닝 코드를 사용하는 대신 기존 코드를 사용할 수 있습니다.  
  
 업그레이드에는 다음 단계도 포함되어야 합니다.  
  
-   연결을 할당하기 전에 **SQLSetEnvAttr을** 호출하여 SQL_OV_ODBC2 SQL_ATTR_ODBC_VERSION 환경 특성을 설정합니다.  
  
-   **SQLAllocEnv,** **SQLAllocConnect**또는 **SQLAllocStmt에** 대한 모든 호출을 SQL_HANDLE_ENV, SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT 적절한 *핸들 유형* 인수로 **SQLAllocHandle에** 대한 호출로 바꿉습니다.  
  
-   **SQLFreeEnv** 또는 **SQLFreeConnect에** 대한 모든 호출을 SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT 적절한 *핸들 유형* 인수로 **SQLFreeHandle에** 대한 호출로 바꿉습니다.  
  
-   **SQLSetConnect옵션에** 대한 모든 호출을 **SQLSetConnectAttr**에 대한 호출로 바꿉니다. 값이 문자열인 특성을 설정하는 경우 *StringLength* 인수를 적절하게 설정합니다. *특성* 인수를 SQL_XXXX SQL_ATTR_XXXX 변경합니다.  
  
-   **SQLGetConnect옵션에** 대한 모든 호출을 **SQLGetConnectAttr에**대한 호출로 바꿉니다. 문자열 또는 이진 특성을 가져오는 경우 *BufferLength를* 적절한 값으로 설정하고 *StringLength* 인수를 전달합니다. *특성* 인수를 SQL_XXXX SQL_ATTR_XXXX 변경합니다.  
  
-   **SQLSetStmt옵션에** 대한 모든 호출을 **SQLSetStmtAttr**에 대한 호출로 바꿉니다. 값이 문자열인 특성을 설정하는 경우 *StringLength* 인수를 적절하게 설정합니다. *특성* 인수를 SQL_XXXX SQL_ATTR_XXXX 변경합니다.  
  
-   **SQLGetStmt옵션에** 대한 모든 호출을 **SQLGetStmtAttr에**대한 호출로 바꿉니다. 문자열 또는 이진 특성을 가져오는 경우 *BufferLength를* 적절한 값으로 설정하고 *StringLength* 인수를 전달합니다. *특성* 인수를 SQL_XXXX SQL_ATTR_XXXX 변경합니다.  
  
-   **SQLTransact에** 대한 모든 호출을 **SQLEndTran에**대한 호출로 바꿉꿉꿉니까? **SQLTransact** 호출에서 가장 올바른 핸들이 환경 핸들인 경우 적절한 *핸들* 인수가 있는 **SQLEndTran** 호출에서 *SQL_HANDLE_ENV 핸들 형식* 인수를 사용해야 합니다. **SQLTransact** 호출에서 가장 올바른 핸들이 연결 핸들인 경우 적절한 *핸들* 인수가 있는 **SQLEndTran** 호출에서 SQL_HANDLE_DBC *핸들 유형* 인수를 사용해야 합니다.  
  
-   **SQLColAttributes에** 대한 모든 호출을 **SQLColAttribute**에 대한 호출로 바꿉꿉니까? *FieldIdentifier* 인수가 SQL_COLUMN_PRECISION SQL_COLUMN_SCALE 또는 SQL_COLUMN_LENGTH 경우 함수 이름 이외의 다른 것은 변경하지 마십시오. 그렇지 않은 경우 *필드식별자를* SQL_COLUMN_XXXX SQL_DESC_XXXX 변경합니다. *FieldIdentifier가* SQL_DESC_CONCISE_TYPE 데이터 형식이 날짜 시간 데이터 형식인 경우 해당 ODBC *3.x* 데이터 유형으로 변경합니다.  
  
-   블록 커서, 스크롤 가능한 커서 또는 둘 다를 사용하는 경우 응용 프로그램은 다음을 수행합니다.  
  
    -   **SQLSetStmtAttr을**사용하여 행 집합 크기, 커서 유형 및 커서 동시성을 설정합니다.  
  
    -   **SQLSetStmtAttr을** 호출하여 상태 레코드 배열을 가리키도록 SQL_ATTR_ROW_STATUS_PTR 설정합니다.  
  
    -   **SQLSetStmtAttr을** 호출하여 SQLINTEGER를 가리키는 SQL_ATTR_ROWS_FETCHED_PTR 설정합니다.  
  
    -   필요한 바인딩을 수행하고 SQL 문을 실행합니다.  
  
    -   **루프에서 SQLFetchScroll를** 호출하여 행을 가져오고 결과 집합에서 이동합니다.  
  
    -   책갈피를 사용하여 가져오려는 경우 응용 프로그램은 **SQLSetStmtAttr을** 호출하여 가져올 행에 대한 책갈피를 포함하는 변수로 SQL_ATTR_FETCH_BOOKMARK_PTR 설정하고 SQL_FETCH_BOOKMARK *FetchOrientation* 인수를 사용하여 **SQLFetchScroll을** 호출합니다.  
  
-   매개 변수 배열을 사용하는 경우 응용 프로그램은 다음을 수행합니다.  
  
    -   **sqlSetStmtAttr을** 호출하여 SQL_ATTR_PARAMSET_SIZE 특성을 매개 변수 배열의 크기로 설정합니다.  
  
    -   **SQLSetStmtAttr을** 호출하여 내부 UDWORD 변수를 가리키도록 SQL_ATTR_ROWS_PROCESSED_PTR 설정합니다.  
  
    -   적절하게 작업을 준비, 바인딩 및 실행합니다.  
  
    -   SQL_NEED_DATA 같은 어떤 이유로 실행이 중지되면 SQL_ATTR_ROWS_PROCESSED_PTR 가리키는 위치를 검사하여 매개 변수의 "현재" 행을 찾을 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [애플리케이션의 이전 버전과의 호환성을 위한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [SQLCloseCursor 호출](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [SQLGetDiagField 호출](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [SQLSetPos 호출](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [커서 라이브러리 작업](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [커서 특성 1 정보 형식 매핑](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
