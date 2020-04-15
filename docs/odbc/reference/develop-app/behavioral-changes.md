---
title: 행동 변화 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e4a433531d90eb0f89d9a5e446464b13fd02526
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283443"
---
# <a name="behavioral-changes"></a>동작 변경
동작 변경은 인터페이스의 *구문이* 동일하게 유지되지만 *의미 체계가* 변경된 변경 내용입니다. 이러한 변경의 경우 ODBC 2에 사용되는 기능입니다. *x는* ODBC 3의 동일한 기능과 다르게 행동합니다. *x*.  
  
 응용 프로그램이 ODBC 2를 나타내는지 여부입니다. *x* 동작 또는 ODBC 3. *x* 동작은 SQL_ATTR_ODBC_VERSION 환경 특성에 의해 결정됩니다. 이 32비트 값은 ODBC 2를 나타내기 위해 SQL_OV_ODBC2 설정됩니다. *odBC* 3을 나타내기 위해 SQL_OV_ODBC3. *x* 동작.  
  
 SQL_ATTR_ODBC_VERSION 환경 특성은 **SQLSetEnvAttr**에 대한 호출에 의해 설정됩니다. 응용 프로그램이 **SQLAllocHandle을** 호출하여 환경 핸들을 할당한 후**SQLSetEnvAttr을** 즉시 호출하여 나타나는 동작을 설정해야 합니다. 따라서 할당되었지만 버전이 없는 상태에서 환경 핸들을 설명하는 새 환경 상태가 있습니다. 자세한 내용은 [부록 B: ODBC 상태 전환 테이블을](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조하십시오.  
  
 응용 프로그램은 SQL_ATTR_ODBC_VERSION 환경 특성과 함께 나타나는 동작을 명시하지만 이 특성은 ODBC 2와 응용 프로그램의 연결에 영향을 주지 않습니다. *x* 또는 ODBC 3. *x* 드라이버. ODBC 3. *x* 응용 프로그램은 ODBC 2 중 하나에 연결할 수 있습니다. *x* 또는 3. *x* 드라이버, 환경 특성의 설정에 상관없이.  
  
 ODBC 3. *x* 응용 프로그램은 **SQLAllocEnv를**호출해서는 안됩니다. 결과적으로 드라이버 **관리자SQLAllocEnv에**대 한 호출을 수신 하는 경우 ODBC 2로 응용 프로그램을 인식 합니다. *x* 응용 프로그램.  
  
 SQL_ATTR_ODBC_VERSION 특성은 ODBC 3의 세 가지 측면에 영향을 줍니다. *x* 드라이버의 동작:  
  
-   SQLSTATE  
  
-   날짜, 시간 및 타임스탬프에 대한 데이터 유형  
  
-   **SQLTable의** *카탈로그 이름* 인수는 ODBC 3의 검색 패턴을 허용합니다. *x*, 하지만 ODBC 2에서. *x*  
  
 SQL_ATTR_ODBC_VERSION 환경 특성의 설정은 **SQLSetParam** 또는 **SQLBindParam**에 영향을 주지 않습니다. **SQLColAttribute도** 이 비트의 영향을 받지 않습니다. **SQLColAttributeODBC** 버전(날짜 유형, 정밀도, 축척 및 길이)의 영향을 받는 특성을 반환하지만 의도된 동작은 *FieldIdentifier* 인수의 값에 의해 결정됩니다. *필드식별자가* SQL_DESC_TYPE 같으면 **SQLColAttribute는** ODBC 3을 반환합니다. 날짜, 시간 및 타임스탬프에 대한 *x* 코드; *필드식별자가* SQL_COLUMN_TYPE 같으면 **SQLColAttribute는** ODBC 2를 반환합니다. *날짜,* 시간 및 타임스탬프에 대한 x 코드입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLSTATE 매핑(SQLSTATE Mappings)](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [날짜/시간 데이터 형식 변경](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
