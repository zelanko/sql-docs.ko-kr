---
title: '부록 D: 데이터 유형 | 마이크로 소프트 문서'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c1abadb962e3a1ee9327bbb8d84e52d180b4a7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292463"
---
# <a name="appendix-d-data-types"></a>부록 D: 데이터 형식
ODBC는 SQL 데이터 형식과 C 데이터 형식이라는 두 가지 데이터 형식 집합을 정의합니다. SQL 데이터 형식은 데이터 원본에 저장된 데이터의 데이터 형식을 나타냅니다. C 데이터 형식은 응용 프로그램 버퍼에 저장된 데이터의 데이터 형식을 나타냅니다.  
  
 SQL 데이터 형식은 SQL-92 표준에 따라 각 DBMS에 의해 정의됩니다. SQL-92 표준에 지정된 각 SQL 데이터 형식에 대해 ODBC 함수에서 인수로 전달되거나 결과 집합의 메타데이터에 반환되는 **#define** 값인 형식 식별자를 정의합니다. ODBC에서 지원되지 않는 유일한 SQL-92 데이터 유형은 BIT(ODBC SQL_BIT 형식은 서로 다른 특성), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE 및 NATIONAL_CHARACTER. 드라이버는 데이터 원본별 SQL 데이터 형식을 ODBC SQL 데이터 형식 식별자 및 드라이버 별 SQL 데이터 형식 식별자에 매핑하는 것을 담당합니다. SQL 데이터 형식은 구현 설명자의 SQL_DESC_CONCISE_TYPE 필드에 지정됩니다.  
  
 ODBC는 C 데이터 형식과 해당 ODBC 형식 식별자를 정의합니다. 응용 프로그램은 **SQLBindCol** 또는 **SQLGetData에**대한 호출에서 *TargetType* 인수에서 적절한 C 형식 식별자를 전달하여 결과 집합 데이터를 수신하는 버퍼의 C 데이터 형식을 지정합니다. **SQLBindParameter**에 대한 호출에서 *ValueType* 인수에서 적절한 C 형식 식별자를 전달하여 문 매개 변수를 포함하는 버퍼의 C 형식을 지정합니다. C 데이터 형식은 응용 프로그램 설명자의 SQL_DESC_CONCISE_TYPE 필드에 지정됩니다.  
  
> [!NOTE]  
>  드라이버 관련 C 데이터 형식이 없습니다.  
  
 각 SQL 데이터 형식은 ODBC C 데이터 형식에 해당합니다. 데이터 원본에서 데이터를 반환하기 전에 드라이버는 데이터를 지정된 C 데이터 유형으로 변환합니다. 데이터 원본으로 데이터를 보내기 전에 드라이버는 지정된 C 데이터 형식에서 데이터를 변환합니다.  
  
 이 부록에는 다음 항목이 포함되어 있습니다.  
  
-   [데이터 형식 식별자 사용](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [SQL 데이터 유형](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [의사(pseudo) 형식 식별자](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [이진 형식으로 데이터 전송](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [간격 및 숫자 데이터 형식에 대한 지침](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [일반 달력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [열 크기, 십진수, 8진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [데이터를 SQL에서 C 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [데이터를 C에서 SQL 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 ODBC 데이터 형식에 대한 설명은 [ODBC의 데이터 형식을](../../../odbc/reference/develop-app/data-types-in-odbc.md)참조하십시오. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오.
