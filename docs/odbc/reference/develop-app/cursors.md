---
title: 커서 | Microsoft 문서
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
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 569714d6cd523498adddbda26576cf376af15c81
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910958"
---
# <a name="cursors"></a>커서
사용 하 여 데이터를 인출 하는 응용 프로그램을 *커서*합니다. 커서는 결과 집합에서 다른: 결과 집합은 특정 검색 조건과 일치 하는 행 집합, 응용 프로그램에는 행을 반환 하는 반면 커서는 소프트웨어입니다. 이름을 *커서* 데이터베이스에 적용 될 때 아마도 터미널 컴퓨터에 깜박이 커서가에서 시작 합니다. 해당 커서 화면과 형식화 된 단어가 표시 되는 위치 다음에 현재 위치에 표시 하는 대로만 결과 집합에서 커서에서 결과 집합은 다음 어떤 행이 반환 되 고 현재 위치를 나타냅니다.  
  
 Odbc에서 커서 모델에 포함 된 SQL 커서 모델을 기반으로 합니다. 이러한 모델 간의 한 가지 주목할 만한 차이점은 방식으로 커서를 열입니다. Embedded SQL에 커서를 명시적으로 선언 이며 전에 사용할 수 있습니다. Odbc에서 커서가 암시적으로 열려 있으면 결과 집합을 만드는 문을 실행 합니다. 커서를 열 때 결과 집합의 첫 번째 행 앞에 배치 됩니다. 에 포함 된 SQL 및 ODBC 둘 모두를 사용 하 여 응용 프로그램을 마친 후 커서를 닫아야 합니다.  
  
 다른 커서 다른 특징을가지고 있습니다. 가장 일반적인 유형의 라고 하는 커서를 한 *정방향 전용 커서* 결과 집합에서 앞으로 이동만 수 있습니다. 이전 행으로 돌아가려면 응용 프로그램 및 커서를 다시 열고를 열어야 다음 결과 필요한 행에 도달할 때까지 집합의 시작 부분에서 행을 읽습니다. 정방향 전용 커서는 결과 집합에 대 한 번 통과 하기 위한 빠른 메커니즘을 제공 합니다.  
  
 정방향 전용 커서도 덜 스크린 기반 응용 프로그램의 경우는 사용자가 스크롤할 뒤로 유용 하 고 데이터를 전달 합니다. 이러한 응용 프로그램 참조 결과 집합을 한 번만 데이터를 로컬로 캐싱 및 스크롤 자신을 수행 하 여 정방향 전용 커서를 사용할 수 있습니다. 그러나이 적은 양의 데이터와만 작동합니다. 더 나은 방법은 사용 하는 *스크롤 가능 커서* 결과 집합에 대 한 임의 액세스를 제공 하는 합니다. 이러한 응용 프로그램 성능을 강화할 수도 한 번에 둘 이상의 데이터 행을 인출 하 여이 이라고는 *커서를 차단 합니다.* 블록 커서에 대 한 자세한 내용은 참조 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md)합니다.  
  
 정방향 전용 커서는 ODBC의 기본 커서 유형을 이며 다음 섹션에서 설명 합니다. 블록 커서 및 스크롤 가능 커서에 대 한 자세한 내용은 참조 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md) 및 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다.  
  
> [!IMPORTANT]  
>  명시적으로 호출 하 여 트랜잭션을 커밋하거나 **SQLEndTran** 또는 자동 커밋 모드에서 작업할으로 설정 하면 일부 데이터 원본에 대 한 연결에 대 한 모든 문이 모든 커서를 닫습니다. 자세한 내용은에서 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 특성을 참조 하십시오.는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
