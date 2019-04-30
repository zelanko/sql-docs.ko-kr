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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 875348a501c292e55b267ece769f16dd6bc9dbdd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270942"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>지원되는 커서 모델(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버를 지 원하는 둘 다 *블록* (*행 집합*) 및 *정적* 커서입니다. 정적 커서는 수준 1 ODBC 준수에 따르는 모든 드라이버에 대 한 지원. 드라이버를 동적으로 키 집합 기반 또는 혼합 (키 집합 및 동적)를 지원 하지 않습니다 커서입니다.  
  
 응용 프로그램에서 호출할 수 있습니다 [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CURSOR_FORWARD_ONLY (블록 커서) 또는 SQL_CURSOR_STATIC (정적 커서)에서는 SQL_CURSOR_TYPE 옵션을 사용 하 여 합니다.  
  
> [!NOTE]  
>  호출 하는 경우 **SQLSetStmtOption** 함수 SQL_CURSOR_FORWARD_ONLY 또는 SQL_CURSOR_STATIC 이외의에서는 SQL_CURSOR_TYPE 옵션을 사용 하 여 01S02의 sqlstate는 SQL_SUCCESS_WITH_INFO를 반환 합니다 (옵션 값이 변경 됨). 드라이버는 SQL_CURSOR_STATIC를 모두 지원 되지 않는 커서 모드를 설정합니다.  
  
 및에 대 한 커서 유형에 대 한 자세한 내용은 **SQLSetStmtOption**를 참조 합니다 [ODBC 프로그래머 참조](../../odbc/reference/odbc-programmer-s-reference.md)합니다.  
  
## <a name="block-cursor"></a>블록 커서(block cursor)  
 정방향 스크롤, 읽기 전용 결과 집합 데이터에 대 한 저장소를 유지 관리 책임이 있는 클라이언트에 반환 합니다.  
  
## <a name="static-cursor"></a>정적 커서(static cursor)  
 쿼리에 정의 된 데이터 집합이 사용 되는 스냅숏. 정적 커서는 다른 사용자가 기본 데이터의 실시간 변경 내용을 반영 하지 않습니다. 커서의 메모리 버퍼는 ODBC 커서 라이브러리를 앞뒤로 스크롤할 수 있도록 하 여 유지 관리 됩니다.  
  
## <a name="rowset"></a>행 집합(rowset)  
 데이터 원본에서 검색 되는 행을 나타내는 커서에 저장 된 데이터 블록입니다.
