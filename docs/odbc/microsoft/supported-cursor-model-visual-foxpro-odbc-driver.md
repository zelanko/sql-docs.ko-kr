---
title: 지원 되는 커서 모델 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf3400f24e20a8fa864404612bf07ea44efce49e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301129"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>지원되는 커서 모델(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버는 *블록* (*행 집합*) 및 *정적* 커서를 모두 지원 합니다. 정적 커서는 수준 1 ODBC 준수를 준수 하는 모든 드라이버에 대해 지원 됩니다. 드라이버는 동적, 키 집합 기반 또는 혼합 (키 집합 및 동적) 커서를 지원 하지 않습니다.  
  
 응용 프로그램은 SQL_CURSOR_FORWARD_ONLY (블록 커서) 또는 SQL_CURSOR_STATIC (정적 커서)의 SQL_CURSOR_TYPE 옵션을 사용 하 여 [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 를 호출할 수 있습니다.  
  
> [!NOTE]  
>  SQL_CURSOR_FORWARD_ONLY 또는 SQL_CURSOR_STATIC 이외의 SQL_CURSOR_TYPE 옵션을 사용 하 여 **SQLSetStmtOption** 를 호출 하는 경우이 함수는 01 S 02의 SQLSTATE를 사용 하 여 SQL_SUCCESS_WITH_INFO을 반환 합니다 (옵션 값이 변경 됨). 드라이버가 지원 되지 않는 모든 커서 모드를 SQL_CURSOR_STATIC 설정 합니다.  
  
 커서 유형 및 **SQLSetStmtOption**에 대 한 자세한 내용은 [ODBC 프로그래머 참조](../../odbc/reference/odbc-programmer-s-reference.md)를 참조 하세요.  
  
## <a name="block-cursor"></a>블록 커서(block cursor)  
 클라이언트에 반환 된 앞으로 스크롤 하는 읽기 전용 결과 집합으로, 데이터에 대 한 저장소를 유지 관리 하는 역할을 담당 합니다.  
  
## <a name="static-cursor"></a>정적 커서(static cursor)  
 쿼리로 정의 된 데이터 집합의 스냅숏입니다. 정적 커서는 다른 사용자가 기본 데이터를 실시간으로 변경 하는 것을 반영 하지 않습니다. 커서의 메모리 버퍼는 ODBC 커서 라이브러리에 의해 유지 관리 되므로 앞으로 스크롤할 수 있습니다.  
  
## <a name="rowset"></a>행 집합(rowset)  
 데이터 원본에서 검색 된 행을 나타내는 커서에 저장 된 데이터 블록입니다.
