---
title: 지원되는 커서 모델(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301129"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>지원되는 커서 모델(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버는 *블록(행* *집합)과* *정적* 커서를 모두 지원합니다. 정적 커서는 레벨 1 ODBC 준수를 준수하는 모든 드라이버에 대해 지원됩니다. 드라이버는 동적 키 집합 기반 또는 혼합(키 집합 및 동적) 커서를 지원하지 않습니다.  
  
 응용 프로그램은 SQL_CURSOR_FORWARD_ONLY(블록 커서) 또는 SQL_CURSOR_STATIC(정적 커서)의 SQL_CURSOR_TYPE 옵션을 사용 하 고 [SQLSetStmtOption을](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 호출할 수 있습니다.  
  
> [!NOTE]  
>  SQL_CURSOR_FORWARD_ONLY 또는 SQL_CURSOR_STATIC 이외의 SQL_CURSOR_TYPE 옵션으로 **SQLSetStmtOption을** 호출하면 함수는 01S02의 SQLSTATE(옵션 값이 변경된)를 SQL_SUCCESS_WITH_INFO 반환합니다. 드라이버는 지원되지 않는 모든 커서 모드를 SQL_CURSOR_STATIC 설정합니다.  
  
 커서 유형 및 **SQLSetStmtOption에**대한 자세한 내용은 [ODBC 프로그래머의 참조를](../../odbc/reference/odbc-programmer-s-reference.md)참조하십시오.  
  
## <a name="block-cursor"></a>블록 커서(block cursor)  
 데이터 저장소를 유지 관리하는 클라이언트에 전달 스크롤전용 결과 집합이 반환됩니다.  
  
## <a name="static-cursor"></a>정적 커서(static cursor)  
 쿼리에 의해 정의된 데이터 집합의 스냅숏입니다. 정적 커서는 다른 사용자가 기본 데이터의 실시간 변경 내용을 반영하지 않습니다. 커서의 메모리 버퍼는 ODBC 커서 라이브러리에 의해 유지관리되어 앞으로 스크롤할 수 있습니다.  
  
## <a name="rowset"></a>행 집합(rowset)  
 데이터 원본에서 검색된 행을 나타내는 커서에 저장된 데이터 블록입니다.
