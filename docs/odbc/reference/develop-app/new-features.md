---
title: "새로운 기능 | Microsoft Docs"
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
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12e66ad8a1aa5e1389b69d5f30156f7b86b3b733
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="new-features"></a>새로운 기능
ODBC 3에서 다음과 같은 새로운 기능을 도입 했습니다. *x*합니다. ODBC 3입니다. *x* 작업 하는 ODBC 2 응용 프로그램*.x* 드라이버가이 기능을 사용할 수 없게 됩니다. ODBC 3입니다. *x* 는 ODBC 2 작업할 때 드라이버 관리자에서는 이러한 기능을 매핑하지 않습니다*.x* 드라이버입니다.  
  
-   설명자를 사용 하는 함수를 인수로 처리: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**, 및 **SQLCopyDesc**합니다.  
  
-   함수 **SQLSetEnvAttr** 및 **SQLGetEnvAttr**합니다.  
  
-   사용 **SQLAllocHandle** 설명자 핸들을 할당 합니다. (사용 **SQLAllocHandle** 환경, 연결 및 문 핸들을 할당 하는 복제, 신규가 아닌 기능입니다.)  
  
-   사용 **SQLGetConnectAttr** SQL_ATTR_AUTO_IPD 연결 특성을 가져옵니다. (사용 **SQLSetConnectAttr** 을 설정 하려면 및 **SQLGetConnectAttr** 다른 연결 특성은 중복 된, 신규가 아닌 기능을 합니다.)  
  
-   사용 **SQLSetStmtAttr** 을 설정 하려면 및 **SQLGetStmtAttr** 다음 문 특성을 가져올 수 있습니다. (사용 **SQLSetStmtAttr** 을 설정 하려면 및 **SQLGetStmtAttr** 다른 문 특성은 중복 된, 신규가 아닌 기능을 합니다.)  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   사용 **SQLGetStmtAttr** 다음 문 특성을 가져옵니다. (사용 **SQLGetStmtAttr** get 다른 문 특성을 중복된 기능을 하지 새로운 기능입니다.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   간격 C 데이터 형식, 간격 SQL 데이터 형식, BIGINT C 데이터 형식 및 SQL_C_NUMERIC 데이터 구조 사용.  
  
-   행 단위 바인딩 매개 변수입니다.  
  
-   같은 오프셋 기반 책갈피 인출 **SQLFetchScroll** 와 *FetchOrientation* SQL_FETCH_BOOKMARK 및 0이 아닌 오프셋을 지정 하는 인수입니다.  
  
-   **SQLFetch** 행 상태 배열이 있는 섞여 있는 전략은 호출 하는 여러 행을 인출, 가져온 행 수를 반환 **SQLFetchScroll**, 및와 섞여 있는 전략은 호출 **SQLBulkOperations** 또는 **SQLSetPos**합니다. 자세한 내용은 다음 섹션을 참조 하십시오. [블록 커서, 스크롤 가능 커서 및 ODBC 3.x 응용 프로그램에 대 한 이전 버전과 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)합니다.  
  
-   명명 된 매개 변수입니다.  
  
-   ODBC 3 중 하나입니다. *x*– 특정 **SQLGetInfo** 옵션입니다. (되었으면 ODBC 3입니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출을 여러 ODBC 2를 대체 한 SQL_XXX_CURSOR_ATTRIBUTES1 정보 유형. *x* 정보 유형이 정보의 일부 안정적 수 있습니다 하지만 일부 수 없습니다. 자세한 내용은 참조 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   오프셋에 바인딩하십시오.  
  
-   업데이트, 새로 고치거 나, 및 책갈피에서 삭제 (호출을 통해 **SQLBulkOperations**).  
  
-   호출 **SQLBulkOperations** 또는 **SQLSetPos** S5 상태에 있습니다.  
  
-   진단 레코드에 ROW_NUMBER 및 COLUMN_NUMBER 필드 (대체 함수에 의해 검색할 필요는 **SQLGetDiagField** 또는 **SQLGetDiagRec**).  
  
-   대략적인 행 수를 계산 합니다.  
  
-   경고 정보 (에서 SQL_ROW_SUCCESS_WITH_INFO **SQLFetchScroll**).  
  
-   가변 길이 책갈피입니다.  
  
-   매개 변수 배열에 대 한 확장된 오류 정보입니다.  
  
-   카탈로그 함수에서 반환 된 결과 집합에 새 열을 모두 합니다.  
  
-   사용 하 여 **SQLDescribeCol** 및 **SQLColAttribute** 열 0에 있습니다.  
  
-   ODBC 3 사용 되었습니다. *x*– 특정 열 특성에 대 한 호출에서 **SQLColAttribute**합니다.  
  
-   여러 환경 핸들 사용 되었습니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [ODBC 3.x 응용 프로그램의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
