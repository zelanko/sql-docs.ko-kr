---
title: Odbc에서 C 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 384f26d8fa33d956582caecf8c6e0911e96a23d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911728"
---
# <a name="c-data-types-in-odbc"></a>Odbc에서 C 데이터 형식
ODBC 응용 프로그램 변수 및 해당 되는 형식 id에서 사용 되는 C 데이터 형식을 정의 합니다. 이러한 문 매개 변수 및 결과 집합 열에 바인딩된 버퍼에서 사용 됩니다. 예를 들어, 응용 프로그램에서 문자 형식으로 결과 집합 열에서 데이터를 검색 하려고 합니다. SQLCHAR 사용 하 여 변수를 선언 * 데이터 입력 하 고이 변수를 SQL_C_CHAR의 형식 식별자를 가진 결과 집합 열에 바인딩합니다. C 데이터 형식 및 유형 식별자의 전체 목록은 참조 하십시오. [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.  
  
 ODBC C 데이터 형식으로 각 SQL 데이터 형식에서 기본 매핑을 정의합니다. 예를 들어 데이터 원본에 2 바이트 정수는 2 바이트 정수 응용 프로그램에 매핑됩니다. 기본 매핑을 사용 하려면 응용 프로그램 SQL_C_DEFAULT 유형 식별자를 지정 합니다. 그러나이 식별자의 사용은 상호 운용성의 이유로 권장 되지 않습니다.  
  
 ODBC 1에 정의 된 모든 정수 C 데이터 형식과 *.x* 서명 되었습니다. 부호 없는 C 데이터 형식 및 해당 되는 형식 id ODBC 2.0에서 추가 되었습니다. 이 인해 응용 프로그램 및 드라이버 필요한 1 다룰 때는 특히 주의를 기울여야 *.x* 버전입니다.  
  
## <a name="c-data-type-extensibility"></a>C 데이터 형식 확장성  
 ODBC 3.8 드라이버 관련 C 데이터 형식을 지정할 수 있습니다. 이렇게 하면 호출 하는 경우 SQL 형식 ODBC 응용 프로그램에서 드라이버 관련 C 형식으로 바인딩할 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), 또는 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)합니다. 이 기존 C 데이터 형식은 새로운 서버 데이터 형식에 제대로 나타나지 않을 수 있습니다 때문에 새 서버 유형을 지 원하는 데 유용할 수 있습니다. 드라이버 관련 C 형식을 사용 하 여 드라이버 수행할 수 있는 변환의 수를 늘릴 수 있습니다.  
  
 예를 들어, 데이터베이스 관리 시스템 (DBMS)에 새 SQL 형식에 도입 된 **DATETIMEOFFSET**날짜 및 시간 표준 시간대 정보로를 나타내기 위해. 에 상응 하는 ODBC에서 특정 C 유형이 없습니다 것 **DATETIMEOFFSET**합니다. 응용 프로그램은 바인딩해야 할 **DATETIMEOFFSET** SQL_C_BINARY 및 캐스트에 대 한 사용자 정의 데이터 형식입니다. 부터는 ODBC 3.8에서 C 데이터 형식 확장성 하 여 드라이버를 새 해당 C 형식을 정의할 수 있습니다. 예를 들어 새 SQL 형식이 DATETIMEOFFSET에 대 한 드라이버 SQL_C_DATETIMEOFFSET 같은 새 해당 C 형식을 정의할 수 있습니다. 그런 다음 응용 프로그램 드라이버 관련 C 형식으로 새 SQL 형식을 바인딩할 수 있습니다.  
  
 드라이버에서 C 데이터 형식은 다음과 같이 정의 됩니다.  
  
-   응용 프로그램, ODBC 드라이버 및 드라이버 관리자는 ODBC 호환성 수준은 3.8 (또는 이상)입니다.  
  
-   드라이버 관련 C 형식의 데이터 범위는 0x4000 사이 0x7FFF입니다.  
  
-   드라이버는 C 형식에 해당 하는 데이터의 구조를 정의 합니다.  드라이버 관련 SDK에서이 작업을 수행할 수 있습니다.  
  
 드라이버 관리자 0x4000 및 0x7FFF;의 범위에 정의 된 C 형식 유효성 검사 되지 않습니다. 드라이버는 유효성 검사 및 데이터 형식 변환을 모두 수행 합니다. 하지만 드라이버 관리자에 게 전달 되는 C 형식의 데이터 범위 또는 0x8000와 0xFFFF 0x0000 0x3FFF 사이 이면 드라이버 관리자 C 데이터 형식의 유효성을 검사 합니다.  
  
> [!NOTE]  
>  드라이버 관련 C 데이터 형식은 드라이버 설명서에 기술 해야 합니다.  
  
 3.8의 ODBC 준수 수준을 지정 하려면 응용 프로그램이 호출 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) 는 SQL_ATTR_ODBC_VERSION 특성은로 설정 **SQL_OV_ODBC3_80**합니다. 드라이버의 버전을 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_DRIVER_ODBC_VER 사용 합니다.  
  
 ODBC 3.8에 대 한 자세한 내용은 참조 [What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)
