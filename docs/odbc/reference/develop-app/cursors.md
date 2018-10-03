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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91765f0572d8c880f7505948f7756b373fe28f62
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656081"
---
# <a name="cursors"></a>커서
사용 하 여 데이터를 인출 하는 응용 프로그램을 *커서*합니다. 커서가 결과 집합에서 다른: 결과 집합은 특정 검색 조건과 일치 하는 행 집합, 응용 프로그램에 이러한 행을 반환 하는 반면 커서는 소프트웨어입니다. 이름을 *커서* 데이터베이스에 적용 될 때 아마도 터미널 컴퓨터 깜박이 커서에서 발생 합니다. 해당 커서 입력된 되는 단어 다음 표시는 화면에 현재 위치를 나타내는, 처럼 커서 결과 집합에서 어떤 행이 다음 반환 결과 집합의 현재 위치를 나타냅니다.  
  
 ODBC의 커서 모델에 포함 된 SQL 커서 모델을 기반으로 합니다. 이러한 모델 간의 주요 차이점 중 하나는 방식으로 커서를 열 경우 Embedded SQL에서 커서 해야 명시적으로 선언 하 고 열린 후 사용할 수 있습니다. ODBC 커서 결과 집합을 만드는 문을 실행할 때 암시적으로 열렸습니다. 커서를 열 때 결과 집합의 첫 번째 행 앞에 배치 됩니다. 모두 포함 된 SQL 및 ODBC의 경우에서 응용 프로그램을 사용 하 여 완료 되 면 커서를 닫아야 합니다.  
  
 다른 커서에 다른 특징이 있습니다. 라고 하는 커서의 가장 일반적인 형식을 *정방향 전용 커서* 결과 집합에서 앞으로 이동만 있습니다. 이전 행으로 돌아가려면 응용 프로그램 및 커서를 닫은 후 다시 열어야 다음 결과 집합을 필요한 행에 도달할 때까지 시작 부분에서 행을 읽습니다. 정방향 전용 커서 결과 집합을 통해 단일 패스를 만들기 위한 빠른 메커니즘을 제공 합니다.  
  
 정방향 전용 커서는 작은 화면 기반 응용 프로그램의 경우는 사용자가 스크롤할 뒤로 유용 하 고 데이터를 통해 전달 됩니다. 이러한 응용 프로그램 데이터를 로컬로 캐시 하 고 자체 스크롤 수행 후 설정 결과 읽도록 정방향 전용 커서를 사용할 수 있습니다. 그러나이 적은 양의 데이터에만 제대로 작동합니다. 더 나은 방법은 사용 하는 *스크롤 가능 커서* 결과 집합에 대 한 임의 액세스를 제공 하는 합니다. 이러한 응용 프로그램 성능을 강화할 수도에서 한 번에 둘 이상의 데이터 행을 인출 이라고는 *커서를 차단 합니다.* 블록 커서에 대 한 자세한 내용은 참조 하세요. [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md)입니다.  
  
 정방향 전용 커서는 ODBC의 기본 커서 유형 및는 다음 섹션에서 설명 합니다. 블록 커서 및 스크롤 가능 커서에 대 한 자세한 내용은 참조 하십시오 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md) 하 고 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다.  
  
> [!IMPORTANT]  
>  커밋 또는 명시적으로 호출 하 여 트랜잭션을 롤백하면 **SQLEndTran** 또는 자동 커밋 모드에서 운영 하 여로 설정 하면 일부 데이터 소스를 연결에서 모든 문에서 모든 커서를 닫습니다. 자세한 내용은 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 특성을 참조 하세요. 합니다 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
