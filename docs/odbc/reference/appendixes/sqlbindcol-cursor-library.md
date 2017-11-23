---
title: "SQLBindCol (커서 라이브러리) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf80a3dfd02c2871267cfe57f1b95ae246094bc9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLBindCol** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLBindCol**, 참조 [SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
 응용 프로그램에서 현재 행 집합을 반환 하는 커서 라이브러리에 대 한 하나 이상의 버퍼를 할당 합니다. 호출 **SQLBindCol** 한 번 이상 이러한 버퍼는 결과 집합에 바인딩할 합니다.  
  
 응용 프로그램에서 호출할 수 **SQLBindCol** 호출한 후 집합 열에 결과 다시 바인딩하려면 **SQLExtendedFetch**, **SQLFetch**, 또는 **SQLFetchScroll**로 C 데이터 형식, 열 크기 및 연결된 된 필드의 10 진수 동일 하 게 유지 합니다. 응용 프로그램 서로 다른 주소에는 열을 바인딩할 커서를 닫지 필요 합니다.  
  
 커서 라이브러리 지원 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 바인딩 오프셋을 사용 하도록 설정 합니다. (**SQLBindCol** 되려면 리바인딩이 대해 호출할 필요는 없습니다.) ODBC 3 커서 라이브러리 사용 됩니다*.x* 드라이버를 바인딩 오프셋이 잘못 되었습니다. 경우에 사용 **SQLFetch** 호출 됩니다. Bind 오프셋 하는 경우 사용 됩니다 **SQLFetch** 커서 라이브러리는 ODBC 2 함께 사용할 때 호출 됩니다. *x* 드라이버 때문에 **SQLFetch** 에 **SQLExtendedFetch**합니다.  
  
 커서 라이브러리 호출을 지 원하는 **SQLBindCol** 책갈피 열을 바인딩할 합니다.  
  
 ODBC 2 작업할 때는. *x* 드라이버 커서 라이브러리 반환 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이) 때 **SQLBindCol** 4 같지 않은 값으로 책갈피 열에 대 한 버퍼 길이 설정 하기 위해 호출 됩니다. ODBC 3 작업할 때*.x* 드라이버 커서 라이브러리의 규모에 버퍼를 허용 합니다.
