---
title: 커서를 차단 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e0ea6ff655140c979f400f67a59cd7259bac9e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118815"
---
# <a name="block-cursors"></a>블록 커서
대부분의 응용 프로그램 네트워크를 통해 데이터를 가져오는 시간을 투입 합니다. 이 시간 부분 실제로 네트워크를 통해 데이터를 가져오는 데 소요 된 하 고 데이터 행을 요청 하려면 드라이버에 의해 수행 된 호출 등의 일부 네트워크 오버 헤드를 소비 됩니다. 응용 프로그램은 효율적으로 사용 하는 경우 두 번째 시간을 줄일 수 있습니다 *블록* 하거나 *fat* *커서* 한 번에 둘 이상의 행을 반환할 수 있는 합니다.  
  
 항상 응용 프로그램에는 블록 커서를 사용 하는 옵션이 있습니다. 한 번에 하나의 행을 가져올 수 있는 데이터 원본에서 드라이버의 블록 커서를 시뮬레이션할 수 있어야 합니다. 이 여러 단일 행 페치를 수행 하 여 수행할 수 있습니다. 모든 성능 향상을 제공할 수 없을 때 응용 프로그램에 대 한 기회가 열립니다. 이러한 응용 프로그램 성능이 향상 될 발생 후 Dbms 블록 커서를 고유 하 게 구현 하 고 해당 Dbms와 연결 된 드라이버를 노출 합니다.  
  
 블록 커서를 사용 하 여 단일 인출에서 반환 되는 행 이라고 합니다 *행 집합*합니다. 결과 집합을 사용 하 여 행 집합을 혼동 하지 않기 위해는 것이 반드시 합니다. 결과 집합은 행 집합은 응용 프로그램 버퍼에서 유지 관리 하는 동안 데이터 원본에 유지 됩니다. 결과 집합을 고정 하는 동안 행 집합에는 없는-위치를 변경 하 고 새 행 집합은 인출 될 때마다 콘텐츠입니다. 현재 행을 기존의 SQL 정방향 전용 커서 지점과 같은 단일 행 커서 처럼 블록 커서를 가리키는 행 집합으로 생각할 수 있습니다 *현재 행*합니다.  
  
 인출 된 행의 여러 하는 경우에 단일 행에 대해 작동 하는 작업을 수행할 먼저 응용 프로그램 행이 현재 행 나타내야 합니다. 현재 행에 대 한 호출에 필요한 **SQLGetData** 배치 업데이트 및 delete 문입니다. 블록 커서 행 집합을 먼저 반환 될 때 현재 행이 행 집합의 첫 번째 행. 응용 프로그램 호출 하 여 현재 행을 변경 하려면 **SQLSetPos** 하거나 **SQLBulkOperations** (책갈피로 업데이트)을 합니다. 다음 그림에서는 결과 집합, 행 집합, 현재 행, 행 집합 커서 및 커서 블록의 관계를 보여 줍니다. 자세한 내용은 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md)이 섹션의 뒷부분에 나오는 및 [배치 업데이트 및 삭제 문을](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) 하 고 [SQLSetPos 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![이전, 첫 번째 및 마지막 행 다음에 가져오는](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 커서를 블록 커서를 인지 하는 것은 스크롤 가능 여부는 관계가 없습니다. 예를 들어 보고서 응용 프로그램에서 작업의 대부분을 검색 하 고 행 인쇄 소요 됩니다. 이 인해 빠른 정방향 전용을 사용 하 여 작업, 블록 커서는 것입니다. 정방향 전용 커서는 스크롤 가능 커서 및 네트워크 트래픽을 줄이기 위해 블록 커서 비용을 방지 하려면 사용 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [블록 커서와 함께 사용하기 위해 열 바인딩](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [행 상태 배열](../../../odbc/reference/develop-app/row-status-array.md)
