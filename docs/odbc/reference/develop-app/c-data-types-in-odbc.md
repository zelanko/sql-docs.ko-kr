---
title: ODBC의 C 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5472595383c7e4fcf448374c1fd85587246328f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199215"
---
# <a name="c-data-types-in-odbc"></a>ODBC의 C 데이터 형식
ODBC 응용 프로그램 변수 및 해당 형식 식별자에서 사용 되는 C 데이터 형식을 정의 합니다. 이러한 문 매개 변수 및 결과 집합 열에 바인딩된 버퍼에 사용 됩니다. 예를 들어, 응용 프로그램에서 문자 형식으로 결과 집합 열에서 데이터를 검색 하려고 합니다. SQLCHAR 사용 하 여 변수 선언 * 데이터 형식으로이 변수를 SQL_C_CHAR의 형식 식별자를 사용 하 여 결과 집합 열에 바인딩합니다. C 데이터 형식 및 형식 식별자의 전체 목록은 참조 하세요. [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.  
  
 ODBC C 데이터 형식으로 각 SQL 데이터 형식에서 기본 매핑을 정의합니다. 예를 들어, 데이터 원본에는 2 바이트 정수는 2 바이트 정수 응용 프로그램에 매핑됩니다. 기본 매핑을 사용 하려면 응용 프로그램의 SQL_C_DEFAULT 형식 식별자를 지정 합니다. 그러나이 식별자의 사용은 상호 운용성의 이유로 권장 되지 않습니다.  
  
 ODBC 1에 정의 된 모든 정수 C 데이터 형식 *.x* 서명 되었습니다. 부호 없는 C 데이터 형식 및 해당 형식 식별자는 ODBC 2.0에 추가 되었습니다. 이 인해 응용 프로그램 및 드라이버 필요 1을 사용 하 여 처리 하는 경우에 특히 주의를 기울여야 *.x* 버전입니다.  
  
## <a name="c-data-type-extensibility"></a>C 데이터 형식 확장성  
 ODBC 3.8의 드라이버 관련 C 데이터 형식을 지정할 수 있습니다. 이렇게 하면 호출 하는 경우 SQL 형식에서 ODBC 응용 프로그램은 드라이버별 C 형식으로 바인딩할 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)를 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), 또는 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)합니다. 이 기존 C 데이터 형식을 새 서버 데이터 형식에 제대로 나타나지 않을 수 있습니다 때문에 새 서버 유형을 지원 하기 위해 유용할 수 있습니다. 드라이버별 C 형식을 사용 하 여 드라이버를 수행할 수 있는 변환의 수를 늘릴 수 있습니다.  
  
 예를 들어, 데이터베이스 관리 시스템 (DBMS) 새 SQL 형식에 도입 **DATETIMEOFFSET**를 날짜 및 표준 시간대 정보를 사용 하 여 시간을 나타냅니다. 에 해당 하는 ODBC에서 특정 C 유형이 없습니다 것 **DATETIMEOFFSET**합니다. 응용 프로그램을 바인딩할 필요가 **DATETIMEOFFSET** SQL_C_BINARY로 캐스팅 하는 사용자 정의 데이터 형식입니다. C 데이터 형식 확장성을 사용 하 여 ODBC 3.8부터, 드라이버는 새 해당 C 형식을 정의할 수 있습니다. 예를 들어 새 SQL 형식 DATETIMEOFFSET에 대해 드라이버 SQL_C_DATETIMEOFFSET 같은 새 해당 C 형식을 정의할 수 있습니다. 그런 다음 응용 프로그램 드라이버별 C 형식으로 새 SQL 형식에 바인딩할 수 있습니다.  
  
 C 데이터 형식 드라이버에서 다음과 같이 정의 됩니다.  
  
-   ODBC 규정 준수는 응용 프로그램, ODBC 드라이버 및 드라이버 관리자에 대 한 수준이 3.8 (또는 이상)입니다.  
  
-   드라이버별 C 형식 데이터 범위의 0x4000 사이 0x7FFF입니다.  
  
-   드라이버 C 형식에 해당 하는 데이터의 구조를 정의 합니다.  드라이버 관련 SDK에서이 수행할 수 있습니다.  
  
 드라이버 관리자 0x4000 및 0x7FFF; 범위에 정의 된 C 형식 검사 하지 않으며 드라이버는 모든 데이터 형식 변환 및 유효성 검사를 수행 합니다. 하지만 드라이버 관리자에 게 전달 되는 C 형식 데이터 범위의 0x0000 0x3FFF 사이 또는 0x8000 0xFFFF 사이 이면 드라이버 관리자 C 데이터 형식의 유효성을 검사 합니다.  
  
> [!NOTE]  
>  드라이버 관련 C 데이터 형식 드라이버 설명서에서 설명 합니다.  
  
 3\.8의 ODBC 준수 수준을 지정 하는 응용 프로그램 호출 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) 를 SQL_ATTR_ODBC_VERSION으로 설정 특성 **SQL_OV_ODBC3_80**합니다. 드라이버의 버전을 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_DRIVER_ODBC_VER를 사용 하 여 합니다.  
  
 ODBC 3.8에 대 한 자세한 내용은 참조 하세요. [What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)
