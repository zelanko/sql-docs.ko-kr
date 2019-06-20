---
title: '부록 D: 데이터 형식 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75ff7e83aa87bca9f33a3a8f44447af2eb60c581
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026765"
---
# <a name="appendix-d-data-types"></a>부록 D: 데이터 형식
ODBC에는 두 가지 데이터 형식 정의합니다. SQL 데이터 형식 및 C 데이터 형식입니다. SQL 데이터 형식에는 데이터 원본에 저장 된 데이터의 데이터 형식을 나타냅니다. C 데이터 형식에는 응용 프로그램 버퍼에 저장 된 데이터의 데이터 형식을 나타냅니다.  
  
 SQL 데이터 형식은 SQL-92 표준에 따라 각 DBMS에 의해 정의 됩니다. SQL-92 표준에 지정 된 각 SQL 데이터 형식에 대 한 ODBC 정의 되는 형식 식별자를 **#define** ODBC 함수에 인수로 전달 되거나 결과 집합의 메타 데이터에서 반환 되는 값입니다. 전용 SQL-92 데이터 형식이 ODBC에서 지원 되지 않습니다 되며 비트 (ODBC SQL_BIT 형식이 서로 다른 특성), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE, NATIONAL_CHARACTER 합니다. 드라이버는 ODBC SQL 데이터 형식 식별자 및 드라이버별 SQL 데이터 형식 식별자를 데이터 소스 관련 SQL 데이터 형식을 매핑하는 일을 담당 합니다. SQL 데이터 형식 구현 설명자의 SQL_DESC_CONCISE_TYPE 필드에 지정 됩니다.  
  
 ODBC C 데이터 형식 및 해당 ODBC 형식 식별자를 정의합니다. 응용 프로그램에서 적절 한 C 형식 식별자를 전달 하 여 결과 집합 데이터를 받을 버퍼의 C 데이터 형식을 지정 합니다 *TargetType* 호출에서 인수 **SQLBindCol** 또는  **SQLGetData**합니다. 적절 한 C 형식 식별자를 전달 하 여 문 매개 변수를 포함 하는 버퍼의 C 형식을 지정 합니다 *ValueType* 호출에서 인수 **SQLBindParameter**합니다. 응용 프로그램 설명자를 SQL_DESC_CONCISE_TYPE 분야에서 C 데이터 형식 지정 됩니다.  
  
> [!NOTE]  
>  드라이버 관련 C 데이터 형식은 없습니다.  
  
 각 SQL 데이터 형식은 ODBC C 데이터 형식에 해당 합니다. 데이터 원본에서 데이터를 반환 하기 전에 드라이버 지정된 된 C 데이터 형식으로 변환 합니다. 데이터 원본에 데이터를 보내기 전에 드라이버 지정된 된 C 데이터 형식에서 변환 합니다.  
  
 이 부록에는 다음 항목에 있습니다.  
  
-   [데이터 형식 식별자 사용](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [의사(pseudo) 형식 식별자](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [이진 형식으로 데이터 전송](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [간격 및 숫자 데이터 형식에 대한 지침](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [일반 달력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [열 크기, 십진수, 8진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [데이터를 SQL에서 C 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [데이터를 C에서 SQL 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 에 대 한 설명은 ODBC 데이터 형식 참조 [ODBC의 데이터 형식](../../../odbc/reference/develop-app/data-types-in-odbc.md)합니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.
