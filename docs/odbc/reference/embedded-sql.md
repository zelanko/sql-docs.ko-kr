---
title: "SQL 포함 | Microsoft Docs"
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
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12d0e4edc34ceb02f9b902016eb82b489c4ca71d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="embedded-sql"></a>Embedded SQL
DBMS SQL 문을 보내기 위한 첫 번째 방법을 포함 된 SQL입니다. SQL 변수 및 흐름 제어 문을 사용 하지 않으므로, C 또는 COBOL 등 기존의 프로그래밍 언어로 작성 된 프로그램에 추가할 수 있는 데이터베이스 하위 언어와 자주 사용 됩니다. 이것은 포함 된 SQL의 중심 아이디어: 호스트 프로그래밍 언어로 작성 된 프로그램에서 SQL 문을 배치 합니다. 간단히 말해서 다음 기술 호스트 언어의 SQL 문을 포함 하는 데 사용 됩니다.  
  
-   포함 된 SQL 문 특수 SQL 프리에 의해 처리 됩니다. 모든 SQL 문을 유도로 시작 하 고 프리에 대 한 SQL 문을 플래그를 지정 하는 종결자로 끝나야 합니다. 유도 자와 종결자 호스트 언어에 따라 다릅니다. 예를 들어는 유도 "EXEC SQL" c에서 및 "& SQL (" MUMPS에 종결자는 세미콜론 (;) 및 C와 MUMPS에 오른쪽 괄호입니다.  
  
-   상수를 사용할 수 있는 위치에 포함 된 SQL 문에서 호스트 변수, 호출 응용 프로그램에서 변수를 사용할 수 있습니다. 이러한 SQL 문을 쿼리 결과를 받는 출력와 특정 상황에 맞게 입력에 사용할 수 있습니다.  
  
-   단일 SELECT 문을; 하 여 데이터의 단일 행을 반환 하는 쿼리 처리 이 문은 쿼리 및 데이터를 반환 하는 호스트 변수 모두를 지정 합니다.  
  
-   여러 데이터 행을 반환 하는 쿼리는 커서와 함께 처리 됩니다. 커서는 결과 집합 내에서 현재 행을 추적 합니다. 쿼리를 정의 하는 DECLARE CURSOR 문에, OPEN 문을 쿼리 처리를 시작, 연속 된 행의 데이터를 검색 하는 FETCH 문이 및 CLOSE 문은 쿼리 처리를 종료 합니다.  
  
-   커서가 열려 있는 동안 위치 지정된 update 및 위치 지정된 delete 문을 사용할 수를 업데이트 하거나 커서에서 현재 선택 된 행을 삭제 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Embedded SQL 예제](../../odbc/reference/embedded-sql-example.md)  
  
-   [Embedded SQL 프로그램 컴파일](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [정적 SQL](../../odbc/reference/static-sql.md)  
  
-   [동적 SQL](../../odbc/reference/dynamic-sql.md)
