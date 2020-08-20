---
description: 스크롤 가능 커서
title: 스크롤 가능 커서 | Microsoft Docs
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
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c347dcb130a2f1f899f2e1b83ae28289ff0a923
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476485"
---
# <a name="scrollable-cursors"></a>스크롤 가능 커서
최신 화면 기반 응용 프로그램에서는 사용자가 앞뒤로 스크롤하고 데이터를 전달 합니다. 이러한 응용 프로그램의 경우 이전에 인출 된 행으로 돌아가는 것은 문제가 됩니다. 커서를 닫았다가 다시 연 다음 커서가 필요한 행에 도달할 때까지 행을 인출 하는 것이 한 가지 가능성은 있습니다. 또 다른 가능성은 결과 집합을 읽고, 로컬로 캐시 하 고, 응용 프로그램에서 스크롤을 구현 하는 것입니다. 두 경우 모두 작은 결과 집합에 대해서만 작동 하며, 후자의 경우에는 구현 하기가 어렵습니다. 더 나은 방법은 *스크롤 가능한 커서를* 사용 하는 것입니다 .이 커서는 결과 집합에서 앞뒤로 이동할 수 있습니다.  
  
 스크롤할 수 있는 *커서* 는 사용자가 데이터를 앞뒤로 스크롤 하는 최신 화면 기반 응용 프로그램에서 일반적으로 사용 됩니다. 그러나 스크롤 가능한 커서는 앞 으로만 이동 가능한 커서 보다 일반적으로 비용이 많이 들기 때문에 응용 프로그램은 전방 전용 커서에서 작업을 수행 하지 않는 경우에만 스크롤 가능 커서를 사용 해야 합니다.  
  
 뒤로 이동 하는 기능을 통해 전방 전용 커서에 적용할 수 없는 질문을 발생 시킬 수 있습니다. 스크롤할 수 있는 커서가 이전에 인출 된 행의 변경 내용을 검색 해야 하나요? 즉, 업데이트, 삭제 및 새로 삽입 된 행을 검색 해야 하나요?  
  
 이 질문은 결과 집합의 정의 (특정 조건과 일치 하는 행 집합)가 행을 검사할 때 해당 기준과 일치 하는지 여부를 확인 하지 않고 행이 인출 될 때마다 동일한 데이터를 포함 해야 하는지 여부를 확인 하기 때문에 발생 합니다. 이전에 생략 된 커서를 사용 하 여 행이 삽입 또는 삭제 되었는지 여부를 검색할 수 있습니다. 반면 후자를 사용 하면 업데이트 된 데이터를 검색할 수 있습니다.  
  
 때로는 변경 사항을 검색 하는 기능이 유용 합니다. 예를 들어, 회계 응용 프로그램은 모든 변경 내용을 무시 하는 커서를 요구 합니다. 커서가 최신 변경 내용을 표시 하는 경우에는 책을 분산할 수 없습니다. 반면에 항공 예약 시스템에는 데이터에 대 한 최신 변경 내용을 표시 하는 커서가 필요 합니다. 이러한 커서가 없으면 데이터베이스를 지속적으로 다시 쿼리하여 최신 비행 가용성을 표시 해야 합니다.  
  
 ODBC는 서로 다른 응용 프로그램의 요구 사항을 다루기 위해 스크롤 가능한 네 가지 커서 유형을 정의 합니다. 이러한 커서는 비용 및 결과 집합에 대 한 변경 내용을 검색 하는 기능에 따라 달라 집니다. 스크롤할 수 있는 커서가 행의 변경 내용을 검색할 수 있으면 해당 행을 다시 페치 할 때만 검색할 수 있습니다. 데이터 원본에서 현재 인출 된 행의 변경 내용을 커서에 알릴 수 있는 방법은 없습니다. 참고로, 변경 내용에 대 한 가시성도 트랜잭션 격리 수준에 의해 제어 됩니다. 자세한 내용은 [트랜잭션 격리](../../../odbc/reference/develop-app/transaction-isolation.md)를 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [스크롤 가능 커서 형식](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [스크롤 가능 커서 사용](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [상대 및 절대 스크롤](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [책갈피](../../../odbc/reference/develop-app/bookmarks-odbc.md)
