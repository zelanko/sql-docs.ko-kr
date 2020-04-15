---
title: 응용 프로그램 선언&#39;ODBC 버전 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba346ed7f7a261446110c5513026d20a86fd3a19
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285233"
---
# <a name="declaring-the-application39s-odbc-version"></a>응용 프로그램 선언&#39;ODBC 버전
응용 프로그램이 연결을 할당하기 전에 SQL_ATTR_ODBC_VERSION 환경 특성을 설정해야 합니다. 이 특성은 응용 프로그램이 다음 항목을 사용할 때 ODBC *2.x* 또는 ODBC *3.x* 사양을 따른다는 것을 명시합니다.  
  
-   **SQLSTATEs**. 많은 SQLSTATE 값은 ODBC *2.x* 및 ODBC *3.x에서*다릅니다.  
  
-   **날짜, 시간 및 타임스탬프 유형 식별자**. 다음 표에서는 ODBC *2.x* 및 ODBC *3.x의*날짜, 시간 및 타임스탬프 데이터에 대한 형식 식별자를 보여 주며 있습니다.  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**SQL 형식 식별자**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 유형 식별자**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_**SQLTable의**카탈로그 이름 인수 .   ODBC *2.x에서* *카탈로그 이름* 인수의 와일드카드 문자("%" 및 "_")는 문자 그대로 처리됩니다. ODBC *3.x에서는*와일드카드 문자로 처리됩니다. 따라서 ODBC *2.x* 사양을 따르는 응용 프로그램은 이러한 문자를 와일드카드 문자로 사용할 수 없으며 리터럴로 사용할 때이 작업을 이스케이프하지 않습니다. ODBC *3.x* 사양을 따르는 응용 프로그램은 이러한 문자를 와일드카드 문자로 사용하거나 이스케이프하여 리터럴로 사용할 수 있습니다. 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.  
  
 ODBC *3.x* 드라이버 관리자와 ODBC *3.x* 드라이버는 응용 프로그램이 작성되고 그에 따라 응답하는 ODBC 사양 의 버전을 확인합니다. 예를 들어 응용 프로그램이 ODBC *2.x* 사양을 따르고 **SQLPrepare를**호출하기 전에 **SQLExecute를** 호출하는 경우 ODBC *3.x* 드라이버 관리자는 SQLSTATE S1010(함수 시퀀스 오류)을 반환합니다. 응용 프로그램이 ODBC *3.x* 사양을 따르는 경우 드라이버 관리자는 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. 자세한 내용은 [이전 버전과의 호환성 및 표준 준수를](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)참조하십시오.  
  
> [!IMPORTANT]  
>  ODBC *3.x* 사양을 따르는 응용 프로그램은 ODBC *2.x* 드라이버로 작업할 때 ODBC *3.x에* 새로운 기능을 사용하지 않도록 조건부 코드를 사용해야 합니다. ODBC 2.x 드라이버는 응용 프로그램이 ODBC *3.x* 사양을 따른다고 선언하기 때문에 ODBC *3.x에* 새로운 기능을 지원하지 않습니다. *3.x* 또한 ODBC *3.x* 드라이버는 응용 프로그램이 ODBC *2.x* 사양을 따른다고 선언한다고 선언하기 때문에 ODBC *3.x에* 새로운 기능을 지원하지 않습니다.
