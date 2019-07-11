---
title: 새로운 기능 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4582a99797d5f6035f6d5d639514c5a6fdd572d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794062"
---
# <a name="new-features"></a>새로운 기능
ODBC에는 다음과 같은 새 기능이 도입 되었습니다 *3.x*합니다. ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *2.x* 드라이버는이 기능을 사용할 수 없습니다. ODBC *3.x* ODBC를 사용 하 여 작업할 때 드라이버 관리자에서는 이러한 기능을 매핑하지 않습니다 *2.x* 드라이버입니다.  
  
-   설명자를 사용 하는 함수의 인수로 서 처리 합니다. **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**, and **SQLCopyDesc**.  
  
-   함수 **SQLSetEnvAttr** 하 고 **SQLGetEnvAttr**합니다.  
  
-   사용 **SQLAllocHandle** 설명자 핸들을 할당 합니다. (사용 **SQLAllocHandle** 환경, 연결 및 문 핸들을 할당 하는 중복, 신규가 아닌 기능입니다.)  
  
-   사용 **SQLGetConnectAttr** SQL_ATTR_AUTO_IPD 연결 특성을 가져옵니다. (사용 **SQLSetConnectAttr** 을 설정 하려면 및 **SQLGetConnectAttr** 다른 연결 특성은 중복, 신규가 아닌 기능을 합니다.)  
  
-   사용 **SQLSetStmtAttr** 을 설정 하려면 및 **SQLGetStmtAttr** 다음 문 특성을 가져올 수 있습니다. (사용 **SQLSetStmtAttr** 을 설정 하려면 및 **SQLGetStmtAttr** 다른 문 특성은 중복, 신규가 아닌 기능을 합니다.)  
  
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
  
-   사용 **SQLGetStmtAttr** 다음 문 특성을 가져옵니다. (사용 **SQLGetStmtAttr** get 다른 문 특성은 중복된 기능을 하지 새로운 기능입니다.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   C 간격 데이터 형식, 간격 SQL 데이터 형식, BIGINT C 데이터 형식 및 SQL_C_NUMERIC 데이터 구조를 사용 합니다.  
  
-   매개 변수의 행 단위 바인딩입니다.  
  
-   호출 등의 오프셋 기반 책갈피 인출 **SQLFetchScroll** 사용 하 여를 *FetchOrientation* SQL_FETCH_BOOKMARK 및 0이 아닌 오프셋을 지정 하는 인수입니다.  
  
-   **SQLFetch** 행 상태 배열이 여러 행을 사용 하 여 섞여 있는 전략은 호출을 가져오는 중에 인출 된 행 수를 반환 **SQLFetchScroll**를 사용 하 여 섞여 있는 전략은 호출 **SQLBulkOperations** 또는 **SQLSetPos**합니다. 자세한 내용은 다음 섹션을 참조 하세요 [블록 커서, 스크롤 가능 커서 및 ODBC 3.x 응용 프로그램에 대 한 이전 버전과 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)합니다.  
  
-   명명 된 매개 변수입니다.  
  
-   모든 ODBC *3.x*-특정 **SQLGetInfo** 옵션입니다. (경우 ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *2.x* 드라이버는 여러 ODBC 대체가 SQL_XXX_CURSOR_ATTRIBUTES1 정보 유형, 호출 *2.x* 정보 유형 정보 중 일부 수도 신뢰할 수 있지만 일부 수 없습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   오프셋을 바인딩하십시오.  
  
-   업데이트, 새로 고침, 및 책갈피에서 삭제 (호출을 통해 **SQLBulkOperations**).  
  
-   호출 **SQLBulkOperations** 하거나 **SQLSetPos** S5 상태에서입니다.  
  
-   진단 레코드의 ROW_NUMBER와 COLUMN_NUMBER 필드 (대체 함수에 의해 검색할 수 있는 **SQLGetDiagField** 하거나 **SQLGetDiagRec**).  
  
-   대략적인 행 개수입니다.  
  
-   경고 정보 (에서 SQL_ROW_SUCCESS_WITH_INFO **SQLFetchScroll**).  
  
-   가변 길이 책갈피입니다.  
  
-   매개 변수 배열에 대 한 확장된 오류 정보입니다.  
  
-   카탈로그 함수에서 반환한 결과 집합에 새 열을 모두 합니다.  
  
-   사용 **SQLDescribeCol** 하 고 **SQLColAttribute** 0 열에 있습니다.  
  
-   ODBC 활용 *3.x*-에 대 한 호출에서 특정 열 특성 **SQLColAttribute**합니다.  
  
-   여러 환경 핸들을 사용 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [ODBC 3.x 애플리케이션의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
