---
title: "응용 프로그램 &#39; 선언 ODBC 버전 s | Microsoft Docs"
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
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32bfeff983ef5dff4ebfe3e575bcf36e855184d0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="declaring-the-application39s-odbc-version"></a>응용 프로그램 &#39; 선언 s ODBC 버전
응용 프로그램이 할당 한 연결을 전에 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 합니다. 이 특성은 응용 프로그램이 ODBC 2 따르는지를 알려 줍니다. *x* 또는 ODBC 3. *x* 사양에 다음 항목을 사용 하는 경우:  
  
-   **Sqlstate**합니다. SQLSTATE 값이 많은 ODBC 2에서 서로 다릅니다. *x* 및 ODBC 3. *x*합니다.  
  
-   **날짜, 시간 및 타임 스탬프 형식 식별자**합니다. 다음 표에서 날짜, 시간 및 ODBC 2의 타임 스탬프 데이터에 대 한 형식 식별자를 보여 줍니다. *x* 및 ODBC 3. *x*합니다.  
  
    |ODBC 2입니다. *x*|ODBC 3입니다. *x*|  
    |----------------|----------------|  
    |**SQL 유형 식별자**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 형식 식별자**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   *CatalogName***SQLTables 인수**합니다.   Odbc 2. *x*에서 와일드 카드 문자 ("%" 및 "_")는 *CatalogName* 인수 리터럴로 취급 됩니다. Odbc 3. *x*, 와일드 카드 문자로 처리 됩니다. 따라서 응용 프로그램 뒤에 오는 ODBC 2. *x* 사양을 사용할 수 없습니다. 이러한 와일드 카드 문자는 문자를 리터럴로 사용 하는 경우 이러한 이스케이프 하지 않습니다. ODBC 3 다음에 나오는 응용 프로그램입니다. *x* 사양이 와일드 카드 문자로 사용 하 여 또는 이스케이프 고, 리터럴로 사용할 수 있습니다. 자세한 내용은 참조 [카탈로그 함수의 인수와](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 ODBC 3*.x* 드라이버 관리자와 ODBC 3*.x* 드라이버는 응용 프로그램이 작성 되는 ODBC 사양의 버전을 확인 하 고 적절 하 게 응답 합니다. 예를 들어 응용 프로그램이 ODBC 2를 따릅니다. *x* 사양 및 호출 **SQLExecute** 호출 하기 전에 **SQLPrepare**, ODBC 3*.x* 드라이버 관리자 SQLSTATE S1010 (반환 함수 시퀀스 오류)입니다. 응용 프로그램 뒤 ODBC 3*.x* 사양에서는 드라이버 관리자 반환 SQLSTATE HY010 (함수 시퀀스 오류). 자세한 내용은 참조 [이전 버전과 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)합니다.  
  
> [!IMPORTANT]  
>  ODBC 3 다음에 나오는 응용 프로그램입니다. *x* 사양 ODBC 3 새 기능을 사용 하지 않는 조건부 코드를 사용 해야 합니다. *x* ODBC 2 작업할 때. *x* 드라이버입니다. ODBC 2입니다. *x* 드라이버는 ODBC 3 새 기능을 지원 하지 않습니다. *x* 해 서 응용 프로그램 선언 ODBC 3을 따릅니다. *x* 사양입니다. 또한 ODBC 3. *x* ODBC 3 새 기능을 지 원하는 드라이버를 중단 하지 않습니다. *x* 응용 프로그램을 ODBC 2 따릅니다 선언 해 서. *x* 사양입니다.

