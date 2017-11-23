---
title: "하려면 ODBC 정적 커서가 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b8073bd935f010a91c9dde8863e1731ab3032a7e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-static-cursors"></a>하려면 ODBC 정적 커서가
정적 커서가 static으로 표시 되는 결과 집합 하나입니다. 멤버 자격, 순서 또는 커서가 열린 후에 결과 집합의 값에 대 한 변경 내용을 일반적으로 감지 하지 못합니다. 예를 들어 정적 커서를 행 및 다른 응용 프로그램을 인출 합니다. 그런 다음 해당 행을 업데이트 합니다. 정적 커서 다시 행을 발견 하는 값에서 다른 응용 프로그램에의 한 변경 되더라도 변경 된지 않습니다.  
  
 이 작업을 수행 하는 데 필요 하지는 않지만 정적 커서는 자체 업데이트, 삭제 및 삽입, 검색할 수 있습니다. SQL_STATIC_SENSITIVITY 옵션을 통해 보고 되는 특정 정적 커서에 이러한 변경 내용을 검색 하는 여부 **SQLGetInfo**합니다. 정적 커서는 업데이트, 삭제 및 삽입 하는 다른 검색 하지 않습니다.  
  
 행 상태 배열이 SQL_ATTR_ROW_STATUS_PTR 문 특성에 지정 된 모든 행에 대 한 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, 또는 SQL_ROW_ERROR 포함할 수 있습니다. 업데이트, 삭제 또는 커서 이러한 변경 내용이 감지할 수 가정 커서에 의해 삽입 된 행에 대 한 SQL_ROW_UPDATED은 SQL_ROW_DELETED, 또는 SQL_ROW_ADDED를 반환 합니다.  
  
 정적 커서는 일반적으로 결과 집합의 행을 잠가 또는 복사 하 여 구현 하거나 집합 결과의 스냅숏이 됩니다. 행 잠금 비교적 쉽게 할 경우에 동시성이 크게 감소 단점은 있습니다. 복사본을 만드는 큰 동시성을 허용 하 고 자체 업데이트, 삭제를 추적 하기 위해 커서를 허용 하 고 복사본을 수정 하 여 삽입 합니다. 그러나 복사본 비용이 더 듭니다를 확인 하 고 해당 데이터는 다른 사용자가 변경 될 때마다 기본 데이터에서 벗어날 수 있습니다.
