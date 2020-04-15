---
title: ODBC 커서 라이브러리 오류 코드 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c263ce53c41546e63dc2a830d3db3b903e2e3515
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301434"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 커서 라이브러리 오류 코드
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Microsoft 데이터 액세스 구성 요소에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 대신 드라이버 및 서버 커서를 사용합니다.  
  
 ODBC 커서 라이브러리는 [ODBC API 참조에](../../../odbc/reference/syntax/odbc-api-reference.md)나열된 SQLSTAT및 다음 SQLSTATEs를 반환합니다.  
  
> [!NOTE]  
>  커서 라이브러리는 상태 레코드를 정렬하지 않습니다. 드라이버 관리자 및 ODBC 3. *x* 드라이버는 상태 레코드를 주문할 책임이 있습니다.  
  
|SQLSTATE|설명|에서 반환할 수 있습니다.|  
|--------------|-----------------|--------------------------|  
|01000|커서는 업데이터 로 처리되지 않습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|커서 라이브러리가 사용되지 않습니다. 로드에 실패했습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|커서 라이브러리가 사용되지 않습니다. 드라이버 지원이 부족합니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|커서 라이브러리가 사용되지 않습니다. 드라이버 관리자와 버전 불일치.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|드라이버가 SQL_SUCCESS_WITH_INFO 돌아왔습니다. 경고 메시지가 손실되었습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|일반 오류: 파일 버퍼를 만들 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼에서 읽을 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼에 쓸 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼를 닫거나 제거할 수 없습니다.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|검색 가능한 열이 바인딩되지 않으므로 위치 지정 요청을 수행할 수 없습니다.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|조인 조건에 의해 결과 집합이 만들어졌기 때문에 위치 지정 요청을 수행할 수 없습니다.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|바인딩된 버퍼가 최대 세그먼트 크기를 초과합니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|**SELECT** 문에 의해 결과 집합이 생성되지 않았습니다.|**SQLGetData**|  
|SL005|**SELECT** 문에는 GROUP BY 절이 포함되어 있습니다.|**SQLGetData**|  
|SL006|매개 변수 배열은 위치 가 있는 요청에서 지원되지 않습니다.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData는** 정방향 전용(버퍼링되지 않은) 커서에서는 허용되지 않습니다.|**SQLGetData**|  
|SL009|SQLFetch 또는 **SQLFetchScroll** 을 호출하기 전에 는 열이 바인딩되지 **않았습니다.**|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol내부** 버퍼에 바인딩하는 동안 SQL_ERROR 반환했습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|명령문 옵션은 **SQLFetch** 또는 **SQLFetchScroll**을 호출한 후에만 유효합니다.|**SQLGetStmtAttr**|  
|SL012|커서가 열려 있는 동안에는 문 바인딩을 변경할 수 없습니다.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|위치 가 있는 요청이 발급되었으며 모든 열 개수 필드가 버퍼링되지 는 않습니다.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** 및 **SQLFetch스크롤을** 혼합할 수 없습니다.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
