---
description: ODBC 커서 라이브러리 오류 코드
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 414de02eb7145006af4faa543735888082a3d6ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466138"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 커서 라이브러리 오류 코드
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Microsoft Data Access 구성 요소에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 대신 드라이버 및 서버 커서를 사용 합니다.  
  
 ODBC 커서 라이브러리는 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)에 나열 된 것 외에 다음과 같은 sqlstates를 반환 합니다.  
  
> [!NOTE]  
>  커서 라이브러리는 상태 레코드를 정렬 하지 않습니다. 드라이버 관리자 및 ODBC 3. *x* 드라이버는 상태 레코드의 순서를 지정 합니다.  
  
|SQLSTATE|설명|다음에서 반환 될 수 있습니다.|  
|--------------|-----------------|--------------------------|  
|01000|커서를 업데이트할 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|커서 라이브러리가 사용 되지 않습니다. 로드 하지 못했습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|커서 라이브러리가 사용 되지 않습니다. 드라이버 지원이 부족 합니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|커서 라이브러리가 사용 되지 않습니다. 드라이버 관리자와 버전이 일치 하지 않습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|드라이버가 SQL_SUCCESS_WITH_INFO 반환 했습니다. 경고 메시지가 손실 되었습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|일반 오류: 파일 버퍼를 만들 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼를 읽을 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼에 쓸 수 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|일반 오류: 파일 버퍼를 닫거나 제거할 수 없습니다.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|검색 가능한 열이 바인딩 되었으므로 위치 지정 요청을 수행할 수 없습니다.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|조인 조건에서 결과 집합을 만들었기 때문에 위치 지정 요청을 수행할 수 없습니다.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|바인딩된 버퍼가 최대 세그먼트 크기를 초과 합니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|**SELECT** 문에서 결과 집합을 생성 하지 않았습니다.|**SQLGetData**|  
|SL005|**SELECT** 문에 group by 절이 포함 되어 있습니다.|**SQLGetData**|  
|SL006|매개 변수 배열은 배치 된 요청에서 지원 되지 않습니다.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|앞 으로만 이동 가능한 (버퍼링 되지 않은) 커서에서는 **SQLGetData** 를 사용할 수 없습니다.|**SQLGetData**|  
|SL009|**Sqlfetch** 또는 **sqlfetchscroll**을 호출 하기 전에 바인딩된 열이 없습니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** 는 내부 버퍼에 바인딩하는 동안 SQL_ERROR 반환 됩니다.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|문 옵션은 **Sqlfetch** 또는 **sqlfetchscroll**을 호출한 후에만 유효 합니다.|**SQLGetStmtAttr**|  
|SL012|커서가 열려 있는 동안에는 문 바인딩을 변경할 수 없습니다.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|배치 된 요청이 발급 되었지만 일부 열 개수 필드가 버퍼링 되지 않았습니다.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**Sqlfetch** 및 **sqlfetchscroll** 은 혼합할 수 없습니다.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
