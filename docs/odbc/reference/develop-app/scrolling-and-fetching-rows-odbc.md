---
title: 행 스크롤 및 페치 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b326ed0c4e9a196904aa0f5c60b705243ef3bd97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061580"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>행 스크롤 및 페치(ODBC)
스크롤 가능 커서를 사용 하는 경우 응용 프로그램은 **Sqlfetchscroll** 을 호출 하 여 커서를 배치 하 고 행을 인출 합니다. **Sqlfetchscroll** 은 상대 스크롤 (다음, 이전 및 상대 *n* 행), 절대 스크롤 (first, last 및 row *n*)을 지원 하 고 책갈피를 기준으로 위치를 지정 합니다. **Sqlfetchscroll** 의 *Fetchorientation* 및 *fetchorientation* 인수는 다음 다이어그램에 표시 된 것 처럼 페치할 행 집합을 지정 합니다.  
  
 ![다음, 이전, 첫 번째 및 마지막 행 집합 페치](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **다음, 이전, 첫 번째 및 마지막 행 집합 페치**  
  
 ![절대, 상대 및 책갈피 지정된 행 집합 페치](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **절대, 상대 및 책갈피를 가진 행 집합 페치**  
  
 **Sqlfetchscroll** 커서를 지정 된 행에 배치 하 고 행 집합에서 행을 반환 하는 행을 반환 합니다. 지정 된 행 집합이 결과 집합의 끝과 겹치면 부분 행 집합이 반환 됩니다. 지정 된 행 집합이 결과 집합의 시작과 겹치면 결과 집합의 첫 번째 행 집합이 반환 됩니다. 자세한 내용은 [Sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 함수 설명을 참조 하세요.  
  
 일부 경우에는 응용 프로그램에서 데이터를 검색 하지 않고 커서를 배치할 수 있습니다. 예를 들어, 행이 있는지 여부를 테스트 하거나 네트워크를 통해 다른 데이터를 가져오지 않고 행의 책갈피를 가져올 수 있습니다. 이렇게 하려면 SQL_ATTR_RETRIEVE_DATA statement 특성을 SQL_RD_OFF로 설정 합니다. 책갈피 열 (있는 경우)에 바인딩된 변수는이 문 특성의 설정에 관계 없이 항상 업데이트 됩니다.  
  
 행 집합을 검색 한 후에는 응용 프로그램이 **SQLSetPos** 를 호출 하 여 행 집합의 특정 행에 배치 하거나 행 집합의 행을 새로 고칠 수 있습니다. **Sqlsetpos**를 사용 하는 방법에 대 한 자세한 내용은 [sqlsetpos를 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)를 참조 하세요.  
  
> [!NOTE]  
>  스크롤은 ODBC 2에서 지원 됩니다. **Sqlextendedfetch**별 *x* 드라이버. 자세한 내용은 [블록 커서, 스크롤 가능 커서 및](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)이전 버전과의 호환성에 대 한 드라이버 지침의 이전 버전과의 호환성을 참조 하세요.
