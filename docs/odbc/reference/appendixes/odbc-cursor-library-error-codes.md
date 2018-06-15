---
title: ODBC 커서 라이브러리 오류 코드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26469f2d439c032b1d4f5f377cc9aab4a4189fae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913908"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 커서 라이브러리 오류 코드
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Microsoft 데이터 액세스 구성 요소에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 대신, 드라이버 및 서버 커서를 사용 합니다.  
  
 ODBC 커서 라이브러리에 나열 된 권한과 함께 다음 SQLSTATEs 반환 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
> [!NOTE]  
>  커서 라이브러리 상태 레코드; 순서를 지정 하지 않습니다. 드라이버 관리자와 ODBC 3입니다. *x* 드라이버는 상태 레코드 순서를 지정 합니다.  
  
|SQLSTATE|Description|반환 될 수 있습니다.|  
|--------------|-----------------|--------------------------|  
|01000|커서를 업데이트할 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|커서 라이브러리 사용 되지 않습니다. 로드 하지 못했습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|커서 라이브러리 사용 되지 않습니다. 드라이버 지원이 부족 합니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|커서 라이브러리 사용 되지 않습니다. 버전 드라이버 관리자를 사용 하 여에 일치 하지 않습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|드라이버는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 경고 메시지가 손실 되었습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|일반 오류: 파일 버퍼를 만들 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼에서 읽을 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼에 쓸 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 닫습니다 하거나 파일 버퍼를 제거할 수 없습니다.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|검색 가능한 열이 없는 바인딩되므로 위치 지정된 요청을 수행할 수 없습니다.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|조인 조건에 따라 결과 집합을 만들었기 때문에 위치 지정된 요청을 수행할 수 없습니다.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|바인딩된 버퍼는 최대 세그먼트 크기를 초과합니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|결과 집합에서 생성 되지 않은 한 **선택** 문.|**SQLGetData**|  
|SL005|**선택** 문에 GROUP BY 절을 포함 합니다.|**SQLGetData**|  
|SL006|위치 지정 요청 매개 변수 배열은 지원 되지 않습니다.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** 앞 으로만 이동 가능한 (버퍼링 되지 않은) 커서에서 허용 되지 않습니다.|**SQLGetData**|  
|SL009|열이 없으면 호출 하기 전에 바인딩된 **SQLFetch** 또는 **SQLFetchScroll**합니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** 을 내부 버퍼에 바인딩하는 동안 SQL_ERROR를 반환 합니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|문 옵션은 호출한 후에 유효 **SQLFetch** 또는 **SQLFetchScroll**합니다.|**SQLGetStmtAttr**|  
|SL012|커서가 열려 있는 동안 문 바인딩은 변경할 수 있습니다.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|위치 지정된 요청을 실행 하 고 모든 열 count 필드가 버퍼링 된 키를 누릅니다.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** 및 **SQLFetchScroll** 혼합할 수 없습니다.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
