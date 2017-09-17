---
title: "커서 모델 (Visual FoxPro ODBC 드라이버)를 지원 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b80cb7cbbea13dbc6d491d757f28d44d5fda1ea6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>지원 되는 커서 모델 (Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버는 둘 다 지원 *블록* (*행 집합*) 및 *정적* 커서입니다. 정적 커서는 수준 1 ODBC 규정 준수에 맞는 모든 드라이버에 대 한 지원 됩니다. 드라이버는 동적으로 키 집합 기반 또는 혼합 (키 집합 및 동적)를 지원 하지 않습니다 커서입니다.  
  
 응용 프로그램에서 호출할 수 [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CURSOR_FORWARD_ONLY (블록 커서) 또는 SQL_CURSOR_STATIC (정적 커서)에서는 SQL_CURSOR_TYPE 옵션을 사용 합니다.  
  
> [!NOTE]  
>  호출 하는 경우 **SQLSetStmtOption** 함수 SQL_CURSOR_FORWARD_ONLY 또는 SQL_CURSOR_STATIC 이외의에서는 SQL_CURSOR_TYPE 옵션을 01 s 02의 sqlstate는 SQL_SUCCESS_WITH_INFO를 반환 합니다 (옵션 값이 변경 됨). 드라이버는 SQL_CURSOR_STATIC를 모든 지원 되지 않는 커서 모드를 설정합니다.  
  
 및에 대 한 커서 유형에 대 한 자세한 내용은 **SQLSetStmtOption**, 참조는 [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md)합니다.  
  
## <a name="block-cursor"></a>블록 커서(block cursor)  
 데이터에 대 한 저장소를 유지 관리 책임이 있는 클라이언트에 반환 하는 정방향 스크롤, 읽기 전용 결과 집합입니다.  
  
## <a name="static-cursor"></a>정적 커서(static cursor)  
 쿼리에 의해 정의 된 데이터 집합의 스냅숏. 정적 커서는 다른 사용자가 기본 데이터의 실시간 변경 사항은 반영 하지 않습니다. 커서의 메모리 버퍼 앞뒤로 스크롤할 수 있도록 하는 ODBC 커서 라이브러리에서 유지 관리 됩니다.  
  
## <a name="rowset"></a>행 집합(rowset)  
 데이터 원본에서 검색 된 행 수를 나타내는 커서에 저장 된 데이터를 차단 합니다.
