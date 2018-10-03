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
manager: craigg
ms.openlocfilehash: 670ed0adbbd5ad993af0942d492ee19f75fa9628
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848031"
---
# <a name="choosing-an-sql-grammar"></a>SQL 문법 선택
SQL 문 생성 하는 경우 첫 번째 결정은 사용 하는 문법입니다. 문법, Open Group, ANSI 및 ISO와 같은 다양 한 표준 기관에서 제공 하는 것 외에도 거의 모든 DBMS 공급 업체는 표준에서 약간씩 다릅니다 각각 자체 문법을 정의 합니다.  
  
 [부록 c: SQL 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), 모든 ODBC 드라이버를 지원 해야 하는 최소 SQL 문법을 설명 합니다. 이 문법에는 SQL-92 항목 수준의 일부입니다. 드라이버는 중간, 전체 경로 또는 FIPS 127-2 전환 수준이 정의에서 SQL-92에 맞게 추가 문법을 지원할 수 있습니다. 자세한 내용은 [SQL 최소 문법](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 부록 c: SQL 문법 및 SQL-92에 있습니다.  
  
 부록 C 정의 *이스케이프 시퀀스* 외부 조인과 같은 일반적으로 사용 가능한 언어 기능에 대 한 표준 문법을 포함 하는 포함 되지 않는 SQL-92 문법입니다. 자세한 내용은 [ODBC 이스케이프 시퀀스](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 부록 c: SQL 문법에서 및 [이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences.md)이 섹션의 뒷부분에 나오는.  
  
 선택 된 문법 드라이버 문을 처리 하는 방법에 적용 됩니다. 드라이버는 SQL-92 SQL 및 DBMS 전용 sql ODBC 정의 된 이스케이프 시퀀스를 수정 해야 합니다. 대부분의 SQL 문법을를 기반으로 하므로 다양 한 표준 중 하나 이상을 대부분의 드라이버는이 요구 사항을 충족 하도록 적거나 없는 작업을 수행 합니다. 종종 만으로 구성 되며 정의 된 이스케이프 시퀀스에 대 한 검색 ODBC 및 DBMS 전용 문법으로 바꿔 여 합니다. 드라이버에서 인식할 수 없는 문법을 발견 문법 DBMS 전용 이며 실행에 대 한 데이터 소스를 수정 하지 않고 SQL 문이 전달 한다고 가정 합니다.  
  
 따라서 실제로 두 가지 방법이 있습니다 문법의 데: SQL-92 문법 (및 이스케이프 시퀀스는 ODBC) 및 DBMS 전용 문법입니다. 둘 중에서 SQL-92 문법만 이므로, 상호 운용 가능한 모든 상호 운용 가능한 응용 프로그램에서 사용 해야 합니다. 상호 운용 되지 않는 응용 프로그램의 SQL-92 문법은 특정 DBMS 문법에 대해서 사용할 수 있습니다. DBMS 관련 문법 두 가지 이점이 있습니다: SQL-92에에서 포함 하지 않는 모든 기능을 이용 하는 것 이며 이다 빠르게 드라이버 수정할 수 없기 때문입니다. 두 번째 기능 검색 및 바꾸기 이스케이프 시퀀스에서 드라이버를 중지 하는 SQL_ATTR_NOSCAN 문 특성을 설정 하 여 부분적으로 적용할 수 있습니다.  
  
 SQL-92 문법을 사용 하는 경우 응용 프로그램 수정 되는 드라이버에서 호출 하 여 검색할 수 있습니다 **SQLNativeSql**합니다. 이 응용 프로그램을 디버깅 하는 경우에 주로 유용 합니다. **SQLNativeSql** SQL 문을 받아서 드라이버에이 파일을 수정한 후 반환 합니다. 이 함수는 핵심 인터페이스 적합성 수준 이므로 모든 드라이버에서 지원 됩니다.
