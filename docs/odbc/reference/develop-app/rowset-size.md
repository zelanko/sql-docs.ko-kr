---
title: 행 집합 크기가 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fda38811fa876c9a0fad55e7f2ee7566ad3026d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943769"
---
# <a name="rowset-size"></a>행 집합 크기
응용 프로그램에서 사용 하는 행 집합 크기에 따라 달라 집니다. 일반적으로 화면 기반 응용 프로그램 두 가지 전략 중 하나를 수행 합니다. 첫 번째는 화면에 표시 되는 행 수의 행 집합 크기를 설정 하려면 사용자의 화면 크기를 조정, 응용 프로그램 그에 따라 행 집합 크기를 변경 합니다. 두 번째 큰 숫자로 100 같은 데이터 원본에 대 한 호출의 수를 줄일 행 집합 크기를 설정 하는 것입니다. 응용 프로그램 로컬 가능한 경우 행 집합 내의 스크롤하고 외부 행 집합으로 스크롤될 때에 새 행을 인출 합니다.  
  
 응용 프로그램 합리적으로 처리할 수 있습니다-행의 최대 수는 행 집합 크기를 설정 하는 경향이 보고서와 같은 다른 응용 프로그램을 더 큰 행 집합을 사용 하 여 행 마다 오버 헤드 네트워크 경우에 따라 줄어듭니다. 정확 하 게 얼마나 큰 행 집합 수는 사용 가능한 메모리의 양과 각 행의 크기에 따라 달라 집니다.  
  
 호출 하 여 행 집합 크기 설정 되어 **SQLSetStmtAttr** 사용 하 여는 *특성* SQL_ATTR_ROW_ARRAY_SIZE의 인수입니다. 응용 프로그램 행 집합 크기를 변경, 새 행 집합 버퍼를 바인딩할 수 있습니다 (호출한 **SQLBindCol** 바인딩 오프셋을 지정 하거나) 인출 된 행을 한 후에 또는 둘 다. 행 집합 크기를 변경의 의미는 함수에 따라 달라 집니다.  
  
-   **SQLFetch** 하 고 **SQLFetchScroll** 호출 시 행 집합 크기를 사용 하 여 인출할 행 수를 결정 합니다. 그러나 **SQLFetchScroll** 사용 하 여를 *FetchOrientation* SQL_FETCH_NEXT 증분 커서 기반 이전 인출 및 다음 인출의 행 집합에서 현재 행 집합 크기를 기준으로 행 집합입니다.  
  
-   **SQLSetPos** 에 대 한 이전 호출을 기준으로 적용 되는 행 집합 크기를 사용 하 여 **SQLFetch** 하거나 **SQLFetchScroll**이므로 **SQLSetPos** 행 집합에서 작동 이미 설정 되었습니다. **SQLSetPos** 도 새 행 집합 크기가 경우 선택할 **SQLBulkOperations** 가 행 집합 크기가 변경 된 후 호출 되었습니다.  
  
-   **SQLBulkOperations** 인출된 된 행 집합의 독립적인 테이블에 대 한 작업을 수행 하므로 호출 시 적용 행 집합 크기를 사용 합니다.
