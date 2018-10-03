---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17a88095611a5f551708f3950359063317368757
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694522"
---
# <a name="sequence-of-status-records"></a>상태 레코드의 시퀀스
상태 레코드를 두 개 이상 반환 되는 경우 드라이버 관리자와 드라이버 순위 다음 규칙에 따라 합니다. 가장 높은 순위를 사용 하 여 레코드는 첫 번째 레코드입니다. 원본 레코드 (드라이버 관리자, 드라이버, 게이트웨이 및 등)의 간주 되지 않습니다 레코드 순위를 지정 합니다.  
  
-   **오류** 오류를 설명 하는 상태 레코드 가장 높은 순위를 가집니다. 오류 레코드 간에 트랜잭션 오류 또는 가능한 트랜잭션 오류를 나타내는 레코드는 다른 모든 레코드 outrank 합니다. 둘 이상의 레코드가 동일한 오류 조건이 설명 하는 경우 (HZ 클래스 03) 열기 그룹 CLI 사양에 정의 된 Sqlstate outrank ODBC 정의 및 드라이버에서 정의 된 Sqlstate입니다.  
  
-   **구현 시 정의 된 데이터 값 없음** 드라이버에서 정의 된 데이터가 없는 값 (클래스 02)을 설명 하는 상태 레코드에는 두 번째가 가장 높은 순위입니다.  
  
-   **경고** (클래스 01) 경고를 설명 하는 상태 레코드 가장 낮은 순위를 가집니다. 둘 이상의 레코드 SQLSTATEs 열기 그룹 CLI 사양에 정의 된 경고를 동일한 경고 조건에 설명 하는 경우 ODBC 정의 및 드라이버에서 정의 된 Sqlstate outrank 합니다.  
  
 가장 높은 순위를 사용 하 여 둘 이상의 레코드의 경우은 첫 번째 레코드는 레코드 하 여 정의 되지 않았습니다. 다른 모든 레코드의 순서가 정의 되지 않습니다. 특히 오류 전에 경고가 나타날 수 있습니다, 되므로 함수가 SQL_SUCCESS 이외의 값을 반환 하는 경우 응용 프로그램 상태 레코드를 모두 확인 해야 합니다.
