---
title: 상태 레코드의 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4b1e2ceea30ecb62dd96be283bb150d2e43385a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911098"
---
# <a name="sequence-of-status-records"></a>상태 레코드의 시퀀스
둘 이상의 상태 레코드가 반환 되는 경우 드라이버 관리자와 드라이버 등급을 매기고 다음 규칙에 따라 합니다. 가장 높은 순위 인 레코드는 첫 번째 레코드입니다. 레코드 (드라이버 관리자, 드라이버, 게이트웨이 및 등)의 소스 간주 되지 않습니다 레코드의 순위를 지정 합니다.  
  
-   **오류** 오류를 설명 하는 상태 레코드 가장 높은 순위를 가져야 합니다. 오류 레코드 중 레코드를 트랜잭션 오류 또는 가능한 트랜잭션 오류를 나타내는 다른 모든 레코드 outrank 합니다. 둘 이상의 레코드가 동일한 오류 조건을 설명 하는 경우 Open 그룹 CLI 사양 (03 HZ 통해 클래스)에 정의 된 Sqlstate outrank ODBC 정의 하 고 드라이버에서 정의 된 Sqlstate입니다.  
  
-   **구현에서 정의 된 데이터 값을 No** 드라이버 정의 된 데이터 없음 값 (클래스 02)를 설명 하는 상태 레코드에는 두 번째는 높은 순위입니다.  
  
-   **경고** 상태 레코드 (클래스 01) 경고를 설명 하는 가장 낮은 순위입니다. 둘 이상의 레코드가 동일한 경고 조건을 SQLSTATEs Open 그룹 CLI 사양에 정의 된 경고에 대해 설명 하는 경우에 ODBC 정의 하 고 드라이버에서 정의 된 Sqlstate outrank 합니다.  
  
 가장 높은 순위와 두 개 이상의 레코드가 없을 경우 레코드는 첫 번째 레코드 하 여 정의 되지 않았습니다. 다른 모든 레코드의 순서가 정의 되지 않습니다. 특히, 오류 하기 전에 경고가 나타날 수 있습니다, 때문에 함수가 SQL_SUCCESS 이외의 값을 반환 하는 경우 응용 프로그램 모든 상태 레코드를 확인 해야 합니다.
