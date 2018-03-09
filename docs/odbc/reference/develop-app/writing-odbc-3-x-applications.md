---
title: "ODBC 3.x 응용 프로그램을 작성할 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da096dd38c87131259f9ea626fa874c0b83b7b95
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="writing-odbc-3x-applications"></a>ODBC 3.x 응용 프로그램 작성
경우는 ODBC 2. *x* 응용 프로그램은 ODBC 3으로 업그레이드 됩니다. *x*, 모두 ODBC 2와 함께 작동 되도록 작성 합니다. *x* 및 3. *x* 드라이버입니다. 응용 프로그램이 ODBC 3을 모두 활용 하려면 조건부 코드를 통합 해야 합니다. *x* 기능입니다.  
  
 SQL_OV_ODBC2를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 해야 합니다. 이 방법을 사용 하면 드라이버는 ODBC 2 비슷하게*.x* 드라이버 섹션에서 설명한 변경과 관련 하 여 [변경 된 동작](../../../odbc/reference/develop-app/behavioral-changes.md)합니다.  
  
 응용 프로그램 섹션에서 설명 하는 기능의 사용은 [새로운 기능](../../../odbc/reference/develop-app/new-features.md), 조건부 코드를 사용 하 여 드라이버는 ODBC 3 인지 여부를 확인 해야 합니다. *x* 또는 ODBC 2*.x* 드라이버입니다. 응용 프로그램이 사용 **SQLGetDiagField** 및 **SQLGetDiagRec** 가져오려면 ODBC 3. *x* SQLSTATEs 오류 이러한 조건부 코드 조각에 대 한 처리를 수행 하는 중입니다. 새로운 기능에 대해 다음 사항은 고려해 야 합니다.  
  
-   변경 행 집합 크기 동작에 영향을 받는 응용 프로그램 호출 하지 않도록 주의 해야 합니다. **SQLFetch** 배열 크기가 1 보다 큰 경우. 이러한 응용 프로그램에 대 한 호출을 대체 해야 **SQLExtendedFetch** 호출 하 여 **SQLSetStmtAttr** SQL_ATTR_ARRAY_STATUS_PTR 문 특성을 설정 하 고 **SQLFetchScroll**, 모두 ODBC 3 사용 가능한 공통 코드를 더 합니다. *x* 및 ODBC 2. *x* 드라이버입니다. 때문에 **SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE를 사용 하 여에 매핑할 수는 **SQLSetStmtAttr** 와 SQL_ROWSET_SIZE ODBC 2. *x* 드라이버, 응용 프로그램 설정 SQL_ATTR_ROW_ARRAY_SIZE 다중 행 인출 작업에 대 한 합니다.  
  
-   업그레이드 하는 대부분의 응용 프로그램 실제로 SQLSTATE 코드에 있는 변경 내용의 영향을 받지 않습니다. 영향을 받는 응용 프로그램, 기계적 검색 수 있으며 대부분의 경우 "SQLSTATE 매핑" 섹션의 오류 변환 테이블을 사용 하 여 ODBC 3 변환할 바꿉니다. *x* 오류 코드를 ODBC 2*.x* 코드입니다. ODBC 3 이후*.x* 드라이버 관리자는 ODBC 2에서 매핑을 수행 됩니다. *x* SQLSTATEs odbc 3. *x* SQLSTATEs, 이러한 응용 프로그램 작성자 검사만 ODBC 3에 대 한 필요 합니다. *x* SQLSTATEs 하며 ODBC 2를 포함 하는 방법에 대 한 걱정 하지 않습니다. *x* 조건부 코드의 Sqlstate입니다.  
  
-   응용 프로그램은 날짜, 시간 및 타임 스탬프 데이터 형식을의 훌륭한 사용, 응용 프로그램 자체는 ODBC 2로 선언할 수 있습니다. *x* 조절 코드를 사용 하는 대신 코드의 기존 응용 프로그램 및 사용 합니다.  
  
 업그레이드도 다음과 같습니다. 다음 단계를  
  
-   호출 **SQLSetEnvAttr** SQL_OV_ODBC2을 SQL_ATTR_ODBC_VERSION 환경 특성 설정에 대 한 연결을 할당 하십시오.  
  
-   에 대 한 모든 호출을 대체 **SQLAllocEnv**, **SQLAllocConnect**, 또는 **SQLAllocStmt** 호출 하 여 **SQLAllocHandle** 는 적절 한 *HandleType* SQL_HANDLE_ENV, sql_handle_dbc 라는, 또는 여의 인수입니다.  
  
-   에 대 한 모든 호출을 대체 **SQLFreeEnv** 또는 **SQLFreeConnect** 호출 하 여 **SQLFreeHandle** 는 적절 한 *HandleType* 인수 sql_handle_dbc 라는 또는 여 합니다.  
  
-   에 대 한 모든 호출을 대체 **SQLSetConnectOption** 호출 하 여 **SQLSetConnectAttr**합니다. 특성 값을 설정 문자열인 경우 설정의 *StringLength* 인수 적절 하 게 합니다. 변경 *특성* 인수는 SQL_XXXX SQL_ATTR_XXXX입니다.  
  
-   에 대 한 모든 호출을 대체 **SQLGetConnectOption** 호출 하 여 **SQLGetConnectAttr**합니다. 문자열이 나 이진 특성을 가져올 경우 설정 *BufferLength* 적절 한 값과 전달에는 *StringLength* 인수입니다. 변경 *특성* 인수는 SQL_XXXX SQL_ATTR_XXXX입니다.  
  
-   에 대 한 모든 호출을 대체 **SQLSetStmtOption** 호출 하 여 **SQLSetStmtAttr**합니다. 특성 값을 설정 문자열인 경우 설정의 *StringLength* 인수 적절 하 게 합니다. 변경 *특성* 인수는 SQL_XXXX SQL_ATTR_XXXX입니다.  
  
-   에 대 한 모든 호출을 대체 **SQLGetStmtOption** 호출 하 여 **SQLGetStmtAttr**합니다. 문자열이 나 이진 특성을 가져올 경우 설정 *BufferLength* 적절 한 값과 전달에는 *StringLength* 인수입니다. 변경 *특성* 인수는 SQL_XXXX SQL_ATTR_XXXX입니다.  
  
-   에 대 한 모든 호출을 대체 **SQLTransact** 호출 하 여 **SQLEndTran**합니다. 경우에 가장 오른쪽에 있는 유효한 핸들은 **SQLTransact** 호출은 환경 핸들을는 *HandleType* SQL_HANDLE_ENV의 인수에 사용 해야는 **SQLEndTran** 하 여 호출 적절 한 *처리* 인수입니다. 경우에 가장 오른쪽에 있는 유효한 핸들 프로그램 **SQLTransact** 호출 되는 연결 핸들을는 *HandleType* sql_handle_dbc 라는의 인수에 사용 해야는 **SQLEndTran** 하 여 호출 적절 한 *처리* 인수입니다.  
  
-   에 대 한 모든 호출을 대체 **SQLColAttributes** 호출 하 여 **SQLColAttribute**합니다. 경우는 *FieldIdentifier* 인수가 SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE, 또는 SQL_COLUMN_LENGTH, 함수 이름이 아닌 다른 값을 변경 하지 마십시오. 그렇지 않은 경우 변경 *FieldIdentifier* SQL_DESC_XXXX SQL_COLUMN_XXXX에서 합니다. 경우 *FieldIdentifier* SQL_DESC_CONCISE_TYPE 이며 데이터 형식은 datetime 데이터 형식, 해당 ODBC 3으로 변경*.x* 데이터 형식입니다.  
  
-   블록 커서, 스크롤 가능 커서 또는 둘 다를 사용 하 여 응용 프로그램은 다음을 수행 합니다.  
  
    -   행 집합 크기, 커서 유형 및 사용 하 여 커서 동시성 설정 **SQLSetStmtAttr**합니다.  
  
    -   호출 **SQLSetStmtAttr** SQL_ATTR_ROW_STATUS_PTR을 상태 레코드의 배열을를 가리키도록 설정할 수 있습니다.  
  
    -   호출 **SQLSetStmtAttr** SQL_ATTR_ROWS_FETCHED_PTR는 SQLINTEGER를 가리키도록 설정할 수 있습니다.  
  
    -   필요한 바인딩을 수행 하 고 SQL 문을 실행 합니다.  
  
    -   호출 **SQLFetchScroll** 행을 인출 하 고 결과에서 이동 하는 루프에서 설정 합니다.  
  
    -   응용 프로그램 호출 하 여 책갈피 인출 하려는 경우 **SQLSetStmtAttr** 은 SQL_ATTR_FETCH_BOOKMARK_PTR fetch, 하려는 하는 행 및 호출에 대 한 책갈피를 포함 하는 변수를 설정 하려면 **SQLFetchScroll** 와 *FetchOrientation* SQL_FETCH_BOOKMARK의 인수입니다.  
  
-   매개 변수 배열을 사용 하 여, 응용 프로그램은 다음을 수행 합니다.  
  
    -   호출 **SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE 특성 매개 변수 배열의 크기를로 설정 합니다.  
  
    -   호출 **SQLSetStmtAttr** SQL_ATTR_ROWS_PROCESSED_PTR 내부 UDWORD 변수를 가리키도록 설정할 수 있습니다.  
  
    -   수행 준비 바인딩하고 적절 하 게 작업을 실행 합니다.  
  
    -   어떤 이유로 든 (예: SQL_NEED_DATA)에 대 한 중단 되어 실행 하는 경우 "현재" 매개 변수 행 SQL_ATTR_ROWS_PROCESSED_PTR 가리키는 위치를 검사 하 여 찾아서.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [응용 프로그램의 이전 버전과의 호환성을 위한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [SQLCloseCursor 호출](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [SQLGetDiagField 호출](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [SQLSetPos 호출](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [커서 라이브러리 작업](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [커서 특성 1 정보 유형 매핑](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
