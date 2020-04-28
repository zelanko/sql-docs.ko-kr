---
title: 블록 커서 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa35888ef93da9648fe6422bdc35ebf9da3a0525
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306354"
---
# <a name="block-cursors"></a>블록 커서
많은 응용 프로그램에서 네트워크를 통해 데이터를 가져오는 데 상당한 시간이 소요 됩니다. 이 시간의 일부는 네트워크를 통해 실제로 데이터를 가져오는 데 소비 되 고 일부는 네트워크 오버 헤드 (예: 드라이버에서 데이터 행을 요청 하기 위해 수행 하는 호출)에 소요 됩니다. 응용 프로그램에서 *블록* 또는 *fat* *커서를* 효율적으로 사용 하 여 한 번에 두 개 이상의 행을 반환할 수 있는 경우에는 후자의 시간이 줄어들 수 있습니다.  
  
 응용 프로그램에는 항상 블록 커서를 사용할 수 있는 옵션이 있습니다. 한 번에 한 행만 인출할 수 있는 데이터 원본에서는 블록 커서를 드라이버에서 시뮬레이션 해야 합니다. 이 작업은 여러 단일 행 페치를 수행 하 여 수행할 수 있습니다. 이렇게 하면 성능이 향상 되는 것은 아니지만 응용 프로그램에 대 한 기회가 열립니다. 그러면 Dbms에서 블록 커서를 기본적으로 구현 하 고 해당 Dbms와 연결 된 드라이버가 노출 하므로 이러한 응용 프로그램의 성능이 향상 됩니다.  
  
 블록 커서를 사용 하 여 단일 인출에서 반환 되는 행을 *행 집합*이라고 합니다. 행 집합을 결과 집합과 혼동 하지 않는 것이 중요 합니다. 결과 집합은 데이터 원본에서 유지 관리 되는 반면 행 집합은 응용 프로그램 버퍼에서 유지 관리 됩니다. 결과 집합은 고정 되어 있지만 행 집합은 새 행 집합이 인출 될 때마다 위치 및 내용을 변경 하지 않습니다. 기존 SQL 전방 전용 커서와 같이 현재 행을 가리키는 단일 행 커서와 마찬가지로 블록 커서는 행 집합을 가리키며 *현재 행*으로 간주할 수 있습니다.  
  
 여러 행을 반입할 때 단일 행에 대해 작동 하는 작업을 수행 하려면 응용 프로그램에서 먼저 현재 행이 있는 행을 표시 해야 합니다. 현재 행은 **SQLGetData** 및 위치 지정 update 및 delete 문을 호출 하는 데 필요 합니다. 블록 커서가 첫 번째 행 집합을 반환 하는 경우 현재 행은 행 집합의 첫 번째 행입니다. 현재 행을 변경 하기 위해 응용 프로그램은 **SQLSetPos** 또는 **SQLBulkOperations** 를 호출 합니다 (책갈피로 업데이트). 다음 그림에서는 결과 집합, 행 집합, 현재 행, 행 집합 커서 및 블록 커서의 관계를 보여 줍니다. 자세한 내용은이 섹션의 뒷부분에 있는 [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md)및 [Update 및 Delete 문 위치](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) 지정 및 [SQLSetPos를 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)를 참조 하세요.  
  
 ![다음, 이전, 첫 번째 및 마지막 행 집합 페치](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 커서가 블록 커서 인지 여부는 스크롤할 수 있는지 여부와 무관 합니다. 예를 들어 보고서 응용 프로그램에서 대부분의 작업은 행을 검색 하 고 인쇄 하는 데 사용 됩니다. 따라서 앞 으로만 이동 가능한 블록 커서를 사용 하 여 가장 빠르게 작동 합니다. 앞 으로만 이동 가능한 커서를 사용 하지 않고, 블록 커서를 사용 하 여 네트워크 트래픽을 줄일 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [블록 커서와 함께 사용하기 위해 열 바인딩](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [행 상태 배열](../../../odbc/reference/develop-app/row-status-array.md)
