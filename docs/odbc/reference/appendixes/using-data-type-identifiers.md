---
title: 데이터 형식 식별자 사용 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b5e9fea64986bf595676540d74bb87a6e62521c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070011"
---
# <a name="using-data-type-identifiers"></a>데이터 형식 식별자 사용
응용 프로그램은 두 가지 방법으로 데이터 형식 식별자를 사용 합니다. 즉, 드라이버에 대 한 버퍼를 설명 하 고 드라이버에서 결과 집합에 대 한 메타 데이터를 검색 하 여 데이터를 저장 하는 데 사용할 C 버퍼 형식을 결정할 수 있습니다. 응용 프로그램은 다음 함수를 호출 하 여 이러한 작업을 수행 합니다.  
  
-   **SQLBindParameter**, **SQLBindCol**및 **SQLGetData** -응용 프로그램 버퍼의 C 데이터 형식을 설명 합니다.  
  
-   **SQLBindParameter** -동적 매개 변수의 SQL 데이터 형식에 대해 설명 합니다.  
  
-   **Sqlcolattribute** 및 **SQLDescribeCol** -결과 집합 열의 SQL 데이터 형식을 검색 합니다.  
  
-   **SQLDescribeParameter** -SQL 데이터 형식의 매개 변수를 검색 합니다.  
  
-   **Sqlcolumns**, **SQLProcedureColumns**및 **SQLSpecialColumns** -다양 한 스키마 정보의 SQL 데이터 형식 검색  
  
-   **SQLGetTypeInfo** -지원 되는 데이터 형식의 목록을 검색 하려면  
  
 데이터 형식 식별자는 설명자의 SQL_DESC_CONCISE_TYPE 필드에 저장 됩니다. **SQLSetDescField** 및 **SQLSetDescRec** 설명자 함수를 적절 한 형식과 함께 사용 하 여 이전 목록에 나열 된 작업을 수행할 수 있습니다. 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)를 참조 하세요.
