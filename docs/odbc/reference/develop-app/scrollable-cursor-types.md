---
description: 스크롤 가능 커서 형식
title: 스크롤 가능 커서 유형 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c27ccd54bfe0ba099d78c002fce4c901e4bf8c1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476515"
---
# <a name="scrollable-cursor-types"></a>스크롤 가능 커서 형식
스크롤 가능한 커서는 정적, 동적, 키 집합 및 혼합의 네 가지 유형이 있습니다. 정적 커서는 변경 내용을 거의 검색 하지 않지만 구현 하기는 상대적으로 저렴 합니다. 동적 커서는 모든 변경 내용을 검색 하지만 구현 하는 데 비용이 많이 듭니다. 키 집합 커서와 혼합 커서는 사이에서 대부분의 변경 내용을 검색 하지만 동적 커서 보다 저렴 한 비용으로 검색 합니다.  
  
 다음 용어는 스크롤 가능한 각 커서 유형의 특성을 정의 하는 데 사용 됩니다.  
  
-   **업데이트, 삭제 및 삽입이 있습니다.** **SQLBulkOperations** 또는 **SQLSetPos** 를 호출 하거나 위치 지정 update 또는 delete 문을 사용 하 여 커서를 통해 수행 된 업데이트, 삭제 및 삽입  
  
-   **기타 업데이트, 삭제 및 삽입** 동일한 트랜잭션의 다른 작업에서 수행한 작업, 다른 트랜잭션을 통해 수행 된 작업, 다른 응용 프로그램에서 수행한 작업 등 커서에 의해 수행 되지 않은 업데이트, 삭제 및 삽입  
  
-   **멤버 자격.** 결과 집합의 행 집합입니다.  
  
-   **주문을.** 커서에서 행이 반환 되는 순서입니다.  
  
-   **값인.** 결과 집합의 각 행에 있는 값입니다.  
  
 데이터를 업데이트, 삭제 및 삽입 하는 방법에 대 한 자세한 내용은 [데이터 업데이트 개요](../../../odbc/reference/develop-app/updating-data-overview.md)를 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 정적 커서](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 동적 커서](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [키 집합 커서](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [혼합 커서](../../../odbc/reference/develop-app/mixed-cursors.md)
