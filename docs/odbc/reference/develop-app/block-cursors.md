---
title: 블록 커서 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306354"
---
# <a name="block-cursors"></a>블록 커서
많은 응용 프로그램은 네트워크를 통해 데이터를 가져오는 데 상당한 시간을 소비합니다. 이 시간의 일부는 실제로 네트워크를 통해 데이터를 가져오는 데 사용되며, 그 중 일부는 드라이버가 데이터 행을 요청하는 호출과 같은 네트워크 오버헤드에 사용됩니다. 응용 프로그램이 한 번에 두 개 이상의 행을 반환 할 수있는 *블록 또는* 지방 *커서를* 효율적으로 사용하는 경우 후자의 시간을 줄일 수 있습니다. *fat,*  
  
 응용 프로그램에는 항상 블록 커서를 사용할 수 있는 옵션이 있습니다. 한 번에 하나의 행만 가져올 수 있는 데이터 원본에서 블록 커서는 드라이버에서 시뮬레이션해야 합니다. 이 작업은 여러 단일 행 가져오기를 수행하여 수행할 수 있습니다. 성능 향상을 제공할 가능성은 낮지만 응용 프로그램에 대한 기회가 열립니다. 그러면 DBMS가 기본적으로 블록 커서를 구현하고 해당 DBMS와 연결된 드라이버가 이를 노출함에 따라 이러한 응용 프로그램이 성능이 향상됩니다.  
  
 블록 커서가 있는 단일 가져오기에서 반환된 행을 *rowset이라고*합니다. 행 집합을 결과 집합과 혼동하지 않는 것이 중요합니다. 결과 집합은 데이터 원본에서 유지되고 행 집합은 응용 프로그램 버퍼에서 유지됩니다. 결과 집합이 고정되어 있지만 행 집합은 고정되지 않습니다. 기존 SQL 정방향 전용 커서와 같은 단일 행 커서가 현재 행을 가리키는 것처럼 블록 커서는 *현재 행으로*생각할 수 있는 행 집합을 가리킵니다.  
  
 여러 행을 가져온 경우 단일 행에서 작동하는 작업을 수행하려면 응용 프로그램이 먼저 현재 행인 행을 표시해야 합니다. 현재 행은 **SQLGetData** 및 위치 업데이트 및 삭제 문을 호출하여 필요합니다. 블록 커서가 먼저 행 집합을 반환하면 현재 행이 행 집합의 첫 번째 행입니다. 현재 행을 변경하려면 응용 프로그램에서 **SQLSetPos** 또는 **SQLBulkOperations를** 호출합니다(책갈피별로 업데이트). 다음 그림에서는 결과 집합, 행 집합, 현재 행, 행 집합 커서 및 블록 커서의 관계를 보여 주며 있습니다. 자세한 내용은 이 섹션의 뒷부분에서 [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md)및 [SQLSetPos를 사용하여](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)문 및 업데이트 문을 [배치하고](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) 데이터를 업데이트하는 것을 참조하십시오.  
  
 ![다음, 이전, 첫 번째 및 마지막 행 집합 페치](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 커서가 블록 커서인지 여부는 스크롤 가능 여부와 독립적입니다. 예를 들어 보고서 응용 프로그램의 대부분의 작업은 행을 검색하고 인쇄하는 데 사용됩니다. 이 때문에 정방향 전용 블록 커서를 사용하면 가장 빠르게 작동합니다. 스크롤 가능한 커서의 비용을 피하기 위해 정방향 전용 커서와 네트워크 트래픽을 줄이기 위한 블록 커서를 사용합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [블록 커서와 함께 사용하기 위해 열 바인딩](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [행 상태 배열](../../../odbc/reference/develop-app/row-status-array.md)
