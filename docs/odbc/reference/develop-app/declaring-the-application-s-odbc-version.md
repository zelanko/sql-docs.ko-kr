---
title: 응용 프로그램을 선언&#39;ODBC 버전 s | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f1dc43ee81f1be386d0518625d36464f029dc0f
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793809"
---
# <a name="declaring-the-application39s-odbc-version"></a>응용 프로그램을 선언&#39;s ODBC 버전
응용 프로그램을 연결에서 할당 전에 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 합니다. 이 특성 상태 응용 프로그램을 ODBC 따르는지 *2.x* 또는 ODBC *3.x* 사양에 다음 항목을 사용 하는 경우:  
  
-   **SQLSTATEs**. ODBC의 SQLSTATE 값이 많은 서로 *2.x* 및 ODBC *3.x*합니다.  
  
-   **날짜, 시간 및 타임 스탬프 형식 식별자**합니다. 다음 표에서 ODBC의 date, time 및 timestamp 데이터 형식 식별자를 보여 줍니다 *2.x* 및 ODBC *3.x*합니다.  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**SQL 유형 식별자**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 형식 식별자**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_**SQLTables 인수**합니다. Odbc에서 *2.x*에서 와일드 카드 문자 ("%" 및 "_")는 *CatalogName* 인수 리터럴로 처리 됩니다. Odbc에서 *3.x*에 와일드 카드 문자로 처리 됩니다. 따라서 응용 프로그램을 ODBC 따릅니다 *2.x* 사양 와일드 카드 문자 및 리터럴로 사용 하는 경우 이러한 이스케이프 하지 않으면 이러한 사용할 수 없습니다. 응용 프로그램을 ODBC 뒤에 오는 *3.x* 사양 와일드 카드 문자로 사용 하 여 또는 이스케이프할를 리터럴로 사용 합니다. 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.  
  
 ODBC *3.x* 드라이버 관리자 및 ODBC *3.x* 드라이버 응용 프로그램 기록 하는 ODBC 사양의 버전을 확인 하 고 그에 따라 응답 합니다. 예를 들어 응용 프로그램을 ODBC 따릅니다 *2.x* 사양과 호출 **SQLExecute** 호출 하기 전에 **SQLPrepare**, ODBC *3.x*드라이버 관리자 SQLSTATE S1010 반환 (함수 시퀀스 오류). 응용 프로그램 뒤 ODBC *3.x* 사양 드라이버 관리자 반환 SQLSTATE HY010 (함수 시퀀스 오류). 자세한 내용은 [이전 버전과 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)합니다.  
  
> [!IMPORTANT]  
>  ODBC를 따르는 응용 프로그램 *3.x* 사양 odbc 새 기능을 사용 하지 않는 조건부 코드를 사용 해야 *3.x* ODBC를 사용 하 여 작업 하는 경우 *2.x* 드라이버입니다. ODBC *2.x* 드라이버는 ODBC에 새 기능을 지원 하지 않습니다 *3.x* 해 서 응용 프로그램을 ODBC 따릅니다 선언 *3.x* 사양입니다. 또한 ODBC *3.x* odbc 새 기능을 지 원하는 드라이버 멈추지 마십시오 *3.x* 해 서 응용 프로그램을 ODBC 따릅니다 선언 *2.x* 사양입니다.
