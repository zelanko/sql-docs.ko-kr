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
ms.openlocfilehash: 748347b0a5b20f22cf7191213c59d2879df67522
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118724"
---
# <a name="c-data-types-in-odbc"></a>ODBC의 C 데이터 형식
ODBC는 응용 프로그램 변수 및 해당 형식 식별자에 사용 되는 C 데이터 형식을 정의 합니다. 이러한 매개 변수는 결과 집합 열 및 문 매개 변수에 바인딩된 버퍼에 사용 됩니다. 예를 들어 응용 프로그램이 결과 집합 열에서 문자 형식으로 데이터를 검색 하려고 한다고 가정 합니다. SQLCHAR * 데이터 형식을 사용 하 여 변수를 선언 하 고이 변수를 형식 식별자가 SQL_C_CHAR 인 결과 집합 열에 바인딩합니다. C 데이터 형식 및 형식 식별자의 전체 목록은 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.  
  
 또한 ODBC는 각 SQL 데이터 형식에서 C 데이터 형식으로의 기본 매핑을 정의 합니다. 예를 들어 데이터 소스에서 2 바이트 정수는 응용 프로그램에서 2 바이트 정수로 매핑됩니다. 기본 매핑을 사용 하기 위해 응용 프로그램에서는 SQL_C_DEFAULT 형식 식별자를 지정 합니다. 그러나 상호 운용성을 위해이 식별자를 사용 하지 않는 것이 좋습니다.  
  
 ODBC 1.x에 정의 된 모든 정수 C 데이터 형식이 서명 *되었습니다.* 부호 없는 C 데이터 형식과 해당 형식 식별자는 ODBC 2.0에 추가 되었습니다. 이러한 이유로 응용 프로그램 및 드라이버는 1.x 버전을 처리할 때 특히 주의 해야 *합니다.*  
  
## <a name="c-data-type-extensibility"></a>C 데이터 형식 확장성  
 ODBC 3.8에서는 드라이버 관련 C 데이터 형식을 지정할 수 있습니다. 이렇게 하면 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)또는 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)를 호출할 때 ODBC 응용 프로그램에서 SQL 형식을 드라이버별 C 형식으로 바인딩할 수 있습니다. 기존 C 데이터 형식이 새 서버 데이터 형식을 올바르게 나타내지 않을 수 있기 때문에 새 서버 유형을 지 원하는 데 유용할 수 있습니다. 드라이버별 C 유형을 사용 하면 드라이버에서 수행할 수 있는 변환 수가 늘어날 수 있습니다.  
  
 예를 들어 DBMS (데이터베이스 관리 시스템)에 새 SQL 유형인 **DATETIMEOFFSET**이 도입 되어 표준 시간대 정보가 포함 된 날짜 및 시간을 나타냅니다. ODBC에는 **DATETIMEOFFSET**으로 속하는지를 특정 C 형식이 없습니다. 응용 프로그램은 **DATETIMEOFFSET** 을 SQL_C_BINARY로 바인딩하고 사용자 정의 데이터 형식으로 캐스팅 해야 합니다. C 데이터 형식 확장성을 사용 하는 ODBC 3.8부터 드라이버는 새로운 해당 C 유형을 정의할 수 있습니다. 예를 들어 새 SQL 유형인 DATETIMEOFFSET의 경우 드라이버는 SQL_C_DATETIMEOFFSET 같은 새로운 해당 C 유형을 정의할 수 있습니다. 그런 다음 응용 프로그램은 새 SQL 형식을 드라이버별 C 형식으로 바인딩할 수 있습니다.  
  
 C 데이터 형식은 드라이버에서 다음과 같이 정의 됩니다.  
  
-   응용 프로그램, ODBC 드라이버 및 드라이버 관리자에 대 한 ODBC 호환성 수준은 3.8 이상입니다.  
  
-   드라이버 관련 C 형식의 데이터 범위는 0x4000에서 0x7FFF 사이입니다.  
  
-   드라이버는 C 유형에 해당 하는 데이터의 구조를 정의 합니다.  드라이버 관련 SDK에서이 작업을 수행할 수 있습니다.  
  
 드라이버 관리자는 0x4000 및 0x7FFF의 범위에 정의 된 C 형식의 유효성을 검사 하지 않습니다. 드라이버는 유효성 검사 및 모든 데이터 형식 변환을 수행 합니다. 하지만 드라이버 관리자에 전달 된 C 형식의 데이터 범위가 지 수와 0x3FFF 사이 이거나 0x8000에서 0xFFFF 사이인 경우 드라이버 관리자는 C 데이터 형식의 유효성을 검사 합니다.  
  
> [!NOTE]  
>  드라이버 관련 C 데이터 형식은 드라이버 설명서에 설명 되어 있습니다.  
  
 ODBC 준수 수준을 3.8로 지정 하기 위해 응용 프로그램은 SQL_ATTR_ODBC_VERSION 특성이 **SQL_OV_ODBC3_80**로 설정 된 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) 를 호출 합니다. 드라이버의 버전을 확인 하기 위해 응용 프로그램은 SQL_DRIVER_ODBC_VER를 사용 하 여 **SQLGetInfo** 를 호출 합니다.  
  
 ODBC 3.8에 대 한 자세한 내용은 [odbc 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)을 참조 하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)
