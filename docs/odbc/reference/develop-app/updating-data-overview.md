---
title: 데이터 개요 업데이트 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9972ab61f041385ae4ca616df093ae63ad7a47d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300389"
---
# <a name="updating-data-overview"></a>데이터 업데이트 개요
응용 프로그램은 SQL 문을 실행하거나 **SQLSetPos** 또는 **SQLBulkOperations**를 호출하여 데이터를 업데이트할 수 있습니다. **UPDATE,** **DELETE**및 **INSERT** 문은 데이터 원본에 직접 작용하며 일반적으로 드라이버에서 지원됩니다. 검색된 업데이트 및 delete 문은 변경할 행의 사양을 포함합니다. 위치 업데이트 및 삭제 문 및 **SQLSetPos** 커서를 통해 데이터 원본에 작동 하 고 덜 광범위 하 게 지원 됩니다.  
  
 이 섹션에 설명된 메서드를 사용하여 커서가 결과 집합에 대한 변경 내용을 검색할 수 있는지 여부는 커서의 유형과 구현 방법에 따라 달라집니다. 정방향 전용 커서는 행을 다시 방문하지 않으므로 변경 내용을 감지하지 못합니다. 스크롤 가능한 커서가 변경 내용을 검색할 수 있는지 여부에 대한 자세한 내용은 [스크롤 가능한 커서 를](../../../odbc/reference/develop-app/scrollable-cursors.md)참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [UPDATE, DELETE 및 INSERT 문](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [현재 위치 업데이트 및 Delete 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [현재 위치 업데이트 및 Delete 문 시뮬레이션](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [영향을 받는 행 수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [SQLSetPos를 사용하여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [SQLBulkOperations로 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Long 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
