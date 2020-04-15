---
title: 데이터 형식 식별자 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8be8eef0441d48ed03ea6ccf8f656627c1dd9b63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301424"
---
# <a name="using-data-type-identifiers"></a>데이터 형식 식별자 사용
응용 프로그램은 두 가지 방법으로 데이터 형식 식별자를 사용: 드라이버에 버퍼를 설명 하 고 데이터를 저장 하는 데 사용할 C 버퍼의 종류를 결정할 수 있도록 드라이버에서 결과 집합에 대 한 메타 데이터를 검색 합니다. 응용 프로그램은 다음 함수를 호출하여 이러한 작업을 수행합니다.  
  
-   **SQLBindParameter**, **SQLBindCol**및 **SQLGetData** - 응용 프로그램 버퍼의 C 데이터 형식을 설명합니다.  
  
-   **SQLBindParameter** - 동적 매개 변수의 SQL 데이터 형식을 설명합니다.  
  
-   **SQLColAttribute** 및 **SQLDescribeCol** - 결과 집합 열의 SQL 데이터 형식을 검색합니다.  
  
-   **SQLDescribeParameter** 매개 변수의 SQL 데이터 형식을 검색합니다.  
  
-   **SQLColumns,** **SQLProcedureColumns**및 **SQLSpecialColumns** - 다양한 스키마 정보의 SQL 데이터 형식을 검색합니다.  
  
-   **SQLGetTypeInfo** - 지원되는 데이터 형식 목록을 검색하려면  
  
 데이터 형식 식별자는 설명자의 SQL_DESC_CONCISE_TYPE 필드에 저장됩니다. 설명자 함수 **SQLSetDescField** 및 **SQLSetDescRec이전** 목록에 나열 된 작업을 수행 하기 위해 적절 한 형식과 함께 사용할 수 있습니다. 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)을 참조하십시오.
