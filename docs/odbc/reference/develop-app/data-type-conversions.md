---
title: 데이터 유형 변환 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd888fe32692494e2b0ceadc1ed872dd96e244a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305215"
---
# <a name="data-type-conversions"></a>데이터 형식 변환
데이터는 한 응용 프로그램 변수에서 다른 응용 프로그램 변수(C에서 C로 전송되는 경우), 응용 프로그램 변수의 데이터가 문 매개 변수(C에서 SQL로 전송되는 경우), 결과 집합 열의 데이터가 응용 프로그램 변수(SQL에서 C로) 반환되는 경우, 데이터가 한 데이터 원본 열에서 다른 데이터 원본 열로 전송되는 경우(SQL에서 SQL로) 등 네 번 중 하나에서 다른 유형으로 데이터를 변환할 수 있습니다.  
  
 한 응용 프로그램 변수에서 다른 응용 프로그램 변수로 데이터를 전송할 때 발생하는 모든 변환은 이 문서의 범위를 벗어납니다.  
  
 응용 프로그램이 변수를 결과 집합 열 또는 문 매개 변수에 바인딩하는 경우 응용 프로그램은 응용 프로그램 변수의 데이터 형식 선택에서 데이터 형식 변환을 암시적으로 지정합니다. 예를 들어 열에 정수 데이터가 포함되어 있다고 가정합니다. 응용 프로그램이 열에 정수 변수를 바인딩하는 경우 변환이 수행되지 없음을 지정합니다. 응용 프로그램이 변수를 열에 바인딩하는 경우 데이터를 정수에서 문자로 변환하도록 지정합니다.  
  
 ODBC는 각 SQL 및 C 데이터 유형 간에 데이터를 변환하는 방법을 정의합니다. 기본적으로 ODBC는 문자에서 정수및 부동 정수와 같은 모든 합리적인 변환을 지원하며 현재까지 부동과 같은 잘못 정의된 변환을 지원하지 않습니다. 드라이버는 지원하는 각 SQL 데이터 유형에 대한 모든 변환을 지원해야 합니다. SQL 및 C 데이터 형식 간의 전체 변환 목록은 [SQL에서 C 데이터 유형으로 데이터를 변환하고](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 부록 D: 데이터 [형식의 C에서 SQL 데이터 유형으로 데이터를 변환하는 것을](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 참조하세요.  
  
 ODBC는 또한 한 SQL 데이터 형식에서 다른 SQL 데이터 유형으로 데이터를 변환하기 위한 스칼라 함수를 정의합니다. **CONVERT** 스칼라 함수는 드라이버에 의해 데이터 원본에서 변환을 수행하도록 정의된 기본 스칼라 함수 또는 함수에 매핑됩니다. 이 함수는 DBMS 별 함수에 매핑되므로 ODBC는 이러한 변환의 작동 방식 또는 지원해야 하는 변환을 정의하지 않습니다. 응용 프로그램은 **SQLGetInfo의**SQL_CONVERT 옵션을 통해 특정 드라이버 및 데이터 원본에서 지원하는 변환을 검색합니다. **CONVERT** 스칼라 함수에 대한 자세한 내용은 ODBC 및 [명시적 데이터 유형 변환 함수의](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md) [이스케이프 시퀀스를](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 참조하십시오.
