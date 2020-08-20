---
description: 상태 레코드의 시퀀스
title: 상태 레코드의 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2cb519cab987a1abd924f1b779a7f07c3201475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476455"
---
# <a name="sequence-of-status-records"></a>상태 레코드의 시퀀스
두 개 이상의 상태 레코드가 반환 되는 경우 드라이버 관리자와 드라이버는 다음 규칙에 따라 순위를 결정 합니다. 순위가 가장 높은 레코드는 첫 번째 레코드입니다. 레코드의 원본 (드라이버 관리자, 드라이버, 게이트웨이 등)은 레코드를 순위를 지정 하는 경우 고려 되지 않습니다.  
  
-   **오류** 오류를 설명 하는 상태 레코드의 순위가 가장 높습니다. 오류 레코드 중에서 트랜잭션 오류 또는 가능한 트랜잭션 오류를 나타내는 레코드는 다른 모든 레코드를 표시 합니다. 두 개 이상의 레코드가 동일한 오류 조건을 설명 하는 경우 Open Group CLI 사양 (클래스 03-HZ)에서 정의 된 SQLSTATEs는 ODBC 정의 및 드라이버 정의 SQLSTATEs입니다.  
  
-   **구현에서 정의 된 데이터 값 없음** 드라이버 정의 데이터 값 없음 (클래스 02)을 설명 하는 상태 레코드에는 두 번째 최고 순위가 있습니다.  
  
-   **경고** 경고 (클래스 01)를 설명 하는 상태 레코드의 순위가 가장 낮습니다. 두 개 이상의 레코드가 동일한 경고 조건을 설명 하는 경우 Open Group CLI 사양 outrank ODBC 정의 및 드라이버 정의 SQLSTATEs에서 정의한 경고 SQLSTATEs  
  
 순위가 가장 높은 레코드가 둘 이상 있는 경우 첫 번째 레코드에 해당 하는 레코드가 정의 되지 않습니다. 다른 모든 레코드의 순서는 정의 되지 않습니다. 특히 오류가 발생 하기 전에 경고가 나타날 수 있기 때문에 응용 프로그램은 함수가 SQL_SUCCESS 이외의 값을 반환할 때 모든 상태 레코드를 확인 해야 합니다.
