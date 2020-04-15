---
title: SQLSTATEs | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be4bca929b8d48c301c6e71917503387004a6ec5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299730"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATE는 경고 또는 오류의 원인에 대한 자세한 정보를 제공합니다. 이 설명서의 SQLSTATE는 IM으로 시작하는 SQLSTATE가 ODBC에만 해당되지만 ISO/IEF CLI 사양에 있는 SQLSTAT를 기반으로 합니다.  
  
 반환 코드와 달리 이 설명서의 SQLSTAT는 지침이며 드라이버는 반환할 필요가 없습니다. 따라서 드라이버는 감지할 수 있는 오류 나 경고에 대해 적절한 SQLSTATE를 반환해야 하지만 응용 프로그램은 항상 발생하는 이 문제에 의존해서는 안 됩니다. 이 상황의 이유는 두 가지입니다.  
  
-   **불완전성** 이 매뉴얼에는 많은 수의 오류와 경고및 이러한 오류 및 경고의 가능한 원인이 나열되어 있지만 완전하지는 않으며 앞으로도 그러하지 않을 것입니다. 드라이버 구현은 단순히 너무 많이 다릅니다. 지정된 드라이버는 이 설명서에 나열된 모든 SQLSTAT를 반환하지 않으며 이 설명서에 나열되지 않은 SQLSTATEs를 반환할 수 있습니다.  
  
-   **복잡성** 일부 데이터베이스 엔진(특히 관계형 데이터베이스 엔진)은 문자 그대로 수천 개의 오류와 경고를 반환합니다. 이러한 엔진의 드라이버는 관련된 노력, 매핑의 부정확성, 결과 코드의 큰 크기 및 결과 코드의 낮은 값으로 인해 이러한 오류및 경고를 모두 SQLSTATE에 매핑할 가능성이 낮으며, 이는 종종 런타임에 발생하지 않아야 하는 프로그래밍 오류를 반환합니다. 따라서 드라이버는 합리적인 것으로 보이는 만큼 많은 오류와 경고를 매핑해야 하며 SQLSTATE 01004(데이터 잘린 데이터)와 같이 응용 프로그램 논리의 기반이 될 수 있는 응용 프로그램 논리에 대한 오류 및 경고를 매핑해야 합니다.  
  
 SQLSTATEs는 안정적으로 반환되지 않으므로 대부분의 응용 프로그램은 발생한 특정 오류 또는 경고 및 기본 오류 코드에 맞게 조정되는 관련 진단 메시지와 함께 사용자에게 표시하기만 하면 됩니다. 응용 프로그램이 대부분의 SQLSTATEs에 프로그래밍 논리를 기반으로 할 수 없기 때문에 이 작업을 수행하는 데 기능이 손실되는 경우는 거의 없습니다. 예를 들어 **SQLExecDirect가** SQLSTATE 42000(구문 오류 또는 액세스 위반)을 반환한다고 가정합니다. 이 오류를 발생 시킨 SQL 문이 응용 프로그램에 의해 하드 코딩 되거나 빌드 하는 경우이 프로그래밍 오류 이며 코드를 수정 해야 합니다. 사용자가 SQL 문을 입력하는 경우 이 오류는 사용자 오류이며 응용 프로그램은 사용자에게 문제를 알려줌으로써 가능한 모든 작업을 수행했습니다.  
  
 응용 프로그램이 SQLSTATEs에서 기본 프로그래밍 논리를 수행하는 경우 SQLSTATE가 반환되지 않거나 다른 SQLSTATE가 반환되지 않도록 준비해야 합니다. 안정적으로 반환되는 SQLSTATEs는 수많은 드라이버의 경험만을 기반으로 할 수 있습니다. 그러나 일반적인 지침은 데이터 원본과 달리 드라이버 또는 드라이버 관리자에서 발생하는 오류에 대한 SQLSTATEs가 안정적으로 반환될 가능성이 높다는 것입니다. 예를 들어 대부분의 드라이버는 SQLSTATE HYC00(선택적 기능이 구현되지 않음)을 반환하는 반면, 적은 수의 드라이버가 SQLSTATE 42021(열이 이미 있음)을 반환할 수 있습니다.  
  
 다음 SQLSTATEs는 런타임 오류 또는 경고를 나타내며 프로그래밍 논리를 기반으로 하는 좋은 후보입니다. 그러나 모든 드라이버가 반환한다는 보장은 없습니다.  
  
-   01004(데이터 잘린)  
  
-   01S02(옵션 값이 변경)  
  
-   HY008(작동 이 취소)  
  
-   HYC00(옵션 기능이 구현되지 않음)  
  
-   HYT00(시간 시간 변경)  
  
 SQLSTATE HYC00(구현되지 않은 선택적 기능)은 응용 프로그램이 드라이버가 특정 명령문 또는 연결 특성을 지원하는지 여부를 결정할 수 있는 유일한 방법이기 때문에 특히 중요합니다.  
  
 SQLSTATEs의 전체 목록과 이를 반환하는 함수는 [부록 A: ODBC 오류 코드를](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)참조하십시오. 각 함수가 특정 SQLSTATE를 반환할 수 있는 조건에 대한 자세한 설명은 해당 함수를 참조하십시오.
