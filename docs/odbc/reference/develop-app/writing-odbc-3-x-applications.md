---
description: ODBC 3.x 애플리케이션 작성
title: ODBC 3.x 응용 프로그램 작성 | Microsoft Docs
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
ms.openlocfilehash: 7df97b99df10e613ee45aaa3c01174b46160e740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421357"
---
# <a name="writing-odbc-3x-applications"></a>ODBC 3.x 애플리케이션 작성
*Odbc 2.x 응용 프로그램* *을 odbc 2.x*로 업그레이드 하는 *경우 odbc 2.x 및 2.x* 드라이버 모두에서 작동 하도록 작성 해야 *합니다.* 응용 프로그램 *은 ODBC 3.x* 기능을 최대한 활용 하기 위해 조건부 코드를 통합 해야 합니다.  
  
 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC2으로 설정 해야 합니다. 이렇게 하면 드라이버가 [동작 변경](../../../odbc/reference/develop-app/behavioral-changes.md)섹션에 설명 된 변경 내용과 관련 *된 ODBC 2.x* 드라이버 처럼 동작 합니다.  
  
 응용 프로그램에서 [새로운 기능](../../../odbc/reference/develop-app/new-features.md)섹션에 설명 된 기능 중 하나를 사용 하는 경우에는 조건부 코드를 사용 하 여 드라이버가 odbc *2.x 또는 odbc* *2.x 드라이버 인지* 여부를 확인 해야 합니다. 응용 프로그램은 이러한 조건부 코드 조각에서 오류 처리를 수행 하는 동안 **SQLGetDiagField** 및 **SQLGetDiagRec** 를 사용 하 여 ODBC 3.x sqlstates를 *가져옵니다.* 새 기능에 대 한 다음 사항을 고려해 야 합니다.  
  
-   행 집합 크기 동작 변경의 영향을 받는 응용 프로그램은 배열 크기가 1 보다 클 경우 **Sqlfetch** 를 호출 하지 않도록 주의 해야 합니다. 이러한 응용 프로그램은 **SQLSetStmtAttr** 에 대 한 호출로 **sqlextendedfetch** 호출을 대체 하 여 SQL_ATTR_ARRAY_STATUS_PTR Statement 특성과 **sqlextendedfetch**을 설정 해야 합니다. *따라서 odbc 2.x* 와 odbc *2.x 드라이버 모두* 에서 작동 하는 공통 코드가 있습니다. SQL_ATTR_ROW_ARRAY_SIZE 있는 **SQLSetStmtAttr** *는 ODBC 2.x* 드라이버의 SQL_ROWSET_SIZE를 사용 하 여 **SQLSetStmtAttr** 에 매핑되므로 응용 프로그램은 다중 행 페치 작업에 대해 SQL_ATTR_ROW_ARRAY_SIZE을 설정할 수 있습니다.  
  
-   업그레이드 하는 대부분의 응용 프로그램은 실제로 SQLSTATE 코드의 변경으로 인해 영향을 받지 않습니다. 영향을 받는 응용 프로그램에 대해 기계적 검색을 수행 하 고 대부분의 경우 "SQLSTATE 매핑" 섹션의 오류 변환 표를 사용 하 여 ODBC *2.x 오류 코드* 를 odbc *2.x 코드로 변환할* 수 있습니다. ODBC *3.X 드라이버 관리자는 odbc 2.x* *SQLSTATES* *에서 odbc 3.x* sqlstates로 매핑을 수행 하므로 이러한 응용 프로그램 작성자는 odbc *2.x sqlstates* 에 대 한 검사를 수행 하 고 조건부 코드에 *는 odbc 2.x* sqlstates를 포함 하는 것에 대해 걱정 하지 않아도 됩니다.  
  
-   응용 프로그램에서 날짜, 시간 및 타임 스탬프 데이터 형식을 효과적으로 사용 하는 경우 응용 프로그램은 스스로 *를 ODBC 2.x* 응용 프로그램으로 선언 하 고 조절 코드를 사용 하는 대신 기존 코드를 사용할 수 있습니다.  
  
 업그레이드에는 다음 단계도 포함 되어야 합니다.  
  
-   SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC2로 설정 하려면 연결을 할당 하기 전에 **SQLSetEnvAttr** 를 호출 합니다.  
  
-   **Sqlallocenv**, **sqlallocenv**또는 **sqlallocenv** 에 대 한 모든 호출을 SQL_HANDLE_ENV, SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT의 적절 한 *HandleType* 인수를 사용 하 여 **SQLAllocHandle** 에 대 한 호출로 바꿉니다.  
  
-   **Sqlfreeenv** 또는 **SQLFreeConnect** 에 대 한 모든 호출을 SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT의 적절 한 *HandleType* 인수를 사용 하 여 **sqlfreeenv** 에 대 한 호출로 바꿉니다.  
  
-   **SQLSetConnectOption** 에 대 한 모든 호출을 **SQLSetConnectAttr**에 대 한 호출로 바꿉니다. 문자열이 값을 갖는 특성을 설정 하는 경우 *Stringlength* 인수를 적절 하 게 설정 합니다. SQL_XXXX에서 SQL_ATTR_XXXX로 *특성* 인수를 변경 하십시오.  
  
-   **SQLGetConnectOption** 에 대 한 모든 호출을 **SQLGetConnectAttr**에 대 한 호출로 바꿉니다. 문자열이 나 이진 특성을 가져오는 경우 *Bufferlength* 를 적절 한 값으로 설정 하 고 *stringlength* 인수를 전달 합니다. SQL_XXXX에서 SQL_ATTR_XXXX로 *특성* 인수를 변경 하십시오.  
  
-   **SQLSetStmtOption** 에 대 한 모든 호출을 **SQLSetStmtAttr**에 대 한 호출로 바꿉니다. 문자열이 값을 갖는 특성을 설정 하는 경우 *Stringlength* 인수를 적절 하 게 설정 합니다. SQL_XXXX에서 SQL_ATTR_XXXX로 *특성* 인수를 변경 하십시오.  
  
-   **SQLGetStmtOption** 에 대 한 모든 호출을 **SQLGetStmtAttr**에 대 한 호출로 바꿉니다. 문자열이 나 이진 특성을 가져오는 경우 *Bufferlength* 를 적절 한 값으로 설정 하 고 *stringlength* 인수를 전달 합니다. SQL_XXXX에서 SQL_ATTR_XXXX로 *특성* 인수를 변경 하십시오.  
  
-   **Sqlendtran**에 대 한 호출로 **sqltransact** 에 대 한 모든 호출을 바꿉니다. **Sqltransact** 호출의 가장 오른쪽 유효한 핸들이 환경 핸들 인 경우 적절 한 *핸들* 인수를 사용 하 여 **sqlendtran** 호출에 SQL_HANDLE_ENV의 *HandleType* 인수를 사용 해야 합니다. **Sqltransact** 호출의 가장 오른쪽 유효한 핸들이 연결 핸들 인 경우 적절 한 *핸들* 인수를 사용 하 여 **sqlendtran** 호출에 SQL_HANDLE_DBC의 *HandleType* 인수를 사용 해야 합니다.  
  
-   **Sqlcolattributes** 에 대 한 모든 호출을 **sqlcolattributes**에 대 한 호출로 바꿉니다. *FieldIdentifier* 인수가 SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE 또는 SQL_COLUMN_LENGTH 인 경우 함수 이름 이외의 값은 변경 하지 마십시오. 그렇지 않으면 *FieldIdentifier* 을 SQL_COLUMN_XXXX에서 SQL_DESC_XXXX로 변경 합니다. *FieldIdentifier* 가 SQL_DESC_CONCISE_TYPE이 고 데이터 형식이 datetime 데이터 형식인 경우 *해당 ODBC 2.x* 데이터 형식으로 변경 합니다.  
  
-   블록 커서, 스크롤 가능 커서 또는 둘 다를 사용 하는 경우 응용 프로그램은 다음을 수행 합니다.  
  
    -   **SQLSetStmtAttr**를 사용 하 여 행 집합 크기, 커서 유형 및 커서 동시성을 설정 합니다.  
  
    -   **SQLSetStmtAttr** 를 호출 하 여 상태 레코드의 배열을 가리키도록 SQL_ATTR_ROW_STATUS_PTR를 설정 합니다.  
  
    -   **SQLSetStmtAttr** 를 호출 하 여 sqlinteger를 가리키도록 SQL_ATTR_ROWS_FETCHED_PTR를 설정 합니다.  
  
    -   필요한 바인딩을 수행 하 고 SQL 문을 실행 합니다.  
  
    -   루프에서 **Sqlfetchscroll** 을 호출 하 여 행을 인출 하 고 결과 집합에서 이동 합니다.  
  
    -   책갈피를 사용 하 여 인출 하려는 경우 응용 프로그램은 **SQLSetStmtAttr** 를 호출 하 여 페치할 행의 책갈피를 포함 하는 변수로 SQL_ATTR_FETCH_BOOKMARK_PTR를 설정 하 고 SQL_FETCH_BOOKMARK의 *fetchorientation* 인수를 사용 하 여 **sqlfetchscroll** 을 호출 합니다.  
  
-   매개 변수 배열을 사용 하는 경우 응용 프로그램은 다음을 수행 합니다.  
  
    -   **SQLSetStmtAttr** 를 호출 하 여 SQL_ATTR_PARAMSET_SIZE 특성을 매개 변수 배열의 크기로 설정 합니다.  
  
    -   **SQLSetStmtAttr** 를 호출 하 여 내부 udword 변수를 가리키도록 SQL_ATTR_ROWS_PROCESSED_PTR를 설정 합니다.  
  
    -   준비, 바인딩 및 실행 작업을 적절 하 게 수행 합니다.  
  
    -   몇 가지 이유로 실행이 중단 되는 경우 (예: SQL_NEED_DATA) SQL_ATTR_ROWS_PROCESSED_PTR가 가리키는 위치를 검사 하 여 매개 변수의 "current" 행을 찾을 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [애플리케이션의 이전 버전과의 호환성을 위한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [SQLCloseCursor 호출](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [SQLGetDiagField 호출](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [SQLSetPos 호출](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [커서 라이브러리 작업](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [커서 특성 1 정보 형식 매핑](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
