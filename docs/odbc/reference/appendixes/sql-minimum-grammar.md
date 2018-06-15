---
title: 최소 SQL 문법을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3e31f53abf8d8788f719adc9e00e180ca7aa96f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909968"
---
# <a name="sql-minimum-grammar"></a>최소 SQL 문법
이 섹션에서는 ODBC 드라이버가 지원 해야 하는 최소 SQL 구문을 설명 합니다. 이 섹션에 설명 된 구문은 SQL 92의 항목 수준 구문의 하위 집합입니다.  
  
 응용 프로그램이 섹션의 구문 중 하나를 사용할 수 있으며 모든 ODBC 규격 드라이버에서 해당 구문의 지원 하는지 보장할 수 있습니다. 이 섹션에는 SQL 92의 추가 기능을 지원 여부를 확인 하려면 응용 프로그램 호출 해야 **SQLGetInfo** SQL_SQL_CONFORMANCE 정보 유형을 사용 합니다. 드라이버는 SQL 92 규칙 수준에 맞지 않는, 경우에 응용 프로그램이 섹션에 설명 된 구문을 사용할 수 있습니다. 드라이버는 SQL 92 수준을 따르는 경우 해당 수준에 포함 된 모든 구문을 지원 반면에 합니다. 이 여기에 설명 된 최소 문법의 하위 집합인 순수 가장 낮은 sql-92 규칙 수준 때문에이 섹션에서는 구문을 포함 합니다. 응용 프로그램에 지원 되는 SQL 92 수준 알고 있듯이 되 면 더 높은 수준의 기능 (있는 경우)를 호출 하 여 지원 되는지 확인 수 것 **SQLGetInfo** 기능에 해당 하는 개별 정보 형식을 사용 합니다.  
  
 읽기 전용 데이터 원본을 사용 하는 드라이버에서 변경 되는 데이터를 처리 하는이 섹션에 포함 된 문법의 부분을 지원 하지 않습니다. 응용 프로그램에서 호출 하 여 데이터 소스는 읽기 전용 경우를 확인할 수 **SQLGetInfo** SQL_DATA_SOURCE_READ_ONLY 정보 유형을 사용 합니다.  
  
## <a name="statement"></a>문  
 *테이블 생성-문* :: =  
  
 CREATE TABLE *기본 테이블 이름*  
  
 (*데이터 형식 열 식별자* [*, 데이터 형식 열 식별자*]...)  
  
> [!IMPORTANT]  
>  로 *데이터 형식* 에 *테이블 생성-문*, 응용 프로그램에서 반환 된 결과 집합의 TYPE_NAME 열에서 데이터 형식을 사용 해야 **SQLGetTypeInfo**합니다.  
  
 *delete 문은 검색* :: =  
  
 DELETE FROM *테이블 이름* [여기서 *검색 조건*]  
  
 *drop-테이블-문을* :: =  
  
 DROP TABLE *기본 테이블 이름*  
  
 *insert 문의* :: =  
  
 INSERT INTO *테이블 이름* [( *열 식별자* [, *열 식별자*]...)]      값 (*삽입 값*[, *삽입 값*]...)  
  
 *선택 문* :: =  
  
 선택 [모든 &#124; DISTINCT] *선택 목록*  
  
 *테이블 참조 목록*  
  
 [여기서 *검색 조건*]  
  
 [*order by 절*]  
  
 *문* :: = *테이블 생성-문*  
  
 &#124;*delete 문은 검색*  
  
 &#124;*놓기 테이블 문*  
  
 &#124;*insert 문*  
  
 &#124;*select 문*  
  
 &#124;*업데이트 문을 검색*  
  
 *update 문을 검색*  
  
 업데이트 *테이블 이름*  
  
 설정 *열 식별자* = {*식* &#124; NULL}  
  
 [, *열 식별자* = {*식* &#124; NULL}]...  
  
 [여기서 *검색 조건*]  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL 문에 사용되는 요소](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [데이터 형식 지원](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [매개 변수 데이터 형식](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [매개 변수 표식](../../../odbc/reference/appendixes/parameter-markers.md)
