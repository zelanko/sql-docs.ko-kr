---
title: 업데이트 데이터 개요 | Microsoft Docs
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
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64f61563836b7deddc65b2dc61307ed686f030ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915898"
---
# <a name="updating-data-overview"></a>업데이트 데이터 개요
SQL 문을 실행 하 여 또는 호출 하 여 응용 프로그램 데이터를 업데이트할 수 **SQLSetPos** 또는 **SQLBulkOperations**합니다. **업데이트**, **삭제**, 및 **삽입** 문 데이터 원본에 직접 역할 및 일반적으로 드라이버에서 지원 합니다. 업데이트 검색 및 delete 문을 변경 하려면 행의 지정을 포함 합니다. 배치 update 및 delete 문 및 **SQLSetPos** 커서를 통해 데이터 원본에 대해 작동 하 고 덜 광범위 하 게 지원 됩니다.  
  
 커서 결과 집합을이 섹션에 설명 된 방법의 변경을 검색할 수 있는지 여부를 어떻게 구현 되었는지 및 커서의 형식에 따라 달라 집니다. 정방향 전용 커서 행 다시 방문 하지 않는 하 고 변경 내용을 검색 하지 않습니다. 스크롤 가능 커서가 변경 내용을 검색할 수 있는지 여부에 대 한 정보를 참조 하십시오. [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [UPDATE, DELETE 및 INSERT 문](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [현재 위치 업데이트 및 Delete 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [현재 위치 업데이트 및 Delete 문 시뮬레이션](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [영향을 받는 행 수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [SQLSetPos를 사용하여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [SQLBulkOperations로 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Long 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
