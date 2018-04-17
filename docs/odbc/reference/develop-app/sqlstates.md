---
title: Sqlstate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92e36a33efeade353f77f476bfc9ef12ce53608b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlstates"></a>SQLSTATE
Sqlstate는 경고 또는 오류의 원인에 대 한 자세한 정보를 제공합니다. 이 설명서에서 Sqlstate 기반으로 ISO/IEF CLI 사양에서 ODBC IM로 시작 하는 이러한 SQLSTATEs 관련이 있지만 합니다.  
  
 반환 코드와 달리이 설명서에서 Sqlstate 지침, 되며 드라이버 이들을 반환할 필요가 없습니다. 따라서 드라이버는 모든 오류 또는 경고를 검색할 수 있는지에 대 한 적절 한 SQLSTATE 반환할지 여부를 하는 동안 응용 프로그램은 항상 발생에 계산 되지 않습니다. 이 경우는 이유는 다음과 같이 두 가지:  
  
-   **불완전성** 드라이버를 사용 해도 단순히 너무 많이 변경;이 설명서에는 많은 수의 오류 및 경고 및 이러한 오류 및 경고에 대 한 가능한 원인을 나열, 되더라도 것 완전 하지 않으며 하지 않이 됩니다. 지정된 된 드라이버 아마도 반환 하지 않습니다이 설명서에 나열 된 모든는 Sqlstate 및이 설명서에 나열 되지 않은 Sqlstate를 반환할 수 있습니다.  
  
-   **복잡성** 일부 데이터베이스 엔진-특히 관계형 데이터베이스 엔진-오류 및 경고 수천 문자 그대로 반환 합니다. 이러한 엔진에 대 한 드라이버 이러한 오류에 매핑할 될 있으며 약간의 노력으로 인해 경고 Sqlstate 관련 매핑의 inexactness, 결과 코드의 크기를 큰 및 프로그래밍에 자주 돌아가는 결과 코드의 낮은 값 런타임 시 발생 하지 해야 하는 오류입니다. 따라서 드라이버 만큼 오류 매핑해야 합니다. 및 경고 합리적으로 보입니다 하 고 이러한 오류 및 경고는 응용 프로그램 논리에 매핑합니다 기준이 될 수 있습니다, SQLSTATE 01004 (데이터 잘림) 등.  
  
 SQLSTATEs 안정적으로 반환 되지 않습니다 때문에 대부분의 응용 프로그램 표시에 종종 맞게 특정 오류 또는 경고가 발생 한, 해당 연결된 진단 메시지와 함께 사용자와 원시 오류 코드에 합니다. 응용 프로그램 없습니다 기반 프로그래밍 논리를 대부분 SQLSTATEs 그래도 때문에이 작업을 수행 하는 기능은 거의 모든 손실이 있습니다. 예를 들어 **SQLExecDirect** SQLSTATE 42000 (구문 오류 또는 액세스 위반)를 반환 합니다. 이 오류를 발생 시킨 SQL 문을 하드 코드 된 또는 응용 프로그램에서 작성 된 경우 프로그래밍 오류 및 코드를 수정 해야 합니다. 사용자가 SQL 문을 입력 된 사용자 오류 및 문제의 사용자에 게 알리는 하 여 모든 응용 프로그램 종료 했습니다.  
  
 응용 프로그램 프로그래밍 논리 SQLSTATEs 기준 수행 하는 경우 이러한 준비 해야 SQLSTATE를 반환 하거나 반환 될 다른 SQLSTATE입니다. 정확 하 게 SQLSTATEs 안정적으로 반환 되는 다양 한 드라이버와 함께 경험에 대해서만 따라 만들어집니다. 그러나 일반적인 지침에는 드라이버 또는 드라이버 관리자를 달리 데이터 소스에서 발생 하는 오류에 대 한 Sqlstate는 안정적으로 반환 될 가능성이 높습니다. 대부분의 드라이버 SQLSTATE HYC00 아마도 반환 되는 예를 들어 (선택적 기능이 구현 되지 않았습니다), 더 적은 드라이버 아마도 반환 하 고 SQLSTATE 42021 반면 (열 이미 있음).  
  
 다음 SQLSTATEs에는 프로그래밍 논리를 기반으로 사용할 적합 한 후보가 및 런타임 오류 또는 경고를 나타냅니다. 그러나 모든 드라이버를 반환 하지 않을 수도가 있습니다.  
  
-   01004 (데이터가 잘렸습니다.)  
  
-   01 s 02 (옵션 값이 변경 됨)  
  
-   HY008 (작업이 취소 됨)  
  
-   HYC00 (선택적 기능이 구현 되지 않았습니다)  
  
-   HYT00 (제한 시간 만료 됨)  
  
 SQLSTATE HYC00 (선택적 기능이 구현 되지 않았습니다)는 유일한 방법은는 응용 프로그램 드라이버가 특정 문 또는 연결 특성을 지원 하는지 여부를 확인할 수 있기 때문에 특히 중요 합니다.  
  
 Sqlstate 및 함수 반환의 전체 목록은 참조 하십시오. [부록 a: ODBC 오류 코드](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)합니다. 각 함수는 특정 SQLSTATE를 반환할 수 있습니다 조건, 대 한 자세한 내용은 해당 함수를 참조 하세요.
