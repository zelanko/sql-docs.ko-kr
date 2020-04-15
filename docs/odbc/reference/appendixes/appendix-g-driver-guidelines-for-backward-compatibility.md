---
title: '부록 G: 이전 버전과의 호환성을 위한 드라이버 지침 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1055f94cb54bba9262f210e5df5f028029aebf5b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292403"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>부록 G: 이전 버전과의 호환성을 위한 드라이버 지침
이 부록은 ODBC 3에서 작업하는 드라이버 작성기에 대한 정보를 제공합니다. *ODBC* 2를 지원해야 하는 x 드라이버. *x* 응용 프로그램. 이전 버전과의 호환성에 대한 자세한 내용은 [이전 버전과의 호환성 및 표준 준수를](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 3.x 드라이버에 대한 블록 커서, 스크롤 가능한 커서 및 이전 버전과의 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) - 새로운 기능은 ODBC 3에 존재하는 기능입니다. *x와* ODBC 2에서 아닙니다. *x*. ODBC 3. *x* 드라이버는 일반적으로 ODBC 2 때문에 새로운 기능과의 이전 버전과의 호환성에 대해 걱정할 필요가 없습니다. *x* 응용 프로그램은 절대 로 사용되지 않습니다. 이에 대한 유일한 예외는 **SQLFetch,** **SQLFetch스크롤,** **SQLSetPos**및 **SQLExtendedFetch와**관련된 기능입니다. 자세한 내용은 이 부록의 다음 을 참조하십시오.  
  
-   [더 이상 사용되지 않는 기능 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) - 중복된 기능은 ODBC 3에서 다르게 구현되는 기능입니다. *x* 및 ODBC 2. *x*. ODBC 3. *x* 드라이버는 항상 ODBC 2를 매핑하기 때문에 중복 된 기능과의 이전 버전과의 호환성에 대해 걱정할 필요가 없습니다. *x* 기능은 ODBC 3에 있습니다. *x* 기능은 ODBC 3을 호출할 때 *x* 드라이버. 따라서, ODBC 3. *x* 드라이버는 ODBC 3만 볼 수 있습니다. *x* 기능. 이러한 매핑에 대한 자세한 내용은 이 부록의 다음 을 참조하십시오.  
  
-   [동작 변경 및 ODBC 3.x 드라이버](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) - 동작 변경은 ODBC 3에서 다르게 처리되는 기능입니다. *x* 및 ODBC 2. *x*. ODBC 3. *x* 드라이버는 동작 변경에 대해 걱정하고 응용 프로그램에서 설정한 SQL_ATTR_ODBC_VERSION 환경 특성에 대한 응답으로 행동해야 합니다.
