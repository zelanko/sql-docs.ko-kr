---
title: 행집합 크기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 11b95768934f96e1587b3c570b2510f3c2849239
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304244"
---
# <a name="rowset-size"></a>행 집합 크기
사용할 행 집합 크기는 응용 프로그램에 따라 다릅니다. 화면 기반 응용 프로그램은 일반적으로 두 가지 전략 중 하나를 따릅니다. 첫 번째는 행 집합 크기를 화면에 표시되는 행 수로 설정하는 것입니다. 사용자가 화면 크기를 조정하면 응용 프로그램은 그에 따라 행 집합 크기를 변경합니다. 두 번째는 데이터 원본에 대한 호출 수를 줄이는 행 집합 크기를 100과 같은 더 큰 숫자로 설정하는 것입니다. 응용 프로그램은 가능하면 행 집합 내에서 로컬로 스크롤하고 행 집합 외부로 스크롤할 때만 새 행을 가져옵니다.  
  
 보고서와 같은 다른 응용 프로그램은 행 집합 크기를 응용 프로그램에서 합리적으로 처리할 수 있는 가장 많은 행으로 설정하는 경향이 있습니다. 행 집합의 크기를 정확히 따라달라질 수 있는 방법은 각 행의 크기와 사용 가능한 메모리 양에 따라 달라집니다.  
  
 행 집합 크기는 SQL_ATTR_ROW_ARRAY_SIZE *특성* 인수를 사용하여 **SQLSetStmtAttr에** 대한 호출로 설정됩니다. 응용 프로그램은 행을 가져온 후에도 행 집합 크기를 **변경하고, SQLBindCol을** 호출하거나 바인딩 오프셋을 지정하여 새 행 집합 버퍼를 바인딩할 수 있습니다. 행 집합 크기를 변경하는 데 따른 의미는 함수에 따라 다릅니다.  
  
-   **SQLFetch** 및 **SQLFetchScroll** 는 호출 시 행 집합 크기를 사용하여 가져올 행 수를 결정합니다. 그러나 *SQL_FETCH_NEXT FetchOrientation을* 가진 **SQLFetchScroll** 이전 가져오기의 행 집합을 기반으로 커서를 증분 한 다음 현재 행 집합 크기를 기반으로 행 집합을 가져옵니다.  
  
-   **SQLSetPos는 SQLSetPos가** 이미 설정된 행 집합에서 작동하기 때문에 **SQLFetch** **SQLSetPos** 또는 **SQLFetchScroll에**대한 이전 호출과 같이 적용되는 행 집합 크기를 사용합니다. **또한 SQLSetPos는** 행 집합 크기를 변경한 후 **SQLBulkOperations가** 호출된 경우 새 행 집합 크기를 선택합니다.  
  
-   **SQLBulkOperations는** 가져온 행 집합과 관계없이 테이블에서 작업을 수행하기 때문에 호출 시 적용되는 행 집합 크기를 사용합니다.
