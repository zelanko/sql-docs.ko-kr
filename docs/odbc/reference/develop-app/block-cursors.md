---
title: "커서를 블록 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8d6b3eb0a520d4c5c83e043f57076d164503f6c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="block-cursors"></a>블록 커서
대부분의 응용 프로그램에 네트워크를 통해 데이터를 가져오는 하는 시간이 많이 소비 해야 합니다. 이 이번의 일부는 네트워크를 통해 데이터를 실제로 가져오는 데 걸리는 및 데이터의 행을 요청 하려면 드라이버에 의해 만들어진 호출과 같은 일부 라도 네트워크 오버 헤드를 소비 됩니다. 응용 프로그램이 효율적으로 사용 하는 경우 두 번째 시간을 줄일 수 있습니다 *블록* 또는 *fat* *커서,* 한 번에 둘 이상의 행을 반환할 수 있는 합니다.  
  
 항상 응용 프로그램에 블록 커서를 사용 하는 옵션이 있습니다. 한 번에 하나의 행을 가져올 수 있는 데이터 원본에서 드라이버에서 블록 커서를 시뮬레이션 해야 합니다. 여러 개의 단일 행 인출을 수행 하 여이 작업을 수행할 수 있습니다. 모든 성능 향상을 제공할 수 없을 때 응용 프로그램에 대 한 기회 열립니다. 이러한 응용 프로그램은 성능이 향상 될 환경의 다음 Dbms 블록 커서를 고유 하 게 구현 하 고 해당 Dbms와 관련 된 드라이버에 노출 합니다.  
  
 블록 커서와 함께 단일 인출에서 반환 되는 행 이라고는 *행 집합*합니다. 결과 집합으로 행 집합을 혼동 하지 않기 위해는 것이 유용 합니다. 결과 집합 행 집합은 응용 프로그램 버퍼에서 유지 관리 하는 동안 데이터 원본에서 유지 관리 됩니다. 결과 집합은 고정 되어 있는 동안입니다-위치를 변경 하 고 새 행 집합을 인출할 때마다 콘텐츠입니다. 현재 행을 기존의 SQL 정방향 전용 커서 지점과 같은 단일 행 커서와 마찬가지로 블록 커서 행 집합으로 생각할 수를 가리키는 *현재 행*합니다.  
  
 인출 된 행의 여러 하는 경우에 단일 행에 작동 하는 작업을 수행할 먼저 응용 프로그램이 어떤 행이 현재 행 나타내야 합니다. 현재 행에 대 한 호출에 필요한 **SQLGetData** 및 배치 update 및 delete 문입니다. 블록 커서 행 집합을 먼저 반환 되 면 현재 행이 행 집합의 첫 번째 행입니다. 현재 행을 호출 하 여 응용 프로그램을 변경 하려면 **SQLSetPos** 또는 **SQLBulkOperations** (책갈피에서 업데이트)에 있습니다. 다음은 결과 집합, 행 집합, 현재 행, 행 집합 커서 및 커서 블록의 관계입니다. 자세한 내용은 참조 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md)이 섹션의 뒷부분에 나오는 및 [배치 Update 및 Delete 문이](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) 및 [SQLSetPos 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)합니다.  
  
 ![다음으로, 이전, 첫 번째 및 마지막 행 집합을 인출](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 커서를 블록 커서를 인지 하는 것은 스크롤 가능 여부는 무관 합니다. 예를 들어 대부분의 작업에는 보고서 응용 프로그램에서 검색 하 고 행 인쇄 소비 됩니다. 이 인해 정방향 전용 빠른 작업, 블록 커서는 것입니다. 네트워크 트래픽을 줄이기 위해 블록 커서 및 스크롤 가능 커서를 비용을 방지 하기 위해 정방향 전용 커서를 사용 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [블록 커서와 함께 사용하기 위해 열 바인딩](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [행 상태 배열](../../../odbc/reference/develop-app/row-status-array.md)
