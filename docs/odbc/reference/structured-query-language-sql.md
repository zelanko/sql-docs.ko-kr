---
title: 구조화 된 쿼리 언어 (SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c669b4424271fc1a3c91dea37159474fb52b97cd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293393"
---
# <a name="structured-query-language-sql"></a>SQL(구조적 쿼리 언어)(Structured Query Language)
일반적인 DBMS를 사용하면 조직적이고 효율적인 방식으로 데이터를 저장, 액세스 및 수정할 수 있습니다. 원래 DBMS 사용자는 프로그래머였습니다. 저장된 데이터에 액세스하려면 COBOL과 같은 프로그래밍 언어로 프로그램을 작성해야 했습니다. 이러한 프로그램은 종종 비기술적 사용자에게 친숙한 인터페이스를 제시하기 위해 작성되었지만, 데이터 자체에 액세스하려면 지식이 풍부한 프로그래머의 서비스가 필요했습니다. 데이터에 대한 캐주얼 액세스는 실용적이지 않았습니다.  
  
 사용자는이 상황에 완전히 만족하지 않았습니다. 데이터에 액세스할 수 있지만 DBMS 프로그래머가 특수 소프트웨어를 작성하도록 설득해야 하는 경우가 많습니다. 예를 들어 영업 부서에서 각 영업 사원의 이전 달 총 매출을 보고 회사의 각 영업 사원의 서비스 기간에 따라 이 정보의 순위를 매기려면 두 가지 선택 사항이 있습니다. 많은 경우에, 이것은 가치보다 더 많은 작업이었고, 항상 일회성 또는 임시 문의를위한 비싼 솔루션이었습니다. 점점 더 많은 사용자가 쉽게 액세스하기를 원함에 따라 이 문제는 점점 더 커졌습니다.  
  
 사용자가 임시로 데이터에 액세스할 수 있도록 허용하려면 요청을 표현할 수 있는 언어를 제공해야 했습니다. 데이터베이스에 대한 단일 요청은 쿼리로 정의됩니다. 이러한 언어를 쿼리 언어라고 합니다. 많은 쿼리 언어는 이러한 목적을 위해 개발되었지만, 이들 중 하나가 가장 인기가되었다: 구조화 쿼리 언어, 1970 년대에 IBM에서 발명. 그것은 더 일반적으로 약어, SQL로 알려져 있으며, "ess-cue-ell"과 "속편"으로 발음된다. SQL은 1986년에 ANSI 표준이 되었고 1987년에는 ISO 표준이 되었습니다. 오늘날 많은 데이터베이스 관리 시스템에서 사용됩니다.  
  
 SQL은 사용자의 임시 요구를 해결했지만 컴퓨터 프로그램의 데이터 액세스 필요성은 사라지지 않았습니다. 실제로 대부분의 데이터베이스 액세스는 정기적인 보고서 및 통계 분석, 주문 입력에 사용되는 데이터 입력 프로그램, 계정을 조정하고 작업 주문을 생성하는 데 사용되는 것과 같은 데이터 조작 프로그램의 형태로 여전히 프로그래밍 방식이었습니다.  
  
 또한 이러한 프로그램은 다음 세 가지 기술 중 하나를 사용하여 SQL을 사용합니다.  
  
-   SQL 문이 C 또는 COBOL과 같은 호스트 언어에 포함되는 **임베디드 SQL입니다.**  
  
-   **SQL 문이**DBMS에서 컴파일되고 호스트 언어에서 호출되는 SQL 모듈입니다.  
  
-   SQL 문을 DBMS에 전달하고 DBMS에서 결과를 검색하기 위해 호출되는 함수로 구성된 **호출 수준 인터페이스**또는 CLI입니다.  
  
> [!NOTE]  
>  동일한 용어인 API(응용 프로그램 프로그래밍 인터페이스 대신 호출 수준 인터페이스)라는 용어가 사용되는 것은 역사적인 사고입니다. 데이터베이스 세계에서 API는 SQL 자체를 설명하는 데 사용됩니다: SQL은 DBMS의 API입니다.  
  
 대부분의 주요 DBMS는 독점 CLI를 지원하지만 이러한 선택 중 임베디드 SQL이 가장 일반적으로 사용됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL 문 처리](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [Embedded SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 모듈](../../odbc/reference/sql-modules.md)  
  
-   [호출 수준 인터페이스](../../odbc/reference/call-level-interfaces.md)
