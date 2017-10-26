---
title: "데이터 버퍼 유형 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c2ed3fb1d6a68737a894663e1b5c841d6cb1041
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="data-buffer-type"></a>데이터 버퍼 종류
버퍼의 C 데이터 형식은 응용 프로그램에 의해 지정 됩니다. 을 단일 변수로 경우가이 응용 프로그램 변수를 할당 합니다. 일반적인 메모리 사용-메모리 즉, void 형식의 포인터에서 가리키는-이 응용 프로그램 메모리를 특정 형식으로 캐스팅 때 발생 합니다. 드라이버는이 이와 같은 두 가지 방법으로 검색 됩니다.  
  
-   **데이터 버퍼 형식 인수입니다.** 연결 된 버퍼와 같은 매개 변수 값 및 결과 집합 데이터를 전송 하는 데 사용 하는 버퍼 *TargetValuePtr* 에 **SQLBindCol**, 일반적으로 등 연결 된 형식 인수에 포함 되어는 * TargetType* 인수 **SQLBindCol**합니다. 이 인수를 응용 프로그램 버퍼 형식에 해당 하는 C 형식 식별자를 전달 합니다. 예를 들어, 다음에 호출에서 **SQLBindCol**, SQL_C_TYPE_DATE 값 지시 드라이버 하는 *날짜* 버퍼가 SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     형식 식별자에 대 한 자세한 내용은 참조는 [ODBC의 데이터 형식](../../../odbc/reference/develop-app/data-types-in-odbc.md) 이 섹션의 뒷부분에 나오는 섹션.  
  
-   **미리 정의 된 형식입니다.** 가리키는 보내고 옵션 또는 버퍼와 같은 특성을 검색 하는 데 사용 되는 버퍼는 *InfoValuePtr* 인수에 **SQLGetInfo**, 지정 된 옵션에 따라 달라 지는 고정 형식이 있습니다. 드라이버는이 형식의 데이터 버퍼 인지 가정 응용 프로그램의 이러한 종류의 버퍼를 할당 합니다. 예를 들어, 다음에 호출에서 **SQLGetInfo**, 드라이버 SQL_STRING_FUNCTIONS 옵션을 사용 하려면 어떤 이므로 버퍼는 32 비트 정수를 가정 합니다.  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 버퍼의 데이터를 해석 하는 C 데이터 형식을 사용 하는 드라이버.

