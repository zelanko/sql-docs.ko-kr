---
title: 열 크기, 10 진수, 전송 옥텟 길이, 표시 크기 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019246"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기-ODBC
데이터 형식은 열 (또는 매개 변수) 크기, 10 진수 숫자, 길이 및 표시 크기로 구분 됩니다. 다음 ODBC 함수는 SQL 문 또는 데이터 원본의 SQL 데이터 형식에 대 한 매개 변수에 대해 이러한 특성을 반환 합니다. 각 ODBC 함수는 다음과 같이 이러한 특성의 다른 집합을 반환 합니다.  
  
-   **SQLDescribeCol** 는 설명 하는 열의 열 크기와 소수 자릿수를 반환 합니다.  
  
-   **SQLDescribeParam** 는 설명 하는 매개 변수의 크기와 소수 자릿수를 반환 합니다. **SQLBindParameter** 는 SQL 문의 매개 변수에 대 한 매개 변수 크기와 소수 자릿수를 설정 합니다.  
  
-   카탈로그 함수 **Sqlcolumns**, **SQLProcedureColumns**및 **SQLGetTypeInfo** 는 테이블의 열, 결과 집합 또는 프로시저 매개 변수 및 데이터 원본에 있는 데이터 형식의 카탈로그 특성에 대 한 특성을 반환 합니다. **Sqlcolumns** 는 지정 된 테이블 (예: 기본 테이블, 뷰 또는 시스템 테이블)에서 열 크기, 10 진수 및 열 길이를 반환 합니다. **SQLProcedureColumns** 는 프로시저의 열 크기, 10 진수 및 열 길이를 반환 합니다. **SQLGetTypeInfo** 는 데이터 원본에 대 한 SQL 데이터 형식의 최대 열 크기와 최소 및 최대 소수 자릿수를 반환 합니다.  
  
 열 또는 매개 변수 크기에 대해 이러한 함수가 반환 하는 값은 ODBC 2에 정의 된 대로 "전체 자릿수"에 해당 합니다. *x*. 그러나이 값은 SQL_DESC_PRECISION 또는 다른 하나의 설명자 필드에 반환 되는 값과 반드시 일치 하지는 않습니다. ODBC 2에 정의 된 대로 "scale"에 해당 하는 10 진수의 경우에도 마찬가지입니다. *x*. SQL_DESC_SCALE 또는 다른 하나의 설명자 필드에 반환 되는 값과 반드시 일치 하는 것은 아니지만 데이터 형식에 따라 다른 설명자 필드에서 제공 됩니다. 자세한 내용은 [열 크기](../../../odbc/reference/appendixes/column-size.md) 및 [소수 자릿수](../../../odbc/reference/appendixes/decimal-digits.md)를 참조 하세요.  
  
 마찬가지로, 전송 옥텟 길이 값은 SQL_DESC_LENGTH에서 제공 되지 않습니다. 모든 문자 및 이진 형식에 대 한 설명자의 필드 SQL_DESC_OCTET_LENGTH에서 제공 됩니다. 다른 형식에 대 한이 정보를 포함 하는 설명자 필드가 없습니다.  
  
 모든 데이터 형식의 표시 크기 값은 SQL_DESC_DISPLAY_SIZE 단일 설명자 필드의 값에 해당 합니다.  
  
 설명자 필드는 결과 집합의 특징을 설명 합니다. 설명자 필드에는 문 실행 전에 데이터에 대 한 유효한 값이 포함 되지 않습니다. 반면 **Sqlcolumns**, **SQLProcedureColumns**및 **SQLGetTypeInfo**에서 반환 하는 열 크기, 10 진수 및 표시 크기에 대 한 값은 데이터 원본의 카탈로그에 있는 테이블 열, 데이터 형식 등의 데이터베이스 개체의 특징을 반환 합니다. 마찬가지로, 결과 집합에서 **Sqlcolattribute** 는 데이터 원본에 있는 열의 크기, 10 진수 숫자 및 전송 옥텟 길이를 반환 합니다. 이러한 값은 SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_OCTET_LENGTH 설명자 필드의 값과 다를 수 있습니다.  
  
 이러한 설명자 필드에 대 한 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)를 참조 하세요.  
  
 관련 항목:  
  
-   [열 크기](../../../odbc/reference/appendixes/column-size.md)  
-   [십진수](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [8진수 길이 전송](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [표시 크기](../../../odbc/reference/appendixes/display-size.md)
