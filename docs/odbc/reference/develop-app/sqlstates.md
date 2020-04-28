---
title: SQLSTATEs | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299730"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATEs는 경고나 오류의 원인에 대 한 자세한 정보를 제공 합니다. 이 설명서의 SQLSTATEs는 ISO/IEF CLI 사양에 있는 것을 기반으로 하며, IM으로 시작 하는 SQLSTATEs는 ODBC와 관련이 있습니다.  
  
 반환 코드와 달리이 설명서의 SQLSTATEs는 지침 이며 드라이버를 반환 하는 데 필요 하지 않습니다. 따라서 드라이버가 검색할 수 있는 오류 또는 경고에 대 한 적절 한 SQLSTATE를 반환 해야 하지만, 응용 프로그램은이 항상 발생 하는 경우를 계산 해서는 안 됩니다. 이러한 상황이 발생 하는 이유는 두 가지입니다.  
  
-   **Incompleteness** 이 수동은 많은 수의 오류와 경고를 나열 하 고 오류 및 경고에 대 한 가능한 원인을 나열 하지만이는 완료 되지 않으며 그렇지 않을 수도 있습니다. 드라이버 구현은 간단 하 게 변경 됩니다. 지정 된 모든 드라이버는이 설명서에 나열 된 SQLSTATEs를 모두 반환 하지 않으며이 설명서에 나열 되지 않은 SQLSTATEs를 반환할 수 있습니다.  
  
-   **복잡성** 일부 데이터베이스 엔진-특히 관계형 데이터베이스 엔진은 수천 개의 오류와 경고를 반환 합니다. 이러한 엔진의 드라이버는 관련 된 활동, 매핑의 inexactness, 결과 코드의 큰 크기 및 결과 코드의 낮은 값 때문에 이러한 모든 오류 및 경고를 SQLSTATEs에 매핑할 가능성이 높습니다 .이는 런타임에 발생 하지 않아야 하는 프로그래밍 오류를 반환 하기도 합니다. 따라서 드라이버는 오류 및 경고의 수를 적절 하 게 매핑하고, SQLSTATE 01004 (데이터 잘림)와 같이 응용 프로그램 논리의 기반으로 사용할 수 있는 오류 및 경고를 매핑해야 합니다.  
  
 SQLSTATEs는 안정적으로 반환 되지 않기 때문에 대부분의 응용 프로그램은 연결 된 진단 메시지와 함께 사용자에 게 표시 합니다 .이 메시지는 발생 한 특정 오류 또는 경고에 맞게 조정 되는 경우가 많으며 네이티브 오류 코드입니다. 응용 프로그램은 대부분의 SQLSTATEs에서 논리를 프로그래밍할 수 없기 때문에이 작업은 거의 손실 되지 않습니다. 예를 들어 **Sqlexecdirect** 에서 SQLSTATE 42000 (구문 오류 또는 액세스 위반)을 반환 한다고 가정 합니다. 이 오류를 발생 시킨 SQL 문이 하드 코드 되거나 응용 프로그램에 의해 빌드된 경우이는 프로그래밍 오류 이며 코드를 수정 해야 합니다. 사용자가 SQL 문을 입력 하는 경우 사용자 오류가 발생 하 고 응용 프로그램에서 문제를 사용자에 게 알려 서 가능한 모든 작업을 수행 합니다.  
  
 응용 프로그램에서 SQLSTATEs의 기본 프로그래밍 논리를 수행 하는 경우 SQLSTATE가 반환 되거나 다른 SQLSTATE가 반환 될 수 있도록 준비 해야 합니다. 안정적으로 반환 되는 SQLSTATEs는 다양 한 드라이버를 사용 하는 환경 에서만 사용할 수 있습니다. 그러나 일반적인 지침은 데이터 원본과는 달리 드라이버 또는 드라이버 관리자에서 발생 하는 오류에 대 한 SQLSTATEs가 안정적으로 반환 될 가능성이 높습니다. 예를 들어 대부분의 드라이버는 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)를 반환 하지만, 드라이버의 수는 SQLSTATE 42021 (열이 이미 있음)을 반환할 수 있습니다.  
  
 다음 SQLSTATEs는 런타임 오류 또는 경고를 나타내며 프로그래밍 논리를 기반으로 할 수 있는 좋은 후보입니다. 그러나 모든 드라이버가 반환 하는 것은 아닙니다.  
  
-   01004 (데이터 잘림)  
  
-   01 S 02 (옵션 값이 변경 됨)  
  
-   HY008 (작업 취소 됨)  
  
-   HYC00 (선택적 기능이 구현 되지 않음)  
  
-   HYT00 (제한 시간 만료)  
  
 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)는 응용 프로그램이 특정 문이나 연결 특성을 지원 하는지 여부를 응용 프로그램에서 확인할 수 있는 유일한 방법 이기 때문에 특히 중요 합니다.  
  
 SQLSTATEs의 전체 목록과이를 반환 하는 함수는 [부록 a: ODBC 오류 코드](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)를 참조 하세요. 각 함수가 특정 SQLSTATE를 반환할 수 있는 조건에 대 한 자세한 설명은 해당 함수를 참조 하세요.
