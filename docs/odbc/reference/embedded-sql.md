---
title: Embedded SQL | Microsoft Docs
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
ms.openlocfilehash: 6a7fa2b3105aedee6cb054c5d5dfa76f3c430f35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915421"
---
# <a name="embedded-sql"></a>Embedded SQL
SQL 문을 DBMS에 보내는 첫 번째 방법은 포함 된 SQL입니다. SQL은 변수 및 흐름 제어 문을 사용 하지 않으므로 C 또는 COBOL과 같은 기존 프로그래밍 언어로 작성 된 프로그램에 추가할 수 있는 데이터베이스 하위 언어로 사용 되는 경우가 많습니다. 이는 포함 된 SQL의 핵심 개념입니다. 호스트 프로그래밍 언어로 작성 된 프로그램에 SQL 문을 배치 하는 것입니다. 간단히 말해서, 다음 기술은 호스트 언어로 SQL 문을 포함 하는 데 사용 됩니다.  
  
-   포함 된 SQL 문은 특수 SQL 미리 컴파일된에서 처리 됩니다. 모든 SQL 문은 lambda-introducer로 시작 하 고 종결자를 사용 하 여 종료 됩니다. 둘 다 미리 컴파일된에 대 한 SQL 문의 플래그를 지정 합니다. Lambda-introducer 및 종결자는 호스트 언어에 따라 달라 집니다. 예를 들어 lambda-introducer는 C의 "EXEC SQL"이 고, MUMPS에서는 "&SQL (" 이며, 종결자는 세미콜론 (;) C에서 MUMPS의 오른쪽 괄호  
  
-   호스트 변수 라고 하는 응용 프로그램 프로그램의 변수는 상수가 허용 될 때마다 포함 된 SQL 문에서 사용할 수 있습니다. 이러한 쿼리는 입력에 사용 하 여 SQL 문을 특정 상황에 맞게 조정 하 고 출력을 사용 하 여 쿼리 결과를 받을 수 있습니다.  
  
-   단일 데이터 행을 반환 하는 쿼리는 단일 SELECT 문을 사용 하 여 처리 됩니다. 이 문은 데이터를 반환할 쿼리와 호스트 변수를 모두 지정 합니다.  
  
-   데이터의 여러 행을 반환 하는 쿼리는 커서를 사용 하 여 처리 됩니다. 커서는 결과 집합 내의 현재 행을 추적 합니다. DECLARE CURSOR 문은 쿼리를 정의 하 고, OPEN 문이 쿼리 처리를 시작 하 고, FETCH 문이 연속 된 데이터 행을 검색 하 고, CLOSE 문은 쿼리 처리를 종료 합니다.  
  
-   커서가 열려 있는 동안 커서에 의해 현재 선택 된 행을 업데이트 하거나 삭제 하는 데 위치 지정 업데이트 및 위치 delete 문을 사용할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Embedded SQL 예제](../../odbc/reference/embedded-sql-example.md)  
  
-   [Embedded SQL 프로그램 컴파일](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [정적 SQL](../../odbc/reference/static-sql.md)  
  
-   [동적 SQL](../../odbc/reference/dynamic-sql.md)
