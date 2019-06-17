---
title: ODBC 커서 라이브러리 오류 코드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1fb077261eda4b2e013abd6d87e894637a29216a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181234"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 커서 라이브러리 오류 코드
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Microsoft 데이터 액세스 구성 요소에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 대신, 드라이버 및 서버 커서를 사용 합니다.  
  
 ODBC 커서 라이브러리 반환에 나열 된 것 외에도 다음 SQLSTATEs [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
> [!NOTE]  
>  커서 라이브러리 상태 레코드; 순서를 지정 하지 않습니다. 드라이버 관리자와 ODBC 3입니다. *x* 드라이버 상태 레코드를 정렬 하는 것에 대 한 책임이 있습니다.  
  
|SQLSTATE|Description|반환 될 수 있습니다.|  
|--------------|-----------------|--------------------------|  
|01000|커서를 업데이트할 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|커서 라이브러리 사용 되지 않습니다. 로드 하지 못했습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|커서 라이브러리 사용 되지 않습니다. 드라이버 지원이 부족 합니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|커서 라이브러리 사용 되지 않습니다. 버전 드라이버 관리자를 사용 하 여에 일치 하지 않습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|드라이버는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 경고 메시지 손실 되었습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|일반 오류: 파일 버퍼를 만들 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼에서 읽을 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼에 쓸 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 닫거나 파일 버퍼를 제거할 수 없습니다.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|검색 가능한 열이 없는 바인딩되므로 위치 지정된 요청을 수행할 수 없습니다.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|조인 조건에 따라 결과 집합 생성 되었기 때문에 위치 지정된 요청을 수행할 수 없습니다.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|바인딩된 버퍼는 최대 세그먼트 크기를 초과합니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|결과 집합에서 생성 되지 않은 한 **선택** 문.|**SQLGetData**|  
|SL005|**선택** 문에 GROUP BY 절이 포함 됩니다.|**SQLGetData**|  
|SL006|위치 지정된 요청을 사용 하 여 매개 변수 배열은 지원 되지 않습니다.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** 정방향 전용 (섹터) 커서에서 허용 되지 않습니다.|**SQLGetData**|  
|SL009|열이 없는 호출 하기 전에 바인딩된 **SQLFetch** 하거나 **SQLFetchScroll**합니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** 내부 버퍼에 바인딩하는 동안 SQL_ERROR를 반환 합니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|문 옵션은 호출 후에 유효한 **SQLFetch** 하거나 **SQLFetchScroll**합니다.|**SQLGetStmtAttr**|  
|SL012|커서가 열려 있는 동안 문의 바인딩을 변경할 수 있습니다.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|위치 지정된 요청을 발행 하 고 모든 열 수가 필드가 버퍼링 된 키를 누릅니다.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** 하 고 **SQLFetchScroll** 혼합할 수 없습니다.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
