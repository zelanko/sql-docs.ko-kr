---
title: '부록 d: 데이터 형식 | Microsoft Docs'
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
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bea62ceaba74b56087ecbb8fa28c8a0108426380
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="appendix-d-data-types"></a>부록 d: 데이터 형식
ODBC에는 두 가지 데이터 형식 정의: SQL 데이터 형식 및 C 데이터 형식입니다. SQL 데이터 형식에는 데이터 원본에 저장 된 데이터의 데이터 형식을 나타냅니다. C 데이터 형식에는 응용 프로그램 버퍼에 저장 된 데이터의 데이터 형식을 나타냅니다.  
  
 SQL 데이터 형식은 sql-92 표준에 따라 각 DBMS에 의해 정의 됩니다. Sql-92 표준에 지정 된 각 SQL 데이터 형식에 대 한 ODBC 형식 식별자가 이미 정의 되어는 **#define** ODBC 함수에 인수로 전달 하거나 결과 집합의 메타 데이터의 반환 값을 합니다. 유일한 SQL 92 ODBC에서 지원 되지 않는 데이터 형식 (ODBC SQL_BIT 형식이 각기 다른 특징이) 비트, BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE, 및 NATIONAL_CHARACTER는 합니다. 드라이버는 ODBC SQL 데이터 형식 식별자 및 드라이버별 SQL 데이터 형식 식별자에 데이터 원본에 따른 특정 SQL 데이터 형식에 매핑합니다. SQL 데이터 형식은 구현 설명자의 SQL_DESC_CONCISE_TYPE 필드에 지정 됩니다.  
  
 ODBC C 데이터 형식 및 해당 ODBC 형식 식별자가 정의합니다. 응용 프로그램에 적절 한 C 유형 식별자를 전달 하 여 결과 집합 데이터를 수신할 버퍼의 C 데이터 형식을 지정 된 *TargetType* 인수에 대 한 호출에 **SQLBindCol** 또는  **SQLGetData**합니다. 적절 한 C 형식 식별자를 전달 하 여 문 매개 변수를 포함 하는 버퍼의 C 형식을 지정 된 *ValueType* 인수에 대 한 호출에 **SQLBindParameter**합니다. C 데이터 형식은 응용 프로그램 설명자의 SQL_DESC_CONCISE_TYPE 필드에 지정 됩니다.  
  
> [!NOTE]  
>  드라이버 관련 C 데이터 형식은 없습니다.  
  
 각 SQL 데이터 형식을 ODBC C 데이터 형식에 해당합니다. 데이터 원본에서 데이터를 반환 하기 전에 드라이버 지정된 된 C 데이터 형식으로 변환 합니다. 데이터 원본에 데이터를 보내기 전에 드라이버 지정된 된 C 데이터 형식에서 변환 합니다.  
  
 이 부록의 내용에는 다음 항목이 포함 되어 있습니다.  
  
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
