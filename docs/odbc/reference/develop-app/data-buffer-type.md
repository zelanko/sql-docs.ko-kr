---
title: 데이터 버퍼 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b98ed2ab0865b98884f6dfa1ff20142540ff314
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305249"
---
# <a name="data-buffer-type"></a>데이터 버퍼 형식
버퍼의 C 데이터 형식은 응용 프로그램에서 지정합니다. 단일 변수를 사용하면 응용 프로그램이 변수를 할당할 때 발생합니다. 일반 메모리( 즉, 형식 void포인터가 가리키는 메모리)를 사용하면 응용 프로그램이 특정 형식에 메모리를 캐스팅할 때 발생합니다. 드라이버는 다음 두 가지 방법으로 이 유형을 검색합니다.  
  
-   **데이터 버퍼 형식 인수입니다.** 매개 변수 값 및 결과 집합 데이터를 전송 하는 데 사용 되는 버퍼(예: **SQLBindCol에서** *TargetValuePtr로* 바인딩된 버퍼) 일반적으로 **SQLBindCol에서** *TargetType* 인수와 같은 관련 형식 인수가 있습니다. 이 인수에서 응용 프로그램은 버퍼의 형식에 해당하는 C 형식 식별자를 전달합니다. 예를 들어 **SQLBindCol에**대한 다음 호출에서 SQL_C_TYPE_DATE 값은 *드라이버에게 날짜* 버퍼가 SQL_DATE_STRUCT 알려줍니다.  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     형식 식별자에 대한 자세한 내용은 [ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) 섹션의 데이터 형식 섹션의 다음 섹션의 다음 을 참조하십시오.  
  
-   **미리 정의된 형식입니다.** **SQLGetInfo에서** *InfoValuePtr* 인수에 의해 가리키는 버퍼와 같은 옵션 또는 특성을 보내고 검색하는 데 사용되는 버퍼에는 지정된 옵션에 따라 달라지는 고정 형식이 있습니다. 드라이버는 데이터 버퍼가 이 형식이라고 가정합니다. 이 형식의 버퍼를 할당하는 것은 응용 프로그램의 책임입니다. 예를 들어 **SQLGetInfo에**대한 다음 호출에서 드라이버는 SQL_STRING_FUNCTIONS 옵션에 필요한 것이기 때문에 버퍼가 32비트 정수라고 가정합니다.  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 드라이버는 C 데이터 형식을 사용하여 버퍼의 데이터를 해석합니다.
