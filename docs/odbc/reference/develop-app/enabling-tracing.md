---
title: 추적 활성화 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80bd4023a0260b67d11d7b4ded1bb810b81e0ab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287353"
---
# <a name="enabling-tracing"></a>추적 사용
추적은 다음 세 가지 방법으로 사용할 수 있습니다.  
  
-   Odbc.ini 레지스트리 항목에서 **추적** 및 **추적 파일** 키워드를 설정합니다. 이렇게 하면 *핸들 유형SQL_HANDLE_ENV* 호출된 **SQLAllocHandle을** 사용할 때 추적을 활성화하거나 사용하지 않도록 설정합니다. 이러한 옵션은 데이터 원본 설정 중에 표시되는 ODBC 데이터 원본 관리자 대화 상자의 추적 탭에 설정됩니다. 자세한 내용은 [데이터 원본에 대한 레지스트리 항목을](../../../odbc/reference/install/registry-entries-for-data-sources.md)참조하십시오.  
  
-   **SQLSetConnectAttr를** 호출하여 SQL_ATTR_TRACE 연결 특성을 SQL_OPT_TRACE_ON 설정합니다. 이렇게 하면 연결 기간 동안 추적을 활성화하거나 사용하지 않도록 설정합니다. 자세한 내용은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 함수 설명을 참조하십시오.  
  
-   **ODBCSharedTraceFlag를** 사용하여 추적을 동적으로 켜거나 끕니다. 자세한 내용은 다음 항목인 [동적 추적을](../../../odbc/reference/develop-app/dynamic-tracing.md)참조하십시오.
