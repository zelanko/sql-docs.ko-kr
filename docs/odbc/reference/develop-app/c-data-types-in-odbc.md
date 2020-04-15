---
title: ODBC의 C 데이터 유형 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e1efba2187e2c1f2d813d43640fc9259ad4f2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306298"
---
# <a name="c-data-types-in-odbc"></a>ODBC의 C 데이터 형식
ODBC는 응용 프로그램 변수 및 해당 형식 식별자에 의해 사용되는 C 데이터 형식을 정의합니다. 결과 집합 열 및 문 매개 변수에 바인딩된 버퍼에서 사용 됩니다. 예를 들어 응용 프로그램이 결과 집합 열에서 문자 형식으로 데이터를 검색하려고 한다고 가정합니다. SQLCHAR * 데이터 형식을 사용 하 고 이 변수를 SQL_C_CHAR 형식 식별자를 사용 하 고 결과 집합 열에 바인딩합니다. C 데이터 유형 및 형식 식별자의 전체 목록은 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조하십시오.  
  
 ODBC는 또한 각 SQL 데이터 형식에서 C 데이터 형식에 대한 기본 매핑을 정의합니다. 예를 들어 데이터 원본의 2바이트 정수는 응용 프로그램의 2바이트 정수에 매핑됩니다. 기본 매핑을 사용 하려면 응용 프로그램은 SQL_C_DEFAULT 형식 식별자를 지정 합니다. 그러나 상호 운용성상의 이유로 이 식별자를 사용하는 것은 권장되지 않습니다.  
  
 ODBC *1.x에* 정의된 모든 정수 C 데이터 형식이 서명되었습니다. 서명되지 않은 C 데이터 형식과 해당 형식 식별자가 ODBC 2.0에 추가되었습니다. 따라서 응용 프로그램과 드라이버는 *1.x* 버전을 처리할 때 특히 주의해야 합니다.  
  
## <a name="c-data-type-extensibility"></a>C 데이터 유형 확장성  
 ODBC 3.8에서 드라이버별 C 데이터 형식을 지정할 수 있습니다. 이렇게 하면 [SQLBindCol,](../../../odbc/reference/syntax/sqlbindcol-function.md) [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)또는 SQLBindParameter 를 호출할 때 ODBC 응용 프로그램에서 드라이버 별 C 유형으로 SQL 형식을 [바인딩할 수 있습니다.](../../../odbc/reference/syntax/sqlbindparameter-function.md) 기존 C 데이터 형식이 새 서버 데이터 형식을 올바르게 나타내지 않을 수 있으므로 새 서버 형식을 지원하는 데 유용할 수 있습니다. 드라이버 별 C 유형을 사용하면 드라이버가 수행할 수 있는 전환 수를 늘릴 수 있습니다.  
  
 예를 들어 데이터베이스 관리 시스템(DBMS)이 표준 시간대 정보로 날짜와 시간을 나타내는 새 SQL **형식인 DATETIMEOFFSET을**도입했다고 가정합니다. **DATETIMEOFFSET에**해당하는 ODBC에는 특정 C 유형이 없습니다. 응용 프로그램은 **dateTIMEOFFSET을** SQL_C_BINARY 바인딩하고 사용자 정의 데이터 형식에 캐스팅해야 합니다. C 데이터 형식 확장성을 갖춘 ODBC 3.8부터 드라이버는 새 해당 C 유형을 정의할 수 있습니다. 예를 들어 새 SQL 형식 DATETIMEOFFSET의 경우 드라이버는 SQL_C_DATETIMEOFFSET 같은 새 해당 C 유형을 정의할 수 있습니다. 그런 다음 응용 프로그램은 새 SQL 형식을 드라이버 별 C 유형으로 바인딩할 수 있습니다.  
  
 C 데이터 형식은 드라이버에서 다음과 같이 정의됩니다.  
  
-   응용 프로그램, ODBC 드라이버 및 드라이버 관리자에 대한 ODBC 준수 수준은 3.8(이상)입니다.  
  
-   드라이버 별 C 유형의 데이터 범위는 0x4000에서 0x7FFF 사이입니다.  
  
-   드라이버는 C 유형에 해당하는 데이터의 구조를 정의합니다.  이 작업은 드라이버 별 SDK에서 수행할 수 있습니다.  
  
 드라이버 관리자는 0x4000 및 0x7FFF 범위에 정의된 C 형식의 유효성을 검사하지 않습니다. 드라이버는 유효성 검사 및 모든 데이터 형식 변환을 수행합니다. 그러나 드라이버 관리자에게 전달된 C 형식의 데이터 범위가 0x0000과 0x3FFF 사이이거나 0x8000과 0xFFFF 사이인 경우 드라이버 관리자는 C 데이터 형식의 유효성을 검사합니다.  
  
> [!NOTE]  
>  드라이버 관련 C 데이터 형식은 드라이버 설명서에 설명해야 합니다.  
  
 ODBC 준수 수준을 3.8로 지정하려면 응용 프로그램이 [sqlSetEnvAttr을](../../../odbc/reference/syntax/sqlsetenvattr-function.md) **SQL_OV_ODBC3_80**SQL_ATTR_ODBC_VERSION 특성으로 호출합니다. 드라이버의 버전을 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_DRIVER_ODBC_VER.  
  
 ODBC 3.8에 대한 자세한 내용은 [ODBC 3.8의 새로운 내용을](../../../odbc/reference/what-s-new-in-odbc-3-8.md)참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)
