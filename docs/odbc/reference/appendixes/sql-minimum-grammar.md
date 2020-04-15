---
title: SQL 최소 문법 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20eee34feadb8e3140f25019ec6b0d036ff02e14
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304994"
---
# <a name="sql-minimum-grammar"></a>SQL 최소 문법
이 섹션에서는 ODBC 드라이버가 지원해야 하는 최소 SQL 구문을 설명합니다. 이 섹션에서 설명하는 구문은 SQL-92의 엔트리 레벨 구문의 하위 집합입니다.  
  
 응용 프로그램은 이 섹션의 모든 구문을 사용할 수 있으며 ODBC 호환 드라이버가 해당 구문을 지원할 수 있습니다. 이 섹션에 없는 SQL-92의 추가 기능이 지원되는지 여부를 확인하려면 응용 프로그램에서 SQL_SQL_CONFORMANCE 정보 형식을 사용하여 **SQLGetInfo를** 호출해야 합니다. 드라이버가 SQL-92 준수 수준을 준수하지 않더라도 응용 프로그램은 이 섹션에 설명된 구문을 계속 사용할 수 있습니다. 반면에 드라이버가 SQL-92 수준을 준수하는 경우 해당 수준에 포함된 모든 구문을 지원합니다. 여기에 설명된 최소 문법은 가장 낮은 SQL-92 준수 수준의 순수 하위 집합이기 때문에 이 섹션의 구문이 포함됩니다. 응용 프로그램이 지원되는 SQL-92 수준을 알고 나면 해당 기능에 해당하는 개별 정보 유형으로 **SQLGetInfo를** 호출하여 상위 수준 기능이 지원되는지 여부를 확인할 수 있습니다.  
  
 읽기 전용 데이터 원본에서만 작동하는 드라이버는 변경 데이터를 다루는 이 섹션에 포함된 문법의 해당 부분을 지원하지 않을 수 있습니다. 응용 프로그램은 데이터 원본이 SQL_DATA_SOURCE_READ_ONLY 정보 형식을 사용하여 **SQLGetInfo를** 호출하여 읽기 전용인지 확인할 수 있습니다.  
  
## <a name="statement"></a>인수를 제거합니다.  
 *테이블 문 만들기* ::=  
  
 테이블 *기본 테이블 이름* 만들기  
  
 (열*식별자 데이터 유형* *[, 열 식별자 데이터*유형]...)  
  
> [!IMPORTANT]  
>  *만들기 테이블-문에서* *데이터 유형으로* 응용 프로그램은 **SQLGetTypeInfo에서**반환하는 결과 집합의 TYPE_NAME 열에서 데이터 형식을 사용해야 합니다.  
  
 *문 삭제 검색* ::=  
  
 테이블 *이름에서* 삭제 [여기서 *검색 조건]*  
  
 *드롭 테이블 문* ::=  
  
 드롭 테이블 *기본 테이블 이름*  
  
 *삽입 문* ::=  
  
 테이블 *이름에* 삽입 [(열 *식별자* [, *열 식별자]...]]*      값 *(삽입 값*[, *삽입 값]...*)  
  
 *select-statement* ::=  
  
 [모두 &#124; 별개] *선택 목록* 선택  
  
 에서 *테이블 참조 목록*  
  
 [어디 *검색 조건]*  
  
 [*주문별 절]*  
  
 *문* ::= *테이블 문 만들기*  
  
 *&#124; 삭제 문 검색*  
  
 &#124; *드롭 테이블 문*  
  
 &#124; *인서삽입문*  
  
 &#124; *선택 문*  
  
 *&#124; 업데이트 문 검색*  
  
 *업데이트 문 검색*  
  
 *테이블 이름* 업데이트  
  
 SET *열 식별자* =*{표현식* &#124; NULL }  
  
 [, *열 식별자* = {*식* &#124; NULL}]...  
  
 [어디 *검색 조건]*  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL 문에 사용되는 요소](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [데이터 형식 지원](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [매개 변수 데이터 형식](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [매개 변수 표식](../../../odbc/reference/appendixes/parameter-markers.md)
