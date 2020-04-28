---
title: 새 기능 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b40803dac6c9f296043a8dcac50f9bc69036875a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302401"
---
# <a name="new-features"></a>새 기능
ODBC 3.x에는 다음과 같은 새로운 기능이 도입 *되었습니다.* Odbc 2.x 드라이버를 사용 하 여 작업 하는 *odbc* *2.x 응용 프로그램* 은이 기능을 사용할 수 없습니다. Odbc 3.x *드라이버 관리자* *는 odbc 2.x* 드라이버로 작업할 때 이러한 기능을 매핑하지 않습니다.  
  
-   **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**및 **sqlcopydesc**라는 인수로 설명자 핸들을 사용 하는 함수입니다.  
  
-   **SQLSetEnvAttr** 및 **SQLGetEnvAttr**함수  
  
-   **SQLAllocHandle** 를 사용 하 여 설명자 핸들을 할당 합니다. 환경, 연결 및 문 핸들을 할당 하는 데 **SQLAllocHandle** 를 사용 하는 것은 새로운 기능이 아니라 중복 됩니다.  
  
-   **SQLGetConnectAttr** 를 사용 하 여 SQL_ATTR_AUTO_IPD 연결 특성을 가져옵니다. ( **SQLSetConnectAttr** 를 설정 하 고 **SQLGetConnectAttr** 를 사용 하는 경우 다른 연결 특성은 새로운 기능이 아니라 중복 됩니다.)  
  
-   **SQLSetStmtAttr** 를 사용 하 여를 설정 하 고 **SQLGetStmtAttr** 를 사용 하 여 다음 문 특성을 가져옵니다. ( **SQLSetStmtAttr** 를 설정 하 고 **SQLGetStmtAttr** 를 사용 하는 경우 다른 문 특성은 새로운 기능이 아니라 중복 됩니다.)  
  
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
  
-   **SQLGetStmtAttr** 를 사용 하 여 다음 문 특성을 가져옵니다. **SQLGetStmtAttr** 를 사용 하 여 다른 문 특성을 가져오는 것은 새로운 기능이 아니라 중복 된 기능입니다.  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   간격 C 데이터 형식, 간격 SQL 데이터 형식, BIGINT C 데이터 형식 및 SQL_C_NUMERIC 데이터 구조를 사용 합니다.  
  
-   매개 변수의 행 단위 바인딩입니다.  
  
-   SQL_FETCH_BOOKMARK의 *Fetchorientation* 인수를 사용 하 여 **sqlfetchscroll** 을 호출 하 고 0이 아닌 오프셋을 지정 하 여 오프셋 기반 책갈피를 페치합니다.  
  
-   **Sqlfetch** -행 상태 배열을 반환 하 고, 인출 된 행 수를 가져오고, 여러 행을 가져오고, **sqlfetchscroll**을 사용 하 여 호출을 결합 하 고, **SQLBulkOperations** 또는 **SQLSetPos**를 사용 하 여 혼용 호출 자세한 내용은 다음 섹션인 [ODBC 3.X 응용 프로그램의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)을 참조 하세요.  
  
-   명명 된 매개 변수입니다.  
  
-   ODBC 2.x 특정 **SQLGetInfo** 옵션 *입니다.* Odbc 2.x 드라이버를 사용 하 여 작업 하 *는 odbc* *2.x 응용 프로그램* 에서 여러 ODBC 2.x 정보 유형을 대체 한 SQL_XXX_CURSOR_ATTRIBUTES1 정보 유형을 호출 하는 경우 *일부 정보는* 신뢰할 수 있지만 일부는 신뢰할 수 없는 것일 수 있습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)를 참조 하세요.)  
  
-   오프셋을 바인딩합니다.  
  
-   **SQLBulkOperations**호출을 통해 책갈피를 통해 업데이트, 새로 고침 및 삭제  
  
-   S5 상태에서 **SQLBulkOperations** 또는 **SQLSetPos** 를 호출 합니다.  
  
-   진단 레코드의 ROW_NUMBER 및 COLUMN_NUMBER 필드 (대체 함수 **SQLGetDiagField** 또는 **SQLGetDiagRec**에서 검색 해야 하는)  
  
-   대략적인 행 개수입니다.  
  
-   경고 정보 ( **Sqlfetchscroll**의 SQL_ROW_SUCCESS_WITH_INFO)  
  
-   가변 길이 책갈피입니다.  
  
-   매개 변수 배열에 대 한 확장 오류 정보입니다.  
  
-   카탈로그 함수에서 반환 하는 결과 집합의 모든 새 열입니다.  
  
-   열 0에 **SQLDescribeCol** 및 **sqlcolattribute** 를 사용 합니다.  
  
-   **Sqlcolattribute**호출에서 ODBC *3(sp3)* 의 특정 열 특성을 사용 합니다.  
  
-   여러 환경 핸들을 사용 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [ODBC 3.x 애플리케이션의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
