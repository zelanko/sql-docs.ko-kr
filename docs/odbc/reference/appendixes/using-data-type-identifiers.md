---
title: 데이터 형식 식별자를 사용 하 여 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f14294b76fc7977de256697c730f7dca31e7a469
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735133"
---
# <a name="using-data-type-identifiers"></a>데이터 형식 식별자 사용
두 가지 방법으로 데이터 형식 식별자를 사용 하는 응용 프로그램: 드라이버에 해당 버퍼를 설명 하 고 결과 데이터를 저장 하는 데 어떤 유형의 C 버퍼링 확인할 수 있도록 드라이버 집합에 대 한 메타 데이터를 검색 합니다. 이러한 작업을 수행 하려면 다음 함수를 호출 하는 응용 프로그램:  
  
-   **SQLBindParameter**, **SQLBindCol**, 및 **SQLGetData** -응용 프로그램 버퍼의 C 데이터 형식에 설명 합니다.  
  
-   **SQLBindParameter** -동적 매개 변수의 SQL 데이터 형식에 설명 합니다.  
  
-   **SQLColAttribute** 하 고 **SQLDescribeCol** -SQL 데이터 형식의 결과 집합 열을 검색 합니다.  
  
-   **Sqldescribeparameter가** -SQL 데이터 형식의 매개 변수를 검색 합니다.  
  
-   **SQLColumns**, **SQLProcedureColumns**, 및 **SQLSpecialColumns** -SQL 데이터 형식의 다양 한 스키마 정보를 검색 합니다.  
  
-   **SQLGetTypeInfo** -지원 되는 데이터 형식의 목록을 검색 하려면  
  
 데이터 형식 식별자는 설명자의 SQL_DESC_CONCISE_TYPE 필드에 저장 됩니다. 설명자 함수 **SQLSetDescField** 하 고 **SQLSetDescRec** 이전 목록에 나열 된 작업을 수행 하 여 적합 한 형식을 사용 하 여 사용할 수 있습니다. 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.
