---
title: 데이터 형식 변환 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84710ffd69ea377c979adf94af1394d8436ef10b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786341"
---
# <a name="data-type-conversions"></a>데이터 형식 변환
데이터가 변환 될 수 형식에서 다른 네 번 중 하나: 데이터는 전송할 때 하나의 응용 프로그램 변수에서 다른 (C에 C,) (C)에서 SQL로 문 매개 변수에 응용 프로그램 변수에서 데이터를 보낼 때 결과 집합 열의 데이터에서 반환 될 때 응용 프로그램 변수 (SQL에서 C로) 및 데이터 원본 열에서 다른 SQL (to SQL)에서 데이터를 전송 하는 경우.  
  
 변환에서 다른 응용 프로그램 변수에서 데이터를 전송 하는 경우 발생 하는이 문서의 범위를 벗어납니다.  
  
 응용 프로그램 변수로 결과 집합 열 또는 문 매개 변수를 바인딩할 때 응용 프로그램 데이터 형식 변환의 다양 한 응용 프로그램 변수의 데이터 형식에서에서 암시적으로 지정 합니다. 예를 들어, 열을 정수 데이터를 포함 합니다. 응용 프로그램 열에 정수 변수를 바인딩할 경우 변환이 수행 함을; 지정 문자 변수 열에 바인딩하면 하는 응용 프로그램, 데이터 문자 정수에서 변환 되어야 함을 지정 합니다.  
  
 ODBC는 각 SQL 및 C 데이터 형식 간에 데이터를 변환 하는 방법을 정의 합니다. 기본적으로 ODBC 문자를 정수 및 부동 소수점, 정수 등의 모든 적절 한 변환을 지원 하 고 누계 float와 같은 잘못 정의 변환을 지원 하지 않습니다. 드라이버가 지 원하는 각 SQL 데이터 형식에 대 한 모든 변환을 지원 해야 합니다. SQL 및 C 데이터 형식 간의 변환의 전체 목록은 참조 하세요. [SQL에서 C 데이터 형식 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 하 고 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 부록 d: 데이터 형식에서입니다.  
  
 또한 ODBC SQL 데이터 형식에서 다른 데이터를 변환 하는 것에 대 한 스칼라 함수를 정의 합니다. 합니다 **변환** 스칼라 함수는 드라이버 기본 스칼라 함수 또는 데이터 원본에서 변환을 수행 하기 위해 정의 된 함수에 의해 매핑됩니다. 이 함수는 DBMS 특정 함수에 매핑되므로 ODBC 지원 해야 하는 어떤 변환 또는 이러한 변환이 작동 하는 방법을 정의 하지 않습니다. 응용 프로그램 검색의 SQL_CONVERT 옵션을 통해 특정 드라이버 및 데이터 원본에 의해 어떤 변환이 지원 됩니다 **SQLGetInfo**합니다. 에 대 한 자세한 내용은 합니다 **변환** 스칼라 함수를 참조 하세요 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 및 [명시적 데이터 형식 변환 함수](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
