---
title: "데이터 형식 식별자를 사용 하 여 | Microsoft Docs"
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
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f29b6e27866b5893c6875ee5c438d7c13a996e9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-data-type-identifiers"></a>데이터 형식 식별자를 사용 하 여
응용 프로그램 데이터 형식 식별자를 사용 하 여 두 가지 방법으로: 드라이버에 해당 버퍼를 설명 하 고 결과 데이터를 저장 하는 데 어떤 유형의 C 버퍼링 확인할 수 있는 드라이버에서 집합에 대 한 메타 데이터를 검색 합니다. 이러한 작업을 수행 하려면 다음 함수를 호출 하는 응용 프로그램:  
  
-   **SQLBindParameter**, **SQLBindCol**, 및 **SQLGetData** -응용 프로그램 버퍼의 C 데이터 형식을 설명 합니다.  
  
-   **SQLBindParameter** -동적 매개 변수의 SQL 데이터 형식을 설명 합니다.  
  
-   **SQLColAttribute** 및 **SQLDescribeCol** -결과 집합 열의 SQL 데이터 형식을 검색 하 합니다.  
  
-   **SQLDescribeParameter** -SQL 데이터 형식 매개 변수를 검색할 수 있습니다.  
  
-   **SQLColumns**, **SQLProcedureColumns**, 및 **SQLSpecialColumns** -를 SQL 데이터 형식의 다양 한 스키마 정보를 검색 합니다.  
  
-   **SQLGetTypeInfo** -지원 되는 데이터 형식 목록을 검색  
  
 데이터 형식 식별자가 설명자의 SQL_DESC_CONCISE_TYPE 필드에 저장 됩니다. 설명자 함수 **SQLSetDescField** 및 **SQLSetDescRec** 위 목록에 나열 된 작업을 수행할 적절 한 형식과 함께 사용할 수 있습니다. 자세한 내용은 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.

