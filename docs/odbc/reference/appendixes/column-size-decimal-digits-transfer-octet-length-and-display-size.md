---
title: 열 크기, 소수 자릿수, 전송 옥텟 길이, 디스플레이 크기 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55b8e9dd305764a89601e9ffd5a337e42a8d8db3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306574"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>열 크기, 소수 자릿수, 전송 옥텟 길이 및 디스플레이 크기 - ODBC
데이터 형식은 열(또는 매개변수) 크기, 소수 자릿수, 길이 및 표시 크기를 특징으로 합니다. 다음 ODBC 함수는 SQL 문의 매개 변수 또는 데이터 원본의 SQL 데이터 형식에 대해 이러한 특성을 반환합니다. 각 ODBC 함수는 다음과 같이 다음과 같이 다른 특성 집합을 반환합니다.  
  
-   **SQLDescribeCol은** 설명하는 열의 열 크기와 소수 자릿수를 반환합니다.  
  
-   **SQLDescribeParam은** 설명하는 매개 변수의 매개 변수 크기와 소수 자릿수를 반환합니다. **SQLBindParameter는** SQL 문의 매개 변수에 대한 매개 변수 크기와 소수 자릿수를 설정합니다.  
  
-   카탈로그함수 **SQLColumns,** **SQLProcedureColumns**및 **SQLGetTypeInfo** 는 테이블, 결과 집합 또는 프로시저 매개 변수 및 데이터 원본의 데이터 형식의 카탈로그 특성에 대한 열에 대한 특성을 반환합니다. **SQLColumns는** 지정된 테이블(예: 기본 테이블, 뷰 또는 시스템 테이블)에서 열 크기, 소수 자릿수 및 열 길이를 반환합니다. **SQLProcedureColumns는** 프로시저에서 열 크기, 소수 자릿수 및 열을 반환합니다. **SQLGetTypeInfo는** 데이터 원본에서 SQL 데이터 형식의 최대 열 크기와 최소 및 최대 소수 자릿수를 반환합니다.  
  
 열 또는 매개 변수 크기에 대해 이러한 함수에서 반환되는 값은 ODBC 2에 정의된 "정밀도"에 해당합니다. *x*. 그러나 값이 SQL_DESC_PRECISION 또는 다른 한 설명자 필드에서 반환되는 값과 반드시 일치하지는 않습니다. ODBC 2에 정의된 "배율"에 해당하는 소수 자릿수의 경우도 마찬가지입니다. *x*. SQL_DESC_SCALE 또는 다른 설명자 필드에서 반환되는 값과 반드시 일치하지는 않지만 데이터 형식에 따라 다른 설명자 필드에서 제공됩니다. 자세한 내용은 [열 크기](../../../odbc/reference/appendixes/column-size.md) 및 [소수 자릿수를](../../../odbc/reference/appendixes/decimal-digits.md)참조하십시오.  
  
 마찬가지로, 전송 옥텟 길이에 대한 값은 SQL_DESC_LENGTH 오지 않는다. 모든 문자 및 이진 형식에 대한 설명자 필드의 SQL_DESC_OCTET_LENGTH 제공됩니다. 다른 형식에 대해 이 정보를 포함하는 설명자 필드가 없습니다.  
  
 모든 데이터 형식의 표시 크기 값은 단일 설명자 필드의 값에 SQL_DESC_DISPLAY_SIZE.  
  
 설명자 필드는 결과 집합의 특성을 설명합니다. 설명자 필드에는 명령문 실행 전에 데이터에 대한 유효한 값이 포함되어 있지 않습니다. 반면에 **SQLColumns,** **SQLProcedureColumns**및 **SQLGetTypeInfo에서**반환되는 열 크기, 소수 자릿수 및 표시 크기에 대한 값은 데이터 원본 카탈로그에 있는 테이블 열 및 데이터 형식과 같은 데이터베이스 개체의 특성을 반환합니다. 마찬가지로 결과 집합에서 **SQLColAttribute는** 데이터 원본에서 열 크기, 소수 자릿수 및 전송 옥텟 열 길이를 반환합니다. 이러한 값은 SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_OCTET_LENGTH 설명자 필드의 값과 반드시 같지는 않습니다.  
  
 이러한 설명자 필드에 대한 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)을 참조하십시오.  
  
 관련 항목:  
  
-   [열 크기](../../../odbc/reference/appendixes/column-size.md)  
-   [십진수](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [8진수 길이 전송](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [표시 크기](../../../odbc/reference/appendixes/display-size.md)
