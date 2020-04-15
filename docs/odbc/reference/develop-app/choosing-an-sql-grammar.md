---
title: SQL 문법 선택 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca9911d3c88f2f540ff1332d77a2e1ebc6a4942
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299163"
---
# <a name="choosing-an-sql-grammar"></a>SQL 문법 선택
SQL 문을 생성할 때 가장 먼저 내리는 결정은 사용할 문법입니다. 오픈 그룹, ANSI 및 ISO와 같은 다양한 표준 기관에서 사용할 수 있는 문법 외에도 거의 모든 DBMS 공급업체는 표준과 약간 다른 자체 문법을 정의합니다.  
  
 [부록 C: SQL 문법은](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)모든 ODBC 드라이버가 지원해야 하는 최소 SQL 문법을 설명합니다. 이 문법은 SQL-92의 엔트리 레벨의 하위 집합입니다. 드라이버는 SQL-92에 정의된 중급, 전체 또는 FIPS 127-2 과도기 수준을 준수하도록 추가 문법을 지원할 수 있습니다. 자세한 내용은 부록 C의 [SQL 최소 문법:](../../../odbc/reference/appendixes/sql-minimum-grammar.md) SQL 문법 및 SQL-92를 참조하십시오.  
  
 부록 C는 또한 SQL-92 문법에서 다루지 않는 외부 조인과 같이 일반적으로 사용 가능한 언어 기능에 대한 표준 문법을 포함하는 *이스케이프 시퀀스를* 정의합니다. 자세한 내용은 부록 C: SQL 문법 및 [이스케이프 시퀀스의](../../../odbc/reference/develop-app/escape-sequences.md) [ODBC 이스케이프 시퀀스를](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 참조하세요.  
  
 선택한 문법은 드라이버가 문을 처리하는 방법에 영향을 줍니다. 드라이버는 SQL-92 SQL 및 ODBC 정의 이스케이프 시퀀스를 DBMS 별 SQL로 수정해야 합니다. 대부분의 SQL 문법은 하나 이상의 다양한 표준을 기반으로 하므로 대부분의 드라이버는 이 요구 사항을 충족하기 위해 거의 또는 전혀 작업을 수행하지 않습니다. ODBC에서 정의한 이스케이프 시퀀스를 검색하고 DBMS 별 문법으로 대체하는 것으로만 구성되는 경우가 많습니다. 드라이버가 인식하지 못하는 문법을 만나면 문법이 DBMS에 해당한다고 가정하고 실행을 위해 데이터 원본을 수정하지 않고 SQL 문을 전달합니다.  
  
 따라서 SQL-92 문법(및 ODBC 이스케이프 시퀀스)과 DBMS 별 문법이라는 두 가지 문법을 사용할 수 있습니다. 둘 중 SQL-92 문법만 상호 운용가능하므로 상호 운용 가능한 모든 응용 프로그램에서 는 이를 사용해야 합니다. 상호 운용할 수 없는 응용 프로그램은 SQL-92 문법 또는 DBMS 별 문법을 사용할 수 있습니다. DBMS 별 문법에는 SQL-92가 다루지 않는 모든 기능을 악용할 수 있으며 드라이버가 수정할 필요가 없기 때문에 약간 더 빠릅니다. 후자의 기능은 SQL_ATTR_NOSCAN 명령문 특성을 설정하여 부분적으로 적용할 수 있으며, 이스케이프 시퀀스를 검색하고 대체하지 못하도록 합니다.  
  
 SQL-92 문법이 사용되는 경우 응용 프로그램은 **SQLNativeSql**을 호출하여 드라이버에 의해 수정되는 방법을 발견 할 수 있습니다. 이 기능은 응용 프로그램을 디버깅할 때 유용합니다. **SQLNativeSql은** SQL 문을 수락하고 드라이버가 수정한 후 반환합니다. 이 함수는 Core 인터페이스 준수 수준에 있으므로 모든 드라이버에서 지원됩니다.
