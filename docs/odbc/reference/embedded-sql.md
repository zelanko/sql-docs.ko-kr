---
title: SQL 포함 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47936b5c085514fca4ecc1c81057ef78a19f05c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628466"
---
# <a name="embedded-sql"></a>Embedded SQL
DBMS SQL 문을 보내기 위한 첫 번째 방법은 포함 된 SQL입니다. SQL 변수 및 흐름 제어 문을 사용 하지 않으므로, C 등 COBOL 기존의 프로그래밍 언어로 작성 된 프로그램에 추가할 수 있는 데이터베이스 하위 언어와 자주 사용 됩니다. Embedded SQL에 대 한 중앙 아이디어입니다: 프로그래밍 언어는 호스트에서 작성 된 프로그램에서 SQL 문을 배치 합니다. 요약 하자면, 다음과 같은 기술은 호스트 언어의 SQL 문을 포함 하는 데 사용 됩니다.  
  
-   포함 된 SQL 문은 한 특수 SQL 다르거나에 의해 처리 됩니다. 모든 SQL 문에 도입부 시작 및 SQL 문을 프리 플래그는 둘 다, 종결자와 함께 종료 합니다. 유도 자와 종결자 호스트 언어를 사용 하 여 달라 집니다. 예를 들어의 도입부는 c에서 "EXEC SQL" 및 "& SQL (" MUMPS에서 종결자는 세미콜론 (;) 및 C 및 MUMPS에서 오른쪽 괄호를.  
  
-   상수를 사용할 수 있는 위치에 포함 된 SQL 문에서 호스트 변수 라고 하는 응용 프로그램에서 변수를 사용할 수 있습니다. 이러한 SQL 문을 쿼리 결과를 받는 출력 및 특정 상황에 맞게 입력에 사용할 수 있습니다.  
  
-   단일 SELECT 문을;를 사용 하 여 데이터의 단일 행을 반환 하는 쿼리 처리 이 문은 쿼리 및 데이터를 반환 하는 호스트 변수 모두를 지정 합니다.  
  
-   여러 데이터 행을 반환 하는 쿼리는 커서를 사용 하 여 처리 됩니다. 커서는 결과 집합의 현재 행을 추적 합니다. 쿼리를 정의 하는 DECLARE CURSOR 문에, OPEN 문을 쿼리 처리를 시작, FETCH 문이 데이터의 연속 된 행을 검색 및 CLOSE 문은 쿼리 처리를 종료 합니다.  
  
-   커서 열기 이지만, 현재 위치 업데이트 및 위치 지정된 delete 문을 사용할 수 있습니다 업데이트 하거나 커서에서 현재 선택한 행을 삭제 하려면.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Embedded SQL 예제](../../odbc/reference/embedded-sql-example.md)  
  
-   [Embedded SQL 프로그램 컴파일](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [정적 SQL](../../odbc/reference/static-sql.md)  
  
-   [동적 SQL](../../odbc/reference/dynamic-sql.md)
