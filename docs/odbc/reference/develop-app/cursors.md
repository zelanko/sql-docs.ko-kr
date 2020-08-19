---
description: 커서 (ODBC)
title: 커서 (ODBC) | Microsoft Docs
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
ms.openlocfilehash: 10dbd2517c29bcd02d1d39abe0b2caec1bf03312
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429405"
---
# <a name="odbc-cursors"></a>ODBC 커서
응용 프로그램은 *커서*를 사용 하 여 데이터를 인출 합니다. 커서는 결과 집합과 다릅니다. 결과 집합은 특정 검색 조건과 일치 하는 행 집합 이지만 커서는 응용 프로그램에 해당 행을 반환 하는 소프트웨어입니다. 데이터베이스에 적용 되는 이름 *커서* 는 컴퓨터 터미널의 깜박이는 커서에서 발생 했을 수 있습니다. 커서가 화면에서 현재 위치를 나타내고 입력 된 단어가 다음에 표시 되는 것 처럼 결과 집합의 커서는 결과 집합의 현재 위치 및 다음에 반환 되는 행을 나타냅니다.  
  
 ODBC의 커서 모델은 포함 된 SQL의 커서 모델을 기반으로 합니다. 이러한 모델 간의 주요 차이점 중 하나는 커서가 열리는 방식입니다. 포함 된 SQL에서 사용 하려면 먼저 커서를 명시적으로 선언 하 고 열어야 합니다. ODBC에서는 결과 집합을 만드는 문이 실행 될 때 커서가 암시적으로 열립니다. 커서를 열 때 커서는 결과 집합의 첫 번째 행 앞에 배치 됩니다. 포함 된 SQL과 ODBC 모두에서 응용 프로그램 사용을 마친 후 커서를 닫아야 합니다.  
  
 다른 커서는 서로 다른 특성을 갖습니다. *앞 으로만* 이동 가능한 커서 라고 하는 가장 일반적인 유형의 커서는 결과 집합을 통해서만 앞으로 이동할 수 있습니다. 이전 행으로 돌아가려면 응용 프로그램은 커서를 닫았다가 다시 연 다음, 필요한 행에 도달할 때까지 결과 집합의 시작 부분에서 행을 읽어야 합니다. 앞 으로만 이동 가능한 커서는 결과 집합을 통해 단일 패스를 만드는 빠른 메커니즘을 제공 합니다.  
  
 앞 으로만 이동 가능한 커서는 사용자가 앞뒤로 데이터를 스크롤하고 화면 기반 응용 프로그램에는 유용 하지 않습니다. 이러한 응용 프로그램은 결과 집합을 한 번 읽고, 로컬로 데이터를 캐시 하 고, 자체적으로 스크롤 하 여 앞 으로만 이동 가능한 커서를 사용할 수 있습니다. 그러나 적은 양의 데이터를 사용 하는 경우에만 제대로 작동 합니다. 더 나은 솔루션은 결과 집합에 대 한 임의 액세스를 제공 하는 *스크롤 가능한 커서* 를 사용 하는 것입니다. 이러한 응용 프로그램은 *블록 커서* 라고 하는 항목을 사용 하 여 한 번에 두 개 이상의 데이터 행을 인출 하 여 성능을 향상 시킬 수도 있습니다. 블록 커서에 대 한 자세한 내용은 [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md)을 참조 하세요.  
  
 앞 으로만 이동 가능한 커서는 ODBC의 기본 커서 유형이 며 다음 섹션에서 설명 합니다. 블록 커서 및 스크롤 가능 커서에 대 한 자세한 내용은 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md) 및 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)를 참조 하세요.  
  
> [!IMPORTANT]  
>  **Sqlendtran** 을 명시적으로 호출 하거나 자동 커밋 모드에서 작동 하 여 트랜잭션을 커밋하거나 롤백하는 경우 일부 데이터 원본에서 연결의 모든 문에 있는 모든 커서를 닫습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명의 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 특성을 참조 하세요.
