---
title: 임베디드 SQL | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ad6fd2753d026f026d72a7aa8f68d5d48ce03cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306676"
---
# <a name="embedded-sql"></a>Embedded SQL
DBMS에 SQL 문을 보내는 첫 번째 기술은 임베디드 SQL입니다. SQL은 변수 및 흐름 제어 문을 사용하지 않으므로 C 또는 COBOL과 같은 기존 프로그래밍 언어로 작성된 프로그램에 추가할 수 있는 데이터베이스 하위 언어로 자주 사용됩니다. 이것은 호스트 프로그래밍 언어로 작성된 프로그램에 SQL 문을 배치하는 임베디드 SQL의 핵심 개념입니다. 간단히 말해서 다음 기술은 호스트 언어로 SQL 문을 포함합니다.  
  
-   포함된 SQL 문은 특수 SQL 사전 컴파일러에 의해 처리됩니다. 모든 SQL 문은 소개자로 시작하여 종료자로 끝나며, 둘 다 사전 컴파일러에 대한 SQL 문에 플래그를 표시합니다. 소개자 및 종사자는 호스트 언어에 따라 다릅니다. 예를 들어 소개자는 C의 "EXEC SQL"이고 MUMPS의 "&SQL(")"이며 종료자는 세미콜론(;) C와 MUMPS의 오른쪽 괄호안에 있습니다.  
  
-   호스트 변수라고 하는 응용 프로그램 프로그램의 변수는 허용되는 모든 위치에서 포함된 SQL 문에서 사용할 수 있습니다. 입력에서 SQL 문을 특정 상황에 맞게 조정하고 출력에서 쿼리 결과를 수신하는 데 사용할 수 있습니다.  
  
-   단일 데이터 행을 반환하는 쿼리는 singleton SELECT 문으로 처리됩니다. 이 문은 쿼리와 데이터를 반환할 호스트 변수를 모두 지정합니다.  
  
-   여러 데이터 행을 반환하는 쿼리는 커서로 처리됩니다. 커서는 결과 집합 내에서 현재 행을 추적합니다. CURSOR 선언 문은 쿼리를 정의하고, OPEN 문은 쿼리 처리를 시작하고, FETCH 문은 연속적인 데이터 행을 검색하고, CLOSE 문은 쿼리 처리를 종료합니다.  
  
-   커서가 열려 있는 동안 위치 업데이트 및 위치 지정 delete 문을 사용하여 커서에서 현재 선택한 행을 업데이트하거나 삭제할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Embedded SQL 예제](../../odbc/reference/embedded-sql-example.md)  
  
-   [Embedded SQL 프로그램 컴파일](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [정적 SQL](../../odbc/reference/static-sql.md)  
  
-   [동적 SQL](../../odbc/reference/dynamic-sql.md)
