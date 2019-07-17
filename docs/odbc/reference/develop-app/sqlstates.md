---
title: Sqlstate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8213c08e6844003d880129dda4b441a5592bbc86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107342"
---
# <a name="sqlstates"></a>SQLSTATE
Sqlstate는 경고 또는 오류의 원인에 대 한 자세한 정보를 제공합니다. 이 설명서에서 Sqlstate에 기반한 ISO/IEF CLI 사양에 있는 ODBC IM로 시작 하는 이러한 SQLSTATEs 관련이 있지만.  
  
 반환 코드에이 설명서에서 Sqlstate는 지침과 달리 드라이버 반환 하지 않아도 됩니다. 따라서 드라이버에서 오류 또는 경고가 감지의 수에 대 한 적절 한 SQLSTATE를 반환 해야 하는 동안 응용 프로그램에이 항상 계산 되지 해야 합니다. 이 이런 이유로 두 가지 면:  
  
-   **불완전성** 드라이버 구현 하기만 하면 큰 차이가;이 수동 많은 오류 및 경고 및 경고와 오류 원인이 나열 되지만 완전 하지 않습니다 하 고 수 하지 않을 수도 있습니다. 지정 된 드라이버 아마도 돌아가지 않습니다이 설명서에 나열 된 모든는 Sqlstate 및이 설명서에 나열 되지 않은 Sqlstate를 반환할 수 있습니다.  
  
-   **복잡성** 일부 데이터베이스 엔진-특히 관계형 데이터베이스 엔진-그대로 수천 개의 오류 및 경고를 반환 합니다. 이러한 엔진에 대 한 드라이버를 매핑할 모든 이러한 오류의 가능성이 없는 및 SQLSTATEs 경고 작업으로 인해 관련 매핑의 inexactness, 결과 코드의 큰 크기 및 종종 프로그래밍을 반환 하는 결과 코드를 낮은 값 런타임에 발생 하지 않아야 하는 오류입니다. 따라서 드라이버에 많은 오류 매핑해야 합니다. 및 경고는 것이 좋습니다와 이러한 오류 및 경고는 응용 프로그램 논리에 매핑해야 합니다 있습니다 수 기반, SQLSTATE 01004 (데이터 잘림) 같은 합니다.  
  
 SQLSTATEs 안정적으로 반환 되지 않습니다 때문에 대부분의 응용 프로그램만 표시할는 종종에 맞게 특정 오류 또는 경고가 발생 한, 해당 연결 된 진단 메시지와 함께 사용자와 원시 오류 코드입니다. 응용 프로그램 없습니다 기반 프로그래밍 논리 대부분의 Sqlstate 그래도 이므로 거의이 수행 하는 기능 손실이 됩니다. 예를 들어 **SQLExecDirect** SQLSTATE 42000 (구문 오류 또는 액세스 위반)를 반환 합니다. 이 오류를이 발생 시키는 SQL 문을 하드 코딩 되었거나 응용 프로그램으로 작성 된 경우이 프로그래밍 오류를 되며 코드를 수정 해야 합니다. 사용자가 SQL 문을 입력 하는 경우이 사용자 오류 이며 문제의 사용자에 게 알리는에서 사용할 수 있는 모든 응용 프로그램 종료 했습니다.  
  
 응용 프로그램 프로그래밍 논리 SQLSTATEs 기준 수행 하는 경우 이러한 준비 해야 SQLSTATE를 반환 하거나 반환할 다른 SQLSTATE입니다. 정확 하 게 SQLSTATEs 안정적으로 반환 되는 다양 한 드라이버를 사용 하 여 환경에만 기반 할 수 있습니다. 그러나는 일반 지침 드라이버 또는 데이터 원본 대신 드라이버 관리자에서 발생 하는 오류에 대 한 Sqlstate는 안정적으로 반환 될 가능성이입니다. 대부분의 드라이버 SQLSTATE HYC00 아마도 반환 되는 예를 들어, (선택적 기능이 구현 되지 않았습니다), 적은 드라이버에는 아마도 SQLSTATE 42021 반환 하는 동안 (열 이미 있음).  
  
 다음 SQLSTATEs에는 프로그래밍 논리를 기반으로 사용할 적합 한 후보가 및 런타임 오류 또는 경고를 나타냅니다. 그러나 모든 드라이버를 반환 하는 보장 되지 있습니다.  
  
-   01004 (데이터가 잘렸습니다.)  
  
-   01S02 (옵션 값이 변경 됨)  
  
-   HY008 (작업이 취소 됨)  
  
-   HYC00 (선택적 기능이 구현 되지 않음)  
  
-   HYT00 (제한 시간 만료 됨)  
  
 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)가 있는 응용 프로그램 드라이버가 특정 문 또는 연결 특성을 지원 하는지 여부를 확인할 수는 유일한 방법은 않으므로 특히 중요 합니다.  
  
 Sqlstate 및 돌려보낼 기능 목록은 참조 하세요. [부록 a: ODBC 오류 코드](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)합니다. 각 함수는 특정 SQLSTATE를 반환할 수 있습니다 조건의 자세한 내용은 해당 함수를 참조 하세요.
