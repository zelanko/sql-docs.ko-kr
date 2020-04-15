---
title: 새로운 기능 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302401"
---
# <a name="new-features"></a>새로운 기능
ODBC *3.x에*다음과 같은 새로운 기능이 도입되었습니다. ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램은 이 기능을 사용할 수 없습니다. ODBC *3.x* 드라이버 관리자는 ODBC *2.x* 드라이버로 작업할 때 이러한 기능을 매핑하지 않습니다.  
  
-   설명자 핸들을 인수로 하는 함수: **SQLSetDescField,** **SQLGetDescField,** **SQLSetDescRec,** **SQLGetDescRec**및 **SQLCopyDesc**.  
  
-   함수 **SQLSetEnvAttr** 및 **SQLGetEnvAttr**.  
  
-   **SQLAllocHandle을** 사용하여 설명자 핸들을 할당합니다. (환경, 연결 및 명령문 핸들을 할당하기 위해 **SQLAllocHandle을** 사용하는 것은 새로운 기능이 아니라 중복됩니다.)  
  
-   **SQLGetConnectAttr을** 사용하여 SQL_ATTR_AUTO_IPD 연결 특성을 가져옵니다. **(SQLSetConnectAttr를** 사용하여 설정하고 **SQLGetConnectAttr을** 사용하여 다른 연결 특성을 얻는 것은 새로운 기능이 아닌 중복됩니다.)  
  
-   **SQLSetStmtAttr을** 사용하여 설정하고 **SQLGetStmtAttr을** 사용하여 다음 문 특성을 가져옵니다. **(SQLSetStmtAttr을** 사용하여 설정하고 **SQLGetStmtAttr을** 사용하여 다른 문 특성을 얻으면 다른 문 특성이 복제되고 새 기능이 아닙니다.)  
  
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
  
-   다음 문 특성을 얻기 위해 **SQLGetStmtAttr을** 사용합니다. (다른 문 특성을 얻기 위해 **SQLGetStmtAttr을** 사용하는 것은 새로운 기능이 아닌 중복 된 기능입니다.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   간격 C 데이터 형식, 간격 SQL 데이터 형식, BIGINT C 데이터 형식 및 SQL_C_NUMERIC 데이터 구조의 사용입니다.  
  
-   매개 변수의 행 별 바인딩입니다.  
  
-   SQL_FETCH_BOOKMARK *FetchOrientation* 인수로 **SQLFetchScroll를** 호출하고 0이 아닌 오프셋을 지정하는 것과 같은 오프셋 기반 책갈피 인출.  
  
-   **SQLFetch** 는 행 상태 배열, 가져온 행 수, 여러 행 가져오기, **SQLFetchScroll와**의 호출 혼합 및 **SQLBulkOperations** 또는 **SQLSetPos와의**상호 혼합 을 반환합니다. 자세한 내용은 ODBC 3.x 응용 프로그램에 대한 다음 섹션, [커서 블록, 스크롤 가능한 커서 및 이전 버전과의 호환성을](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)참조하십시오.  
  
-   명명된 매개 변수입니다.  
  
-   ODBC *3.x-특정* **SQLGetInfo** 옵션 중 어느 것이든. ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 여러 ODBC *2.x* 정보 유형을 대체한 SQL_XXX_CURSOR_ATTRIBUTES1 정보 형식을 호출하는 경우 일부 정보는 신뢰할 수 있지만 일부는 신뢰할 수 없을 수 있습니다. 자세한 내용은 [SQLGetInfo를](../../../odbc/reference/syntax/sqlgetinfo-function.md)참조하십시오.  
  
-   오프셋을 바인딩합니다.  
  
-   **SQLBulkOperations에**대한 호출을 통해 책갈피별로 업데이트, 새로 고침 및 삭제합니다.  
  
-   S5 상태에서 **SQLBulkOperations** 또는 **SQLSetPos를** 호출합니다.  
  
-   진단 레코드의 ROW_NUMBER 및 COLUMN_NUMBER **필드(SQLGetDiagField** 또는 **SQLGetDiagRec)를**대체 함수로 검색해야 합니다.  
  
-   대략적인 행 개수입니다.  
  
-   경고 **정보(SQLFetchScroll의**SQL_ROW_SUCCESS_WITH_INFO).  
  
-   가변 길이 책갈피.  
  
-   매개 변수 배열에 대한 확장된 오류 정보입니다.  
  
-   카탈로그 함수에서 반환되는 결과 집합의 모든 새 열입니다.  
  
-   열 0에서 **SQLDescribeCol** 및 **SQLColAttribute** 사용.  
  
-   **SQLColAttribute**에 대한 호출에서 ODBC *3.x-특정*열 특성사용  
  
-   여러 환경 핸들 사용.  
  
 이 섹션에는 다음 항목이 포함되어 있습니다.  
  
-   [ODBC 3.x 애플리케이션의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
