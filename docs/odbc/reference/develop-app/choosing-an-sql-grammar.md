---
title: SQL 문법 선택 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f7bf7e77f892f10de17402b59e732523d58fbc6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036552"
---
# <a name="choosing-an-sql-grammar"></a>SQL 문법 선택
SQL 문을 구성할 때의 첫 번째 결정은 사용할 문법입니다. Open Group, ANSI 및 ISO와 같은 다양 한 표준 본문에서 사용할 수 있는 문법 외에도 거의 모든 DBMS 공급 업체는 자체 문법을 정의 하며, 각는 표준에서 약간 다릅니다.  
  
 [부록 C: Sql 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)은 모든 ODBC 드라이버에서 지원 해야 하는 최소 sql 문법을 설명 합니다. 이 문법은 SQL-92의 항목 수준 하위 집합입니다. 드라이버는 SQL-92에서 정의한 중간, 전체 또는 FIPS 127-2 전환 수준을 따르도록 추가 문법을 지원할 수 있습니다. 자세한 내용은 부록 C: SQL 문법 및 SQL-92의 [Sql 최소 문법](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 을 참조 하세요.  
  
 또한 부록 C는 외부 조인과 같이 일반적으로 사용 가능한 언어 기능에 대 한 표준 문법을 포함 하는 *이스케이프 시퀀스* 를 정의 합니다 .이는 SQL-92 문법에서 다루지 않습니다. 자세한 내용은이 섹션의 뒷부분에 나오는 부록 C: SQL 문법 및 [이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences.md)의 [ODBC 이스케이프 시퀀스](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 를 참조 하세요.  
  
 선택한 문법은 드라이버가 문을 처리 하는 방법에 영향을 줍니다. 드라이버는 SQL-92 SQL 및 ODBC 정의 이스케이프 시퀀스를 DBMS 관련 SQL로 수정 해야 합니다. 대부분의 SQL 문법이 하나 이상의 다양 한 표준을 기반으로 하기 때문에 대부분의 드라이버는이 요구 사항을 충족 하는 작업을 거의 수행 하지 않습니다. 일반적으로 ODBC에 정의 된 이스케이프 시퀀스를 검색 하 고 DBMS 관련 문법으로 대체 하는 경우에만 구성 됩니다. 드라이버가 인식 하지 못하는 문법을 발견할 경우 문법이 DBMS에 특정 한 것으로 가정 하 고 실행을 위해 데이터 소스를 수정 하지 않고 SQL 문을 전달 합니다.  
  
 따라서 사용 하는 문법에는 SQL-92 문법 (및 ODBC 이스케이프 시퀀스)과 DBMS 별 문법을 사용 하는 두 가지 선택 사항이 있습니다. 둘 중에는 SQL-92 문법을 상호 운용할 수 있으므로 모든 상호 운용 가능한 응용 프로그램에서이를 사용 해야 합니다. 상호 운용 되지 않는 응용 프로그램은 SQL-92 문법 또는 DBMS 관련 문법을 사용할 수 있습니다. DBMS 별 문법에는 두 가지 장점이 있습니다. 즉, SQL-92에 포함 되지 않은 모든 기능을 이용할 수 있으며 드라이버에서 수정할 필요가 없기 때문에 속도가 매우 빠릅니다. SQL_ATTR_NOSCAN statement 특성을 설정 하 여 두 번째 기능을 부분적으로 적용할 수 있습니다. 그러면 드라이버가 이스케이프 시퀀스를 검색 하 고 대체 하는 것을 중지 합니다.  
  
 92 문법을 사용 하는 경우 응용 프로그램은 **SQLNativeSql**를 호출 하 여 드라이버에 의해 수정 되는 방법을 검색할 수 있습니다. 이는 응용 프로그램을 디버깅할 때 유용한 경우가 많습니다. **SQLNativeSql** 는 SQL 문을 수락 하 고 드라이버에서 수정한 후 반환 합니다. 이 함수는 핵심 인터페이스 규칙 수준에 있기 때문에 모든 드라이버에서 지원 됩니다.
