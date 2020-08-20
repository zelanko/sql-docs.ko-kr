---
description: SQL 최소 문법
title: SQL 최소 문법 | Microsoft Docs
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
ms.openlocfilehash: 07adcbb100fa28a941be4fdac6efabb445ffb9ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456566"
---
# <a name="sql-minimum-grammar"></a>SQL 최소 문법
이 섹션에서는 ODBC 드라이버가 지원 해야 하는 최소 SQL 구문에 대해 설명 합니다. 이 섹션에서 설명 하는 구문은 SQL-92의 항목 수준 구문 하위 집합입니다.  
  
 응용 프로그램은이 섹션의 모든 구문을 사용할 수 있으며, 모든 ODBC 호환 드라이버에서 해당 구문을 지원 하도록 보장할 수 있습니다. 이 섹션에서 제공 하는 SQL-92의 추가 기능이 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 SQL_SQL_CONFORMANCE 된 정보 형식으로 **SQLGetInfo** 를 호출 해야 합니다. 드라이버가 92 규칙 수준을 따르지 않더라도 응용 프로그램은이 섹션에 설명 된 구문을 사용할 수 있습니다. 반면 드라이버는 SQL-92 수준을 준수 하는 경우 해당 수준에 포함 된 모든 구문을 지원 합니다. 여기에 설명 된 최소 문법이 가장 낮은 92 규칙 수준의 순수 하위 집합 이기 때문에이 섹션의 구문은 여기에 포함 됩니다. 응용 프로그램에서 지원 되는 SQL-92 수준을 알고 있으면 해당 기능에 해당 하는 개별 정보 형식으로 **SQLGetInfo** 를 호출 하 여 상위 수준 기능이 지원 되는지 여부를 확인할 수 있습니다 (있는 경우).  
  
 읽기 전용 데이터 원본 에서만 작동 하는 드라이버는 변경 데이터를 처리 하는이 섹션에 포함 된 문법의 해당 부분을 지원 하지 않을 수 있습니다. 응용 프로그램은 SQL_DATA_SOURCE_READ_ONLY 정보 형식으로 **SQLGetInfo** 를 호출 하 여 데이터 소스가 읽기 전용인 지 여부를 확인할 수 있습니다.  
  
## <a name="statement"></a>인수를 제거합니다.  
 *create-table-statement* :: =  
  
 CREATE TABLE *기본 테이블 이름*  
  
 (*열 식별자 데이터 형식* [*, 열 식별자 데이터 형식*] ...)  
  
> [!IMPORTANT]  
>  **SQLGetTypeInfo**에서 *반환 하는*결과 집합의 TYPE_NAME 열에 있는 데이터 형식을 응용 *프로그램에서 사용* 해야 합니다.  
  
 *delete-문-검색* :: =  
  
 *테이블 이름* 에서 삭제 [ *검색 조건*]  
  
 *drop table-statement* :: =  
  
 테이블 *기본 테이블 이름* 삭제  
  
 *insert 문* :: =  
  
 테이블에 삽입 *-이름* [( *열 식별자* [, *열 식별자*] ...)]      값 (값*삽입*[, *값 삽입*] ...)  
  
 *select-statement* ::=  
  
 [모두 &#124; 고유] 선택 *목록* 선택  
  
 *테이블 참조 목록* 에서  
  
 [WHERE *검색 조건*]  
  
 [*order by 절*]  
  
 *statement* :: = *create-table 문*  
  
 &#124; *delete-문-검색*  
  
 &#124; *drop table 문*  
  
 &#124; *insert 문*  
  
 &#124; *select 문*  
  
 &#124; *업데이트-문-검색*  
  
 *업데이트-문-검색*  
  
 *테이블 이름* 업데이트  
  
 *열 식별자* = {*expression* &#124; NULL} 설정  
  
 [, *열 식별자* = {*expression* &#124; NULL}] ...  
  
 [WHERE *검색 조건*]  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL 문에 사용되는 요소](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [데이터 형식 지원](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [매개 변수 데이터 형식](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [매개 변수 표식](../../../odbc/reference/appendixes/parameter-markers.md)
