---
description: 응용 프로그램&#39;s ODBC 버전 선언
title: 응용 프로그램&#39;s ODBC 버전 선언 | Microsoft Docs
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
ms.openlocfilehash: 0ff41a7a8b56133b0a44947980805c5b46238bad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424724"
---
# <a name="declaring-the-application39s-odbc-version"></a>응용 프로그램&#39;s ODBC 버전 선언
응용 프로그램에서 연결을 할당 하기 전에 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 해야 합니다. 이 특성은 다음 항목을 사용 하는 경우 응용 프로그램이 ODBC *2.x 또는 odbc* *2.x 사양을 따르는지* 여부를 명시 합니다.  
  
-   **Sqlstates**. 대부분의 SQLSTATE 값 *은 odbc*2.X *와 odbc* 3.x에서 다릅니다.  
  
-   **날짜, 시간 및 타임 스탬프 유형 식별자**입니다. 다음 표에서 *는 odbc* *2.x 및 odbc* 3.x의 날짜, 시간 및 타임 스탬프 데이터에 대 한 형식 식별자를 보여 줍니다.  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**SQL 형식 식별자**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 형식 식별자**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_**Sqltables의 CatalogName 인수**   *ODBC 2.x에서* *CatalogName* 인수의 와일드 카드 문자 ("%" 및 "_")는 리터럴로 취급 됩니다. *ODBC 3.x에서는 와일드*카드 문자로 처리 됩니다. 따라서 ODBC 2.x 사양을 따르는 응용 프로그램은이를 와일드 카드 문자로 사용할 수 없으며 리터럴로 사용할 때 이스케이프 되지 *않습니다.* ODBC 3.x 사양을 따르는 응용 프로그램은 이러한 문자를 와일드 카드 문자로 사용 하거나 이스케이프 처리 하 여 리터럴로 사용할 수 *있습니다.* 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.  
  
 ODBC 3.x *드라이버 관리자 및 odbc* *3.x 드라이버는* 응용 프로그램이 작성 된 odbc 사양의 버전을 확인 하 고 그에 따라 응답 합니다. 예를 들어 응용 프로그램이 ODBC *2.x 사양을 따르고* **sqlexecute**를 호출 하기 전에 **sqlexecute** 를 호출 하는 *경우 ODBC 3.X* 드라이버 관리자는 SQLSTATE S1010 (함수 시퀀스 오류)를 반환 합니다. 응용 프로그램이 ODBC *2.x 사양을 따르는* 경우 드라이버 관리자는 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. 자세한 내용은 [이전 버전과의 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)를 참조 하세요.  
  
> [!IMPORTANT]  
>  *Odbc 3.x 사양을 따르는* 응용 프로그램은 odbc 2.x *드라이버를* *사용할 때 odbc* 3.x의 새로운 기능을 사용 하지 않도록 조건부 코드를 사용 해야 합니다. Odbc *2.x 드라이버는* odbc 3.x의 새로운 기능을 지원 하지 않습니다. *x* 는 응용 프로그램이 odbc *3.x 사양을 따르는* 것으로 선언 하기 때문입니다. 또한 *odbc 3.x 드라이버는* odbc 2.x의 새 기능을 지원 하지 않습니다. *x* 는 응용 프로그램이 odbc *2.x 사양을 따르는* 것으로 선언 하기 때문입니다.
