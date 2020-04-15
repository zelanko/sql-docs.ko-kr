---
title: 커서 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da899e4dc47daff03c31277b3edd4d9c642b87cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305294"
---
# <a name="cursors"></a>커서
응용 프로그램은 *커서를*사용하여 데이터를 가져옵니다. 커서는 결과 집합과 다릅니다: 결과 집합은 특정 검색 조건과 일치하는 행 집합인 반면 커서는 해당 행을 응용 프로그램에 반환하는 소프트웨어입니다. 데이터베이스에 적용되는 이름 *커서는* 컴퓨터 터미널의 깜박이는 커서에서 비롯된 것일 수 있습니다. 해당 커서가 화면의 현재 위치와 다음에 입력된 단어가 표시되는 위치를 나타내는 것처럼 결과 집합의 커서는 결과 집합의 현재 위치와 다음에 반환될 행을 나타냅니다.  
  
 ODBC의 커서 모델은 포함된 SQL의 커서 모델을 기반으로 합니다. 이러한 모델 간의 한 가지 주목할 만한 차이점은 커서를 여는 방식입니다. 포함된 SQL에서는 커서를 사용하려면 먼저 명시적으로 선언하고 열어야 합니다. ODBC에서 결과 집합을 만드는 문이 실행될 때 커서가 암시적으로 열립니다. 커서가 열리면 결과 집합의 첫 번째 행 앞에 배치됩니다. 임베디드 SQL 및 ODBC 모두에서 응용 프로그램 사용을 완료한 후 커서를 닫아야 합니다.  
  
 커서마다 특성이 다릅니다. *정방향 전용 커서라고* 하는 가장 일반적인 커서 유형은 결과 집합을 통해서만 앞으로 이동할 수 있습니다. 이전 행으로 돌아가려면 응용 프로그램이 커서를 닫고 다시 연 다음 필요한 행에 도달할 때까지 결과 집합의 시작 부분에서 행을 읽어야 합니다. 정방향 전용 커서는 결과 집합을 통과하는 단일 패스를 만들기 위한 빠른 메커니즘을 제공합니다.  
  
 순방향 전용 커서는 사용자가 데이터를 앞뒤로 스크롤하는 화면 기반 응용 프로그램에는 덜 유용합니다. 이러한 응용 프로그램은 결과 집합을 한 번 읽고, 데이터를 로컬로 캐싱하고, 스크롤을 수행하여 정방향 전용 커서를 사용할 수 있습니다. 그러나 이 작업은 소량의 데이터에서만 효과적입니다. 더 나은 해결책은 결과 집합에 대한 임의 액세스를 제공하는 *스크롤 가능한 커서를* 사용하는 것입니다. 또한 이러한 응용 프로그램은 *블록 커서라고* 하는 것을 사용하여 한 번에 두 개 이상의 데이터 행을 가져오면 성능이 향상될 수 있습니다. 블록 커서에 대한 자세한 내용은 [블록 커서 사용을](../../../odbc/reference/develop-app/using-block-cursors.md)참조하십시오.  
  
 정방향 전용 커서는 ODBC의 기본 커서 유형이며 다음 섹션에서 설명합니다. 블록 커서 및 스크롤 가능한 커서에 대한 자세한 내용은 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md) 및 [스크롤 가능한 커서를](../../../odbc/reference/develop-app/scrollable-cursors.md)참조하십시오.  
  
> [!IMPORTANT]  
>  **SQLEndTran을** 명시적으로 호출하거나 자동 커밋 모드에서 작동하여 트랜잭션을 커밋하거나 롤백하면 일부 데이터 원본이 연결의 모든 명령문의 모든 커서를 닫습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명에서 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 특성을 참조하십시오.
