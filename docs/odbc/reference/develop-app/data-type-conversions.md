---
title: "데이터 형식 변환 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2369b39ff415a5387205ce62811594fe08a9f324
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-conversions"></a>데이터 형식 변환
데이터가 변환 될 수 한 형식에서 다른 4 배 중 하나에서: 전송 될 때 데이터는 하나의 응용 프로그램 변수에서 (C에 C)를 다른 응용 프로그램 변수에서 데이터를 문 매개 변수 (C)에서 SQL로 보낼 때 결과 집합 열에는 데이터에 반환 될 때 응용 프로그램 변수 (SQL에서 C로) 및 때 데이터가 전송 되는지 하나의 데이터 원본 열에서 다른 SQL (to SQL)입니다.  
  
 다른 응용 프로그램 변수에서 데이터를 전송할 때 발생 하는 변환이 문서의 범위를 벗어납니다.  
  
 응용 프로그램 변수를 결과 집합 열 또는 문 매개 변수를 바인딩할 때 응용 프로그램의 응용 프로그램 변수의 데이터 형식 선택에 데이터 형식 변환이 암시적으로 지정 합니다. 예를 들어 정수 데이터를 포함 하는 열입니다. 응용 프로그램 열에는 정수 변수를 바인딩할 경우 변환 작업 없이; 수행 함을 지정합니다 응용 프로그램 열에 문자 변수를 바인딩할 경우 데이터 문자 정수에서 변환 되어야 함을 지정 합니다.  
  
 ODBC는 각 SQL 및 C 데이터 형식 간에 데이터를 변환 하는 방법을 정의 합니다. 기본적으로, ODBC는 문자를 정수 및 부동 소수점, 정수 등의 모든 적절 한 변환을 지원 하 고 누계 float 같은 기본 변환을 지원 하지 않습니다. 드라이버가 지 원하는 각 SQL 데이터 형식에 대 한 모든 변환을 지 원하는 데 필요 합니다. SQL 및 C 데이터 형식 간의 변환에 대 한 전체 목록은 참조 하십시오. [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 및 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 부록 d: 데이터 형식에서입니다.  
  
 또한 ODBC SQL 데이터 형식에서 데이터 변환에 대 한 스칼라 함수를 정의 합니다. **변환** 스칼라 함수는 드라이버 기본 스칼라 함수 또는 변환을 수행 하기 위해 데이터 원본에 정의 된 함수에 의해 매핑됩니다. 이 함수는 DBMS 관련 함수에 매핑되므로 ODBC 어떤 변환이 지원 되어야 합니다 또는 이러한 변환이 작동 하는 방법을 정의 하지 않습니다. 응용 프로그램은 어떤 변환이 SQL_CONVERT 옵션을 통해 특정 드라이버 및 데이터 원본에 의해 지원 됩니다 검색 **SQLGetInfo**합니다. 에 대 한 자세한 내용은 **변환** 스칼라 함수 참조 [odbc에서 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 및 [명시적 데이터 형식 변환 함수](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)합니다.

