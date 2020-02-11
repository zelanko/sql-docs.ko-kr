---
title: 데이터 버퍼 유형 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 615625ca396e5f2ae094962457cc9e746730ddcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067409"
---
# <a name="data-buffer-type"></a>데이터 버퍼 형식
버퍼의 C 데이터 형식은 응용 프로그램에 의해 지정 됩니다. 단일 변수를 사용 하는 경우이는 응용 프로그램에서 변수를 할당할 때 발생 합니다. 일반 메모리, 즉 void 형식의 포인터가 가리키는 메모리-이는 응용 프로그램이 메모리를 특정 형식으로 캐스팅할 때 발생 합니다. 드라이버는 다음과 같은 두 가지 방법으로이 유형을 검색 합니다.  
  
-   **데이터 버퍼 형식 인수입니다.** **SQLBindCol**의 *Targetvalueptr* 에 바인딩된 버퍼와 같은 매개 변수 값 및 결과 집합 데이터를 전송 하는 데 사용 되는 버퍼에는 일반적으로 **SQLBindCol**의 *TargetType* 인수와 같이 연결 된 형식 인수가 있습니다. 이 인수에서 응용 프로그램은 버퍼의 형식에 해당 하는 C 형식 식별자를 전달 합니다. 예를 들어 **SQLBindCol**에 대 한 다음 호출에서 값 SQL_C_TYPE_DATE은 *날짜* 버퍼가 SQL_DATE_STRUCT 임을 드라이버에 알립니다.  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     형식 식별자에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 [ODBC의 데이터 형식](../../../odbc/reference/develop-app/data-types-in-odbc.md) 섹션을 참조 하십시오.  
  
-   **미리 정의 된 형식입니다.** **SQLGetInfo**의 *Infovalueptr* 인수에서 가리키는 버퍼와 같은 옵션 또는 특성을 보내고 검색 하는 데 사용 되는 버퍼에는 지정 된 옵션에 따라 고정 된 형식이 있습니다. 드라이버는 데이터 버퍼가이 형식 이라고 가정 합니다. 이 형식의 버퍼를 할당 하는 것은 응용 프로그램의 책임입니다. 예를 들어 다음 **SQLGetInfo**호출에서 드라이버는 SQL_STRING_FUNCTIONS 옵션에 필요한 것 이기 때문에 버퍼가 32 비트 정수일 것으로 가정 합니다.  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 드라이버는 C 데이터 형식을 사용 하 여 버퍼의 데이터를 해석 합니다.
