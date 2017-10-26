---
title: "SQL 문법과 선택 | Microsoft Docs"
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cc1da3dfbe7f06e7d98430c5cec8fbaab3176971
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="choosing-an-sql-grammar"></a>SQL 문법과 선택
첫 번째로 결정 해야 SQL 문을 생성할 때 사용 하는 문법을입니다. Open Group, ANSI 및 ISO를 같은 다양 한 표준 기관에서 사용할 수 있는 문법 외에도 거의 모든 DBMS 공급 업체는 표준에서 조금 다름는 각각 자체 문법을 정의 합니다.  
  
 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), 모든 ODBC 드라이버를 지원 해야 하는 최소 SQL 문법을 설명 합니다. 이 문법에는 SQL 92 항목 수준의 일부입니다. 드라이버는 중간, 전체 경로 또는 sql-92 FIPS 127-2 전환 수준 정의에 맞게 추가 문법을 지원할 수 있습니다. 자세한 내용은 참조 [최소 SQL 문법을](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 부록 c: SQL 문법 및 s Q l-92에 있습니다.  
  
 부록 C도 정의 *이스케이프 시퀀스* 외부 조인과 같은 일반적으로 사용 가능한 언어 기능에 대 한 표준 문법을 포함 하는 포함 되지 않은 SQL 92 문법입니다. 자세한 내용은 참조 [ODBC 이스케이프 시퀀스](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 부록 c: SQL 문법에 및 [이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences.md)이 섹션의 뒷부분에 나오는 합니다.  
  
 선택 된 문법 드라이버 문을 처리 하는 방법에 적용 됩니다. 드라이버는 SQL 92 SQL 및 ODBC 정의 된 이스케이프 시퀀스 DBMS 전용 SQL 수정 해야 합니다. 대부분 SQL 문법의 다양 한 표준 중 하나 이상을 기반으로, 하기 때문에 대부분의 드라이버는이 요구 사항을 충족 하기 위해 거의 없거나 전혀 없이 작업을 수행 합니다. 종종 으로만 구성 정의 된 이스케이프 시퀀스에 대 한 검색으로 ODBC 및 DBMS 전용 문법으로 바꿉니다. 드라이버에서 인식할 수 없는 문법을 발견 하면 문법 DBMS 전용 이며 SQL 문 실행에 대 한 데이터 원본에는 수정 되지 않은 상태로 전달 한다고 가정 합니다.  
  
 따라서은 실제로 사용할 문법의 두 가지 선택 사항: SQL 92 문법 (및 이스케이프 시퀀스는 ODBC) 및 DBMS 전용 문법입니다. 둘 중는 SQL 92 문법 되므로 상호 운용성이 있는 모든 상호 운용 가능한 응용 프로그램에서 사용 해야 합니다. SQL 92 문법 또는 특정 DBMS 문법 상호 운용할 수 없는 응용 프로그램을 사용할 수 있습니다. 특정 DBMS 문법 두 가지 이점이 있습니다: SQL 92에서 포함 하지 않는 모든 기능을 악용할 수 있으며 미미 더 빠른 드라이버 수정할 필요가 없기 때문에 합니다. 후자의 기능 검색 및 바꾸기 이스케이프 시퀀스의 드라이버를 중지 하는 SQL_ATTR_NOSCAN 문 특성을 설정 하 여 부분적으로 적용 될 수 있습니다.  
  
 응용 프로그램 수정 된 드라이버에 의해 호출 하 여 검색할 수는 SQL 92 문법을 사용 하는 경우 **SQLNativeSql**합니다. 유용 종종 응용 프로그램을 디버그 합니다. **SQLNativeSql** SQL 문을 받아서 드라이버에이 파일을 수정한 후이 반환 합니다. 이 함수는 핵심 인터페이스 규칙 수준 이므로 모든 드라이버에서 사용할 수 있습니다.

