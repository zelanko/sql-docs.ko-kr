---
title: 행 집합 크기 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67943769"
---
# <a name="rowset-size"></a>행 집합 크기
사용할 행 집합 크기는 응용 프로그램에 따라 달라 집니다. 화면 기반 응용 프로그램은 일반적으로 두 가지 전략 중 하나를 따릅니다. 첫 번째는 행 집합 크기를 화면에 표시 되는 행의 수로 설정 하는 것입니다. 사용자가 화면의 크기를 조정 하면 응용 프로그램은 행 집합 크기를 적절 하 게 변경 합니다. 두 번째는 데이터 원본에 대 한 호출 수를 줄일 수 있도록 행 집합 크기를 100과 같은 큰 수로 설정 하는 것입니다. 가능 하면 응용 프로그램은 행 집합 내에서 로컬로 스크롤하고 행 집합 외부에서 스크롤하면 새 행을 페치합니다.  
  
 보고서와 같은 다른 응용 프로그램은 행 집합 크기를 응용 프로그램이 합리적으로 처리할 수 있는 최대 행 수로 설정 하는 경향이 있습니다. 더 큰 행 집합을 사용 하는 경우 행당 네트워크 오버 헤드가 줄어듭니다. 행 집합의 크기는 각 행의 크기 및 사용 가능한 메모리 양에 따라 달라질 수 있습니다.  
  
 행 집합 크기는 SQL_ATTR_ROW_ARRAY_SIZE *특성* 인수를 사용 하 여 **SQLSetStmtAttr** 에 대 한 호출로 설정 됩니다. 행이 인출 된 후에도 응용 프로그램에서 행 집합 크기를 변경 하거나, 새 행 집합 버퍼를 바인딩하거나 (바인딩 오프셋을 지정 하 여) 행이 인출 된 후에도 **SQLBindCol** 수 있습니다. 행 집합 크기 변경의 의미는 함수에 따라 달라 집니다.  
  
-   **Sqlfetch** 및 **sqlfetchscroll** 호출 시 행 집합 크기를 사용 하 여 페치할 행의 수를 결정 합니다. 그러나 **Sqlfetchscroll** SQL_FETCH_NEXT의 *fetch방향은* 이전 FETCH의 행 집합을 기반으로 커서를 증가 시킨 다음 현재 행 집합 크기를 기준으로 행 집합을 인출 합니다.  
  
-   **Sqlsetpos는** 이미 설정 된 행 집합에 대해 **sqlsetpos** 가 작동 하므로 **Sqlfetch** 또는 **sqlfetchscroll**에 대 한 이전 호출에서 적용 되는 행 집합 크기를 사용 합니다. 행 집합 크기가 변경 된 후에도 **SQLBulkOperations** 가 호출 되 면 **SQLSetPos** 는 새 행 집합 크기를 선택 합니다.  
  
-   **SQLBulkOperations** 는 인출 된 행 집합에 관계 없이 테이블에 대 한 작업을 수행 하기 때문에 호출 시 적용 되는 행 집합 크기를 사용 합니다.
