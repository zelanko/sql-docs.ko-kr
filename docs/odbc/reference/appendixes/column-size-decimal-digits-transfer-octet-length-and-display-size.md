---
title: 열 크기, 십진수, 8 진수 길이 전송 크기를 표시 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8d7f1b8ec5647a34b09f0636fc8fcc2ad070f72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019246"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>열 크기, 십진수, 8 진수 길이 전송 및 표시 크기-ODBC
데이터 형식 열 (또는 매개 변수) 크기, 소수 자릿수, 길이 따라 구분 됩니다 및 크기를 표시 합니다. 다음 ODBC 함수는 데이터 원본에 대해 SQL 문에서 매개 변수 또는 SQL 데이터 형식을 위한 이러한 특성을 반환합니다. 각 ODBC 함수는 다음과 같은 다양 한 이러한 특성을 반환합니다.  
  
-   **SQLDescribeCol** 설명 열의 크기 및 소수 자릿수는 열을 반환 합니다.  
  
-   **SQLDescribeParam** 크기 및 소수 자릿수에 설명 하는 매개 변수를 매개 변수를 반환 합니다. **SQLBindParameter** SQL 문에서 매개 변수는 매개 변수에 대 한 크기 및 소수 자릿수를 설정 합니다.  
  
-   카탈로그 함수 **SQLColumns**를 **SQLProcedureColumns**, 및 **SQLGetTypeInfo** 테이블, 결과 집합 또는 프로시저 매개 변수 열에 대 한 특성을 반환 하 고 데이터 원본에서 데이터 형식의 카탈로그 특성입니다. **SQLColumns** (예: 기본 테이블, 뷰 또는 시스템 테이블)에 지정 된 테이블에서 열 크기, 소수 자릿수 및 열의 길이 반환 합니다. **SQLProcedureColumns** 프로시저에서 열 크기, 소수 자릿수와 열의 길이 반환 합니다. **SQLGetTypeInfo** 데이터 원본에 대해 최대 열 크기와 SQL 데이터 형식의 최소 및 최대 10 진수 숫자를 반환 합니다.  
  
 열에 대 한 이러한 함수에서 반환 된 값 또는 "정밀도"로 ODBC 2에 정의 된 매개 변수 크기에 해당 합니다. *x*합니다. 그러나 SQL_DESC_PRECISION 또는 다른 하나의 설명자 필드에서 반환 되는 값에 값을 반드시 일치 하지 않습니다. "Scale"로 ODBC 2에 정의 된에 해당 하는 소수 자릿수에 대 한도 마찬가지입니다. *x*합니다. 자릿수가 SQL_DESC_SCALE 또는 다른 하나의 설명자 필드를 반환 하는 값을 따르지 않을 않지만 데이터 형식에 따라 다른 설명자 필드에서 제공 됩니다. 자세한 내용은 참조 하세요. [열 크기](../../../odbc/reference/appendixes/column-size.md) 하 고 [진수](../../../odbc/reference/appendixes/decimal-digits.md)합니다.  
  
 마찬가지로, 8 진수 길이 전송에 대 한 값 SQL_DESC_LENGTH에서 제공 되지 않습니다. 이러한 모든 문자 및 이진 형식에 대 한 설명자 필드의 SQL_DESC_OCTET_LENGTH에서 제공 됩니다. 다른 유형에 대 한이 정보를 포함 하는 설명자 필드가 있습니다.  
  
 모든 데이터 형식에 대 한 표시 크기 값 SQL_DESC_DISPLAY_SIZE 단일 설명자 필드의 값에 해당합니다.  
  
 설명자 필드는 결과 집합의 특징을 설명 합니다. 설명자 필드는 문 실행 하기 전에 데이터에 대 한 유효한 값을 포함 하지 않습니다. 열에 대 한 값 10 진수 숫자, 크기 및 표시 크기 반환한 **SQLColumns**를 **SQLProcedureColumns**, 및 **SQLGetTypeInfo**반면 다른 반환, 데이터 원본의 카탈로그에 있는 테이블 열과 데이터 형식 등의 데이터베이스 개체의 특성입니다. 해당 결과 집합에 마찬가지로 **SQLColAttribute** 열 크기, 소수 자릿수 및 데이터 소스에 있는 열의 8 진수 길이 전송 반환이 하나일 필요가 없는 SQL_ 자릿수가 SQL_DESC_PRECISION에 대 한 값과 동일 DESC_SCALE, 및 SQL_DESC_OCTET_LENGTH 설명자 필드입니다.  
  
 이러한 설명자 필드에 대 한 자세한 내용은 참조 하세요. [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.  
  
 관련 항목:  
  
-   [열 크기](../../../odbc/reference/appendixes/column-size.md)  
-   [십진수](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [8진수 길이 전송](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [표시 크기](../../../odbc/reference/appendixes/display-size.md)
